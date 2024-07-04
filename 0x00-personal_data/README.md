# 0x00. Personal Data

## Project Overview

This project focuses on handling Personally Identifiable Information (PII) in a secure and efficient manner. You'll learn to obfuscate sensitive information in logs, connect to a secure database, and implement secure password hashing and validation.

## Learning Objectives

By the end of this project, you should be able to:
- Identify examples of PII.
- Implement a log filter to obfuscate PII fields.
- Encrypt passwords and validate their correctness.
- Use environment variables to authenticate database connections securely.

## Requirements

- **Python Version**: 3.7
- **OS**: Ubuntu 18.04 LTS
- **Style Guide**: Follow `pycodestyle` (version 2.5)
- **Execution**: All scripts must be executable and end with a new line.
- **Documentation**: Each module, class, and function must have a descriptive docstring.
- **Type Annotations**: All functions should have type annotations.

## Tasks

### Task 0: Regex-ing

Create a function `filter_datum` that obfuscates specified fields in a log message.

**Function Signature**:
```python
def filter_datum(fields: List[str], redaction: str, message: str, separator: str) -> str:
```

**Description**:
- **fields**: List of strings to obfuscate.
- **redaction**: Replacement string for obfuscation.
- **message**: Log message containing the fields.
- **separator**: Character separating the fields in the log message.

Example usage:
```python
fields = ["password", "date_of_birth"]
message = "name=egg;email=eggmin@eggsample.com;password=eggcellent;date_of_birth=12/12/1986;"
print(filter_datum(fields, 'xxx', message, ';'))
# Output: name=egg;email=eggmin@eggsample.com;password=xxx;date_of_birth=xxx;
```

### Task 1: Log Formatter

Implement the `RedactingFormatter` class to filter sensitive information from log records.

**Class Structure**:
```python
import logging

class RedactingFormatter(logging.Formatter):
    REDACTION = "***"
    FORMAT = "[HOLBERTON] %(name)s %(levelname)s %(asctime)-15s: %(message)s"
    SEPARATOR = ";"

    def __init__(self, fields: List[str]):
        super().__init__(self.FORMAT)
        self.fields = fields

    def format(self, record: logging.LogRecord) -> str:
        # Obfuscate fields in the log record
```

**Usage**:
```python
message = "name=Bob;email=bob@dylan.com;ssn=000-123-0000;password=bobby2019;"
log_record = logging.LogRecord("my_logger", logging.INFO, None, None, message, None, None)
formatter = RedactingFormatter(fields=["email", "ssn", "password"])
print(formatter.format(log_record))
# Output: [HOLBERTON] my_logger INFO 2019-11-19 18:24:25,105: name=Bob;email=***;ssn=***;password=***;
```

### Task 2: Create Logger

Implement `get_logger` to create a logger named "user_data" with specific logging settings.

**Function Signature**:
```python
def get_logger() -> logging.Logger:
```

**Description**:
- The logger should log up to `INFO` level.
- Should use `RedactingFormatter` for formatting.
- Should not propagate messages to other loggers.

**PII_FIELDS**:
A tuple containing the PII fields: `("name", "email", "phone", "ssn", "password")`

**Usage**:
```python
logger = get_logger()
logger.info("This is a test log message.")
```

### Task 3: Connect to Secure Database

Implement `get_db` to connect to a MySQL database using environment variables for credentials.

**Function Signature**:
```python
def get_db() -> mysql.connector.connection.MySQLConnection:
```

**Description**:
- Retrieves database credentials from environment variables.
- Returns a MySQL connection object.

**Environment Variables**:
- `PERSONAL_DATA_DB_USERNAME`: Database username (default: `root`)
- `PERSONAL_DATA_DB_PASSWORD`: Database password (default: `""`)
- `PERSONAL_DATA_DB_HOST`: Database host (default: `localhost`)
- `PERSONAL_DATA_DB_NAME`: Database name

**Usage**:
```python
db = get_db()
cursor = db.cursor()
cursor.execute("SELECT * FROM users;")
for row in cursor:
    print(row)
cursor.close()
db.close()
```

### Task 4: Read and Filter Data

Implement the `main` function to fetch and log filtered user data from the database.

**Function Signature**:
```python
def main() -> None:
```

**Description**:
- Connects to the database using `get_db`.
- Retrieves all rows from the `users` table.
- Logs each row, obfuscating sensitive fields.

**Usage**:
```python
if __name__ == "__main__":
    main()
```

### Task 5: Encrypting Passwords

Implement `hash_password` to hash a password using bcrypt.

**Function Signature**:
```python
def hash_password(password: str) -> bytes:
```

**Description**:
- Returns a salted, hashed password.

**Usage**:
```python
print(hash_password("MyAmazingPassw0rd"))
```

### Task 6: Check Valid Password

Implement `is_valid` to validate a password against a hashed password.

**Function Signature**:
```python
def is_valid(hashed_password: bytes, password: str) -> bool:
```

**Description**:
- Returns `True` if the password matches the hashed password, `False` otherwise.

**Usage**:
```python
hashed_password = hash_password("MyAmazingPassw0rd")
print(is_valid(hashed_password, "MyAmazingPassw0rd"))  # Output: True
```

## Repository

- **GitHub Repository**: [alx-backend-user-data](https://github.com/paschalugwu/alx-backend-user-data)
- **Directory**: `0x00-personal_data`

**Note**: Ensure all your Python files are executable and follow the specified coding standards.

---

This README provides a structured overview of each task, ensuring you understand the objectives and can implement the necessary functions effectively. For full implementation details, refer to the source files in the repository.
