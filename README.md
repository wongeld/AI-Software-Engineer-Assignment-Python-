# AI Experts Assignment 3

This repository contains the solution for the AI Experts Assignment.  
The goal is to set up a small Python project with reproducible installs, write focused tests, and implement minimal fixes.

---

## Project Overview

- **Python version:** 3.11  
- **Dependencies pinned** in `requirements.txt`  
- **Tests** written with `pytest`  
- **Dockerized** for CI-style, non-interactive test execution  

The project includes:

- `Dockerfile` for building and running tests in a container  
- `requirements.txt` with pinned dependencies  
- `tests/` directory containing test cases  

---

## How to Run the Tests

### Locally

1. **Create and activate a virtual environment:**
   ```bash
   python -m venv venv
   # Windows
   venv\Scripts\activate
   # macOS / Linux
   source venv/bin/activate

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt

3. **Run the tests:**
   ```bash
   python -m pytest -v

### Using Docker 

1. **Build the Docker image:**
   ```bash
   docker build -t ai-experts-assignment .

2. **Run the tests in a container:**
   ```bash
   docker run --rm ai-experts-assignment

*The container will automatically run the test suite in verbose mode using pytest.*

### On Google Colab

1. **Clone the repository:**
   ```bash
   !git clone <your-repository-url>
   %cd ai-experts-assignment-3

2. **Install dependencies:**
   ```bash
   !pip install -r requirements.txt

3. **Run the tests:**
   ```bash
   !python -m pytest -v