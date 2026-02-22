# Inventory Management REST API

A secure REST API built with FastAPI and PostgreSQL for tracking inventory items. Features full CRUD operations, JWT-based authentication, and interactive API documentation.

## Features

- **Full CRUD Operations** - Create, read, update, and delete inventory items
- **JWT Authentication** - Secure user registration and login with token-based auth
- **PostgreSQL Database** - Robust relational database with proper indexing
- **Password Hashing** - Secure password storage using bcrypt
- **Interactive Documentation** - Auto-generated Swagger/OpenAPI docs
- **Input Validation** - Request validation using Pydantic schemas

## Tech Stack

- **Backend**: Python 3.11+, FastAPI
- **Database**: PostgreSQL
- **Authentication**: JWT (JSON Web Tokens), bcrypt
- **ORM**: SQLAlchemy
- **API Documentation**: OpenAPI/Swagger

## Prerequisites

- Python 3.11 or higher
- PostgreSQL
- Git

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/Dinurian123/inventory-api.git
   cd inventory-api
   ```

2. **Create and activate virtual environment**
   ```bash
   python -m venv venv
   
   # Windows
   venv\Scripts\activate
   
   # Mac/Linux
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install fastapi uvicorn psycopg2-binary sqlalchemy python-jose passlib bcrypt
   ```

4. **Set up PostgreSQL database**
   - Install PostgreSQL if you haven't already
   - Create a database named `inventory_db`
   - Update the database URL in `app/database.py` with your credentials:
     ```python
     DATABASE_URL = "postgresql://postgres:YOUR_PASSWORD@localhost:5432/inventory_db"
     ```

5. **Run the application**
   ```bash
   uvicorn app.main:app --reload
   ```

6. **Access the API**
   - API: http://127.0.0.1:8000
   - Interactive docs: http://127.0.0.1:8000/docs

## API Endpoints

### Authentication

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/register` | Register a new user | No |
| POST | `/token` | Login and get access token | No |

### Inventory Items

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/items` | Create a new item | Yes |
| GET | `/items` | Get all items | Yes |
| GET | `/items/{id}` | Get a specific item | Yes |
| PUT | `/items/{id}` | Update an item | Yes |
| DELETE | `/items/{id}` | Delete an item | Yes |

## Authentication

This API uses JWT (JSON Web Tokens) for authentication.

1. **Register a new user**
   ```bash
   POST /register
   {
     "username": "testuser",
     "password": "password123"
   }
   ```

2. **Login to get access token**
   ```bash
   POST /token
   Form Data:
   - username: testuser
   - password: password123
   ```

3. **Use the token in requests**
   - In Swagger docs: Click "Authorize" button and enter your credentials
   - In API calls: Add header `Authorization: Bearer YOUR_TOKEN`

##  Example Usage

### Register a User
```bash
curl -X POST "http://127.0.0.1:8000/register" \
  -H "Content-Type: application/json" \
  -d '{"username": "john", "password": "secret123"}'
```

### Login
```bash
curl -X POST "http://127.0.0.1:8000/token" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "username=john&password=secret123"
```

### Create an Item (with authentication)
```bash
curl -X POST "http://127.0.0.1:8000/items" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Laptop Charger",
    "description": "65W USB-C charger",
    "quantity": 15,
    "price": 29.99
  }'
```

### Get All Items
```bash
curl -X GET "http://127.0.0.1:8000/items" \
  -H "Authorization: Bearer YOUR_TOKEN"
```

## Project Structure

```
inventory-api/
├── app/
│   ├── __init__.py
│   ├── main.py           # FastAPI app and endpoints
│   ├── database.py       # Database connection
│   ├── models.py         # SQLAlchemy models
│   ├── schemas.py        # Pydantic schemas
│   └── auth.py           # Authentication logic
├── .gitignore
├── requirements.txt
└── README.md
```

## Security Features

- Passwords are hashed using bcrypt before storage
- JWT tokens expire after 30 minutes
- Protected endpoints require valid authentication
- SQL injection protection through SQLAlchemy ORM

## Deployment

This API can be deployed on platforms like:
- Render
- Railway
- Fly.io
- Heroku


## Author

**Javier Bigio Dávila**
- GitHub: [@Dinurian123](https://github.com/Dinurian123)
- Email: Javibig16@gmail.com

## Acknowledgments

Built as part of a software development portfolio project to demonstrate:
- RESTful API design
- Database architecture
- Authentication implementation
- Modern Python web development practices

