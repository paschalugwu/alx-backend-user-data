# User Authentication Service

## Overview
This project focuses on implementing a user authentication service using Python and Flask. The objective is to understand the various steps involved in creating an authentication system from scratch, which includes handling user registration, password hashing, session management, and more.

## Learning Objectives
By the end of this project, you should be able to:
- Declare API routes in a Flask app.
- Get and set cookies.
- Retrieve request form data.
- Return various HTTP status codes.

## Requirements
- Allowed editors: `vi`, `vim`, `emacs`
- Files will be interpreted/compiled on Ubuntu 18.04 LTS using `python3` (version 3.7)
- All files should end with a new line
- First line of all files should be `#!/usr/bin/env python3`
- Code should use `pycodestyle` style (version 2.5)
- Use `SQLAlchemy` 1.3.x
- All files must be executable
- Modules, classes, and functions should have documentation
- Functions should be type annotated
- Flask app should only interact with Auth and never with DB directly
- Only public methods of Auth and DB should be used outside these classes

## Setup
To get started, install bcrypt:
```sh
pip3 install bcrypt
```

## Tasks

### 0. User Model
Create a SQLAlchemy model named `User` for a database table `users` with the following attributes:
- `id`: Integer primary key
- `email`: Non-nullable string
- `hashed_password`: Non-nullable string
- `session_id`: Nullable string
- `reset_token`: Nullable string

### 1. Create User
Implement the `add_user` method in the `DB` class, which adds a new user to the database with email and hashed password.

### 2. Find User
Implement the `find_user_by` method in the `DB` class to find a user based on arbitrary keyword arguments. Handle `NoResultFound` and `InvalidRequestError` exceptions.

### 3. Update User
Implement the `update_user` method in the `DB` class to update a user's attributes based on given keyword arguments. Raise a `ValueError` for invalid attributes.

### 4. Hash Password
Define the `_hash_password` method to hash a password using `bcrypt.hashpw` and return the salted hash.

### 5. Register User
Implement the `register_user` method in the `Auth` class to register a new user. If a user with the given email already exists, raise a `ValueError`.

### 6. Basic Flask App
Set up a basic Flask app with a single GET route `/` that returns a JSON payload `{"message": "Bienvenue"}`.

### 7. Register User Endpoint
Implement the `/users` route in the Flask app to register a user. Expect form data fields `email` and `password`. Return appropriate JSON responses based on registration success or failure.

### 8. Credentials Validation
Implement the `valid_login` method in the `Auth` class to validate user credentials using `bcrypt.checkpw`.

### 9. Generate UUIDs
Implement the `_generate_uuid` function to return a string representation of a new UUID.

### 10. Get Session ID
Implement the `create_session` method in the `Auth` class to generate and store a new session ID for a user.

### 11. Log In
Implement the `/sessions` route to log in a user. Validate credentials, create a session, and set the session ID as a cookie in the response. Return a JSON payload with login status.

## Repository Structure
```
alx-backend-user-data
├── 0x03-user_authentication_service
│   ├── app.py
│   ├── auth.py
│   ├── db.py
│   └── user.py
└── README.md
```

## Running the App
To run the Flask app, use:
```sh
python3 app.py
```

You can test the registration and login endpoints using `curl` commands as described in the tasks.

## Conclusion
This project provides a hands-on approach to implementing a user authentication service from scratch, covering essential aspects like database management, password hashing, and session handling.
