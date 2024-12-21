# Python Pydantic

Pydantic is a Python library for **data validation** and **settings management** using Python type annotations. It allows you to define data structures or configurations and automatically validate and parse the input data against these structures. Pydantic ensures that data conforms to the specified types and formats while providing useful error messages when validation fails.

---

## Key Features of Pydantic:
1. **Data Validation**:
    - Automatically validates input data types and constraints.
    - Ensures data integrity by rejecting invalid or improperly formatted inputs.

2. **Parsing Data**:
    - Converts input data (e.g., strings, JSON) into strongly-typed Python objects.
    - Automatically handles type coercion, such as converting strings to integers or dates.

3. **BaseModel**:
    - Central to Pydantic, the `BaseModel` class is used to define data models with fields and their expected types.
    - Fields can have optional default values, constraints, or dependencies.

4. **Integration with Python Type Annotations**:
    - Leverages Python's `typing` module for specifying types like `str`, `int`, `List`, `Dict`, `Optional`, etc.

5. **Performance**:
    - Written in pure Python but highly optimized for speed.
    - Uses `cython` under the hood for better performance.

6. **Error Handling**:
    - Provides detailed error messages when input data doesn't match the expected schema, highlighting where the validation failed.

7. **Environment Settings Management**:
    - Used for managing application settings and configurations by parsing environment variables, configuration files, or other inputs.

8. **Extensibility**:
    - Allows for custom validators for more complex validation needs.

---

## Example: Defining and Validating a Model with Pydantic

### Basic Data Validation and Parsing

```python
from pydantic import BaseModel, ValidationError
from typing import List, Optional
from datetime import datetime

# Define a data model
class User(BaseModel):
    id: int
    name: str
    signup_date: datetime
    friends: List[int]
    is_active: Optional[bool] = True  # Optional field with a default value

# Valid input data
data = {
    "id": 1,
    "name": "John Doe",
    "signup_date": "2024-12-01T15:30:00",
    "friends": [2, 3, 4]
}

# Parse and validate input
user = User(**data)
print(user)
# Output:
# id=1 name='John Doe' signup_date=datetime.datetime(2024, 12, 1, 15, 30) friends=[2, 3, 4] is_active=True

# Invalid input data
try:
    invalid_data = {"id": "abc", "name": "Jane", "friends": "not_a_list"}
    User(**invalid_data)
except ValidationError as e:
    print(e)
# Output:
# 1 validation error for User
# id
#   value is not a valid integer (type=type_error.integer)
# friends
#   value is not a valid list (type=type_error.list)
```

### Default Values
```python
class User(BaseModel):
    id: int
    name: str
    is_active: bool = True  # Default value

user = User(id=1, name="Alice")
print(user)
```

### Type Coercion
```python
class User(BaseModel):
    id: int
    age: int

user = User(id="123", age="30")  # Strings will be converted to integers
print(user)
```

### Data Validation with Constrained Types
```python
from pydantic import BaseModel, Field, EmailStr, constr

class User(BaseModel):
    id: int
    name: constr(min_length=3, max_length=50)  # Name must be 3-50 characters long
    email: EmailStr  # Validates email addresses
    age: int = Field(..., ge=18, le=100)  # Age must be between 18 and 100

# Valid data
user = User(id=1, name="Alice", email="alice@example.com", age=25)
print(user)

# Invalid email or age raises ValidationError
# user = User(id=1, name="Bob", email="invalid-email", age=150)
```

### Nested Models
```python
class Address(BaseModel):
    city: str
    zip_code: str

class User(BaseModel):
    id: int
    name: str
    address: Address

input_data = {
    "id": 1,
    "name": "Alice",
    "address": {
        "city": "New York",
        "zip_code": "10001"
    }
}

user = User(**input_data)
print(user)
```

### Custom Validators
```python
from pydantic import BaseModel, validator

class User(BaseModel):
    id: int
    name: str
    age: int

    @validator('age')
    def check_age(cls, value):
        if value < 18:
            raise ValueError("Age must be at least 18")
        return value

user = User(id=1, name="Alice", age=25)
print(user)

# Raises ValidationError for age < 18
# invalid_user = User(id=2, name="Bob", age=15)
```

### Model Serialization
```python
class User(BaseModel):
    id: int
    name: str

user = User(id=1, name="Alice")

# To dictionary
print(user.dict())

# To JSON
print(user.json())
```

### Environment Variables with BaseSettings
```python
from pydantic import BaseSettings

class AppConfig(BaseSettings):
    app_name: str
    debug: bool = False

    class Config:
        env_file = ".env"  # Load variables from a .env file

# Example: .env file contains:
# APP_NAME=MyApp
# DEBUG=True

config = AppConfig()
print(config.app_name)  # Output: MyApp
print(config.debug)  # Output: True
```

### Using Aliases
```python
class User(BaseModel):
    id: int
    full_name: str = Field(..., alias="fullName")

data = {"id": 1, "fullName": "Alice Johnson"}
user = User(**data)
print(user.full_name)  # Output: Alice Johnson
```

### Immutable Models
```python
class User(BaseModel):
    id: int
    name: str

    class Config:
        frozen = True

user = User(id=1, name="Alice")
# user.name = "Bob"  # Raises a TypeError
```

## Common Use Cases for Pydantic:
1. **API Development**:
   - Validate request/response payloads in frameworks like **FastAPI** (Pydantic is the backbone of FastAPI for defining schemas).

2. **Configuration Management**:
   - Parse and validate environment variables or configuration files in applications.

3. **Data Serialization and Deserialization**:
   - Parse incoming data (e.g., JSON or CSV) into Python objects, and serialize Python objects into formats like JSON.

4. **Data Processing Pipelines**:
   - Validate and enforce schema for data flowing through ETL pipelines or other data processing systems.

---

## Advantages of Pydantic:
- **Strong integration with Python’s typing system**:
   - Makes it easier to define and enforce data structures with type annotations.

- **Clear, readable syntax for defining schemas**:
   - Pydantic provides a simple and intuitive way to define models, making code easier to understand.

- **Fast and efficient**:
   - Optimized for performance, suitable for high-throughput applications.

- **Excellent support for nested models and complex data structures**:
   - Pydantic handles nested data models and complex types with ease.

--- 

### Limitations:
- Pydantic is designed for **runtime validation and parsing**, not for compile-time type checking.
- It **doesn't enforce schema in databases**; it's strictly for Python application logic.
