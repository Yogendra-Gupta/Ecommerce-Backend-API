# Ecommerce-Backend-API

The project is a small FastAPI-based E-commerce Product Management API that demonstrates REST API development, request validation using Pydantic, dependency injection, CRUD operations, filtering, sorting, pagination, and JSON-based data persistence.

---

## Project Objective
The project implements a RESTful backend API for managing products in an e-commerce application.

Instead of using a database, product information is stored inside a JSON file.

The application demonstrates:
- REST API development
- CRUD operations
- Validation
- Dependency Injection
- Business Rule Validation
- Pagination
- Filtering
- Sorting
- Nested Data Models
---

## Technical Skills Demonstrated
- Python
- FastAPI
- REST APIs
- Pydantic
- CRUD Operations
- Dependency Injection
- JSON Data Management
- API Validation
- OpenAPI/Swagger
- Uvicorn
- Modular Architecture

---

## Project Folder Structure

```
ecommerce-backend-api/
│
├── app/
│   │
│   ├── main.py
│   │
│   ├── schema/
│   │      product.py
│   │
│   ├── service/
│   │      products.py
│   │
│   ├── data/
│          products.json
│    
├── requirements.txt
```
---

## Module Explanation

This file acts as the API Controller.

Responsibilities include:

- Creating FastAPI app
- Defining routes
- Receiving requests
- Returning responses
- Calling service functions
- Exception handling
---




