# 🛒 Ecommerce-FastAPI

A lightweight **RESTful E-commerce Product Management API** built with **Python, FastAPI, and Pydantic v2**.

The project demonstrates **CRUD operations, request validation, dependency injection, business-rule validation, search, filtering, sorting, pagination, nested Pydantic models, and JSON-based persistence**.

## 🚀 Project Overview

Ecommerce-FastAPI provides a backend API for managing products in an e-commerce application.

### Core capabilities

- Create, read, update, and delete products
- Search and filter products
- Sort products by price
- Pagination with limit/offset
- UUID-based product identification
- Pydantic v2 validation
- Nested Seller and Dimensions models
- Custom business-rule validation
- Computed product values
- FastAPI Dependency Injection
- Structured HTTP exception handling
- Automatic Swagger/OpenAPI documentation
- Environment-variable configuration

Product data is stored in `products.json` rather than a relational database, keeping the project lightweight and easy to understand.

---

## 🏗️ Architecture

The application follows a simple layered architecture:

```text
                    ┌─────────────────┐
                    │      Client     │
                    └────────┬────────┘
                             │ HTTP
                             ▼
                    ┌─────────────────┐
                    │   FastAPI API   │
                    │    main.py      │
                    └────────┬────────┘
                             │
                             │ Dependency Injection
                             ▼
                    ┌─────────────────┐
                    │  Service Layer  │
                    │ products.py     │
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │  products.json  │
                    │   Data Layer    │
                    └─────────────────┘

              Pydantic Schema / Validation
                       ▲
                       │
                Request / Response
```

### Layers

| Layer | Responsibility |
|---|---|
| API Layer | HTTP routes, requests, responses, exceptions |
| Validation Layer | Pydantic schemas and business rules |
| Service Layer | Product CRUD and data operations |
| Data Layer | JSON-based persistence |

---

## 📁 Project Structure

```text
fastapi-ecommerce/
│
├── app/
│   ├── main.py
│   ├── schema/
│   │   └── product.py
│   ├── service/
│   │   └── products.py
│   └── data/
│       └── products.json
└── README.md
```

### Module responsibilities

- **`app/main.py`** — FastAPI application, routes, request/response handling, dependency injection, exceptions.
- **`app/schema/product.py`** — Pydantic models, nested schemas, validation, computed fields, business rules.
- **`app/service/products.py`** — JSON loading/saving and product CRUD operations.
- **`app/data/products.json`** — Product persistence.

---

## 🔌 API Endpoints

### `GET /`

Returns basic application information.

### `GET /products`

Returns products with search, sorting, and pagination.

Examples:

```http
GET /products
GET /products?name=iphone
GET /products?sort_by_price=true
GET /products?limit=5
GET /products?offset=10
```

### `GET /products/{id}`

Retrieves a product using its UUID.

Returns `404` if the product does not exist.

### `POST /products`

Creates a product.

```text
Request
  ↓
Pydantic Validation
  ↓
Generate UUID + created_at
  ↓
Check Duplicate SKU
  ↓
Save JSON
  ↓
Return Product
```

### `PUT /products/{id}`

Updates a product and supports partial updates, including nested objects.

### `DELETE /products/{id}`

Deletes a product and persists the updated collection.

---

## 🧩 Pydantic Models

The project uses nested models:

```text
Product
├── Seller
└── Dimensions
```

### Product

Includes fields such as:

```text
id, sku, name, description, category, brand,
price, currency, discount, stock, rating,
tags, images, seller, dimensions, created_at
```

### Seller

```text
id
name
email
website
```

### Dimensions

```text
length
width
height
```

---

## ✅ Validation & Business Rules

The project demonstrates both field-level and model-level validation.

| Field / Rule | Validation |
|---|---|
| SKU | Format such as `ABC-123` |
| Price | `> 0` |
| Rating | `0–5` |
| Discount | `0–90%` |
| Stock | `>= 0` |
| Images | Valid URLs |
| Seller email | `EmailStr` validation |
| Seller website | URL + allowed-domain validation |

Cross-field rules include:

```text
stock == 0
    → is_active cannot be true
```

