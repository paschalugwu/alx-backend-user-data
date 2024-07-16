# Basic Authentication Project

## Overview

This project focuses on understanding and implementing Basic Authentication on a simple API using Python and Flask. The goal is to learn about the authentication process and how to implement it step by step.

## Learning Objectives

By the end of this project, you should be able to explain:
- What authentication means
- What Base64 encoding is and how to encode a string in Base64
- The concept of Basic Authentication
- How to send the Authorization header

## Requirements

- All files are interpreted/compiled on Ubuntu 18.04 LTS using Python 3.7
- Follow `pycodestyle` (version 2.5)
- Ensure all files are executable and end with a new line
- Proper documentation for modules, classes, and functions

## Project Tasks

### Task 0: Simple-basic-API

**Objective:** 
- Set up a simple API with a User model. Users are stored via serialization/deserialization in files.
- Start the server and test the API.

**Steps:**
1. Install the necessary dependencies from `requirements.txt`.
2. Start the server using environment variables for host and port.
3. Use `curl` or a browser to interact with the API endpoint `/api/v1/status` to ensure it's working.

### Task 1: Error Handler - Unauthorized

**Objective:**
- Implement an error handler for HTTP 401 Unauthorized status code.

**Steps:**
1. Edit `api/v1/app.py` to add a new error handler for status code 401 that returns a JSON response `{"error": "Unauthorized"}`.
2. Add a new endpoint `/api/v1/unauthorized` in `api/v1/views/index.py` that raises a 401 error using `abort`.

### Task 2: Error Handler - Forbidden

**Objective:**
- Implement an error handler for HTTP 403 Forbidden status code.

**Steps:**
1. Edit `api/v1/app.py` to add a new error handler for status code 403 that returns a JSON response `{"error": "Forbidden"}`.
2. Add a new endpoint `/api/v1/forbidden` in `api/v1/views/index.py` that raises a 403 error using `abort`.

### Task 3: Auth Class

**Objective:**
- Create a class to manage API authentication.

**Steps:**
1. Create the folder `api/v1/auth` and the class `Auth` in `api/v1/auth/auth.py`.
2. Implement the following methods:
   - `require_auth(self, path: str, excluded_paths: List[str]) -> bool`
   - `authorization_header(self, request=None) -> str`
   - `current_user(self, request=None) -> TypeVar('User')`

### Task 4: Define Routes That Don't Need Authentication

**Objective:**
- Update the `require_auth` method to exclude certain paths from authentication.

**Steps:**
1. Modify `require_auth` to return `True` if the path is not in the list of excluded paths.
2. Ensure the method is slash tolerant.

### Task 5: Request Validation

**Objective:**
- Validate all requests to secure the API.

**Steps:**
1. Update `authorization_header` to return the value of the Authorization header if present.
2. In `api/v1/app.py`, initialize the `auth` variable based on the environment variable `AUTH_TYPE`.
3. Implement `before_request` to filter requests and handle authentication.

### Task 6: Basic Auth

**Objective:**
- Implement Basic Authentication by creating a `BasicAuth` class that inherits from `Auth`.

**Steps:**
1. Create the `BasicAuth` class in `api/v1/auth/basic_auth.py`.
2. Update `api/v1/app.py` to use `BasicAuth` based on the environment variable `AUTH_TYPE`.

### Task 7: Basic - Base64 Part

**Objective:**
- Extract the Base64 part of the Authorization header.

**Steps:**
1. Add the method `extract_base64_authorization_header` in `BasicAuth` to return the Base64 part of the header.
2. Ensure the method handles edge cases where the header is not properly formatted.

## Repository Structure

```
alx-backend-user-data
│
├── 0x01-Basic_authentication
│   ├── api
│   │   ├── v1
│   │   │   ├── app.py
│   │   │   ├── views
│   │   │   │   ├── index.py
│   │   ├── auth
│   │   │   ├── __init__.py
│   │   │   ├── auth.py
│   │   │   ├── basic_auth.py
│   ├── README.md
```

## Running the Project

1. Clone the repository.
2. Navigate to `0x01-Basic_authentication`.
3. Install the dependencies: `pip3 install -r requirements.txt`.
4. Start the server: `API_HOST=0.0.0.0 API_PORT=5000 AUTH_TYPE=basic_auth python3 -m api.v1.app`.
5. Use `curl` or a browser to interact with the API endpoints.
