# Pydantic Tutorial - Data Validation and Model Management

This project demonstrates the usage of Pydantic for data validation and model management in Python. Pydantic is a powerful data validation library that uses Python type annotations to validate and parse data.

## Features

- Basic Pydantic model creation and validation
- Optional fields and default values
- List field validation
- Nested model structures
- Custom field constraints and validation
- JSON schema generation

## Installation

```bash
pip install pydantic
```

## Examples

### 1. Basic Model

```python
from pydantic import BaseModel

class Person(BaseModel):
    name: str
    age: int
    city: str

person = Person(name="John", age=30, city="New York")
```

### 2. Optional Fields

```python
from typing import Optional

class Employee(BaseModel):
    id: int
    name: str
    department: str
    salary: Optional[float] = None
    is_active: Optional[bool] = True
```

### 3. List Fields

```python
from typing import List

class Classroom(BaseModel):
    room_number: int
    students: List[str]
    capacity: int
```

### 4. Nested Models

```python
class Address(BaseModel):
    street: str
    city: str
    zip_code: str

class Customer(BaseModel):
    name: str
    age: int
    address: Address
```

### 5. Field Constraints

```python
from pydantic import Field

class Item(BaseModel):
    name: str = Field(min_length=3, max_length=15)
    price: float = Field(ge=0, le=1000)
```

### 6. Email Validation

```python
class User(BaseModel):
    username: str = Field(..., min_length=3, max_length=15)
    email: str = Field(..., pattern=r"^[a-zA-Z0-9_.+-]+@[a-zA-Z0-9-]+\.[a-zA-Z0-9-.]+$")
```

## Key Features Demonstrated

1. **Type Validation**: Automatic validation of data types
2. **Optional Fields**: Support for optional fields with default values
3. **List Validation**: Validation of list elements
4. **Nested Models**: Complex data structures with nested models
5. **Field Constraints**: Custom validation rules using Field
6. **Pattern Matching**: Regular expression validation for fields
7. **JSON Schema**: Generation of JSON schema from models

## Error Handling

Pydantic provides detailed validation errors when data doesn't match the model's requirements. For example:

```python
try:
    invalid_val = Classroom(
        room_number=101,
        students=["John", "Jane", 10],  # Invalid: 10 is not a string
        capacity=30,
    )
except Exception as e:
    print(e)
```

## Requirements

- Python 3.11+
- pydantic

## License

This project is open source and available under the MIT License. 