# 0x02. Session Authentication

## Back-end Authentication

### Overview
This project focuses on implementing a Session Authentication system. The aim is to understand the mechanisms behind session-based authentication by building it from scratch, without using any external modules or frameworks.

### Background Context
In a production environment, it is advisable to use established libraries and frameworks for session authentication. However, for educational purposes, this project requires a step-by-step implementation to gain a deep understanding of session management.

### Learning Objectives
By the end of this project, you should be able to:
- Explain what authentication and session authentication mean.
- Understand what cookies are and how they are used in session management.
- Send and parse cookies in HTTP requests.

### Requirements
- Python 3.7 on Ubuntu 18.04 LTS
- Code should adhere to `pycodestyle` (version 2.5)
- All scripts should be executable
- Proper documentation for modules, classes, and functions

### Tasks

#### 0. Et moi et moi et moi!
Copy all work from the previous `0x06. Basic authentication` project. Implement a new endpoint `GET /users/me` to retrieve the authenticated User object. Update `@app.before_request` in `api/v1/app.py` and modify the route in `api/v1/views/users.py`.

#### 1. Empty session
Create a class `SessionAuth` inheriting from `Auth`. This class will be empty initially, serving as a base for session authentication. Ensure it integrates correctly by using environment variables to switch authentication mechanisms in `api/v1/app.py`.

#### 2. Create a session
Update `SessionAuth` to include:
- A class attribute `user_id_by_session_id` (an empty dictionary).
- An instance method `create_session(self, user_id: str = None) -> str` that generates and stores a session ID for a user ID.

#### 3. User ID for Session ID
Add an instance method `user_id_for_session_id(self, session_id: str = None) -> str` to `SessionAuth`. This method retrieves a User ID based on a session ID.

#### 4. Session cookie
Enhance `api/v1/auth/auth.py` with a method `session_cookie(self, request=None)` to extract the session cookie value from a request using the environment variable `SESSION_NAME`.

#### 5. Before request
Update the `@app.before_request` method in `api/v1/app.py` to exclude `/api/v1/auth_session/login/` from authentication and handle requests without an authorization header or session cookie by returning a `401` error.

#### 6. Use Session ID for identifying a User
Implement `current_user(self, request=None)` in `SessionAuth` to return a User instance based on the session cookie.

#### 7. New view for Session Authentication
Create a new Flask view to handle session authentication routes:
- In `api/v1/views/session_auth.py`, add a route `POST /auth_session/login` to handle login, validate credentials, and create a session.
- Add this view in `api/v1/views/__init__.py`.

#### 8. Logout
Update `SessionAuth` with a method `destroy_session(self, request=None)` to delete a user session. Add a route `DELETE /api/v1/auth_session/logout` in `api/v1/views/session_auth.py` to handle logout requests.

#### 9. Expiration?
Create `SessionExpAuth` inheriting from `SessionAuth` to include session expiration. Overload methods to handle session creation and validation with an expiration date.

#### 10. Sessions in database
Implement `SessionDBAuth` inheriting from `SessionExpAuth` to store sessions in a database. Create a new model `UserSession` in `models/user_session.py` to manage session persistence. Overload methods to handle session creation, retrieval, and destruction from the database.

### Usage
To use this authentication system, set the appropriate environment variables and ensure all necessary routes and handlers are configured in your Flask application.

### Conclusion
This project provides a comprehensive understanding of session-based authentication by building it from the ground up. By following the steps outlined, you'll gain practical insights into managing user sessions, cookies, and authentication mechanisms in a web application.