```text
discount > 0
    → rating cannot be zero
```

These rules are implemented using Pydantic model validators.

---

## 🧮 Computed Fields

### Final Price

```text
final_price = price × (1 - discount / 100)
```

### Product Volume

```text
volume = length × width × height
```

These values are calculated from existing product data rather than requiring clients to submit them.

---

## 🔄 Request Lifecycle

```text
Client
  ↓
FastAPI Route
  ↓
Dependency Injection
  ↓
Pydantic Validation
  ↓
Service Layer
  ↓
products.json
  ↓
Response
  ↓
Client
```

---

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| **Python** | Backend language |
| **FastAPI** | REST API framework |
| **Pydantic v2** | Data validation and schemas |
| **Uvicorn** | ASGI server |
| **Swagger UI / OpenAPI** | API documentation |
| **JSON** | Data persistence |
| **python-dotenv** | Environment variables |

---

## ⚙️ Setup

### 1. Clone

```bash
git clone <your-repository-url>
cd fastapi-ecommerce
```

### 2. Create virtual environment

```bash
python -m venv .venv
```

Windows:

```bash
.venv\Scripts\activate
```

Linux/macOS:

```bash
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

> The project report notes that the supplied `requirements.txt` is currently empty, so it should be populated with the application's dependencies before relying on a clean-clone installation.

### 4. Configure environment variables

Create a `.env` file as required by the application.

Do not commit credentials or environment-specific secrets to Git.

### 5. Run the API

```bash
uvicorn app.main:app --reload
```

API:

```text
http://127.0.0.1:8000
```

Swagger:

```text
http://127.0.0.1:8000/docs
```

ReDoc:

```text
http://127.0.0.1:8000/redoc
```

---

## ⚠️ Current Limitations

The current implementation is intentionally lightweight. The project report identifies these limitations:

- JSON file instead of PostgreSQL/MySQL
- No authentication or authorization
- No SQLAlchemy ORM
- No Alembic migrations
- No automated unit tests
- No structured logging
- No Redis caching
- No Docker support
- No API versioning
- No repository pattern
- No CI/CD pipeline
- Limited configuration management

### JSON Persistence

Current flow:

```text
Read JSON
   ↓
Modify in memory
   ↓
Write JSON
```

This is simple for a learning project, but it does not provide the concurrency, transactions, and scalability expected from a production database-backed system.

---

## 🔮 Future Improvements

The project can evolve toward a production-oriented e-commerce backend by adding:

- PostgreSQL
- SQLAlchemy
- Alembic migrations
- JWT authentication
- Role-based authorization
- Product categories
- Shopping cart
- Orders
- Inventory management
- Payment integration
- Redis caching
- Async database operations
- Docker / Docker Compose
- Pytest
- GitHub Actions CI/CD
- Structured logging
- Cloud deployment
- Monitoring and observability

---

## 🎯 What This Project Demonstrates

```text
Python
  +
FastAPI
  +
REST API Design
  +
CRUD
  +
Pydantic v2
  +
Nested Models
  +
Custom Validation
  +
Business Rules
  +
Dependency Injection
  +
Pagination
  +
Filtering
  +
Sorting
  +
Exception Handling
  +
OpenAPI / Swagger
  +
JSON Persistence
```

This project demonstrates practical **Python backend and FastAPI fundamentals** and provides a foundation that can be extended into a database-backed production-style e-commerce service.

---

## 💼 Resume Description

**Ecommerce Backend API — FastAPI**

- Developed a RESTful e-commerce product management API using **Python and FastAPI**, implementing CRUD operations, search, sorting, filtering, and pagination.
- Designed a layered backend architecture separating **API routes, Pydantic validation schemas, business logic, and JSON data persistence**.
- Implemented **Pydantic v2 nested models, custom validators, computed fields, UUID-based identification, and cross-field business rules** for robust product validation.
- Applied **FastAPI Dependency Injection** and structured HTTP exception handling while exposing interactive **OpenAPI/Swagger documentation**.

---

## 👨‍💻 Author

**Yogendra Gupta**

Data Science | Python Backend Development
