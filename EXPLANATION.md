# Bug Explanation

## What was the bug?
`Client.request` didn’t refresh the OAuth2 token when `self.oauth2_token` was a dictionary.  
The test `test_api_request_refreshes_when_token_is_dict` failed because only `None` or expired `OAuth2Token` objects triggered a refresh.

## Why did it happen?
Original code: in `app/http_client.py`:
```python
if not self.oauth2_token or (
    isinstance(self.oauth2_token, OAuth2Token) and self.oauth2_token.expired
):
```
only triggered a refresh if `oauth2_token` was falulty like `None` or if it was an instance of `OAuth2Token` and expired. 

If `oauth2_token` was a `dict`, `not self.oauth2_token` was false, and `isinstance(self.oauth2_token, OAuth2Token)` was also false, so no refresh occurred.

## Fix
The fix adds an explicit check for the dictionary type:
```python
if (
    not self.oauth2_token
    or isinstance(self.oauth2_token, dict)
    or (isinstance(self.oauth2_token, OAuth2Token) and self.oauth2_token.expired)
):
```
This ensures that if the token is passed as a dictionary (which the test case and `__init__` type hint suggest is possible), it will be refreshed into a proper `OAuth2Token` object before use.

## One realistic case / edge case your tests still don’t cover
The current tests do not cover the case where refresh itself fails (e.g., network error or invalid credentials).
