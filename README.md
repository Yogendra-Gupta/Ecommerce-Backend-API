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


## Executive Summary

- Developed a RESTful E-commerce Backend API using Python and FastAPI, implementing complete CRUD operations for product management.
- Designed a modular backend architecture by separating API routes, business logic, validation schemas, and data access layers, improving code maintainability and scalability.
- Implemented advanced Pydantic v2 models with nested schemas, custom validators, computed fields, and business rule validation to ensure robust data integrity.
- Built REST endpoints supporting product creation, retrieval, update, deletion, search, filtering, sorting, and pagination for efficient product management.
- Implemented UUID-based product identification and comprehensive request validation with structured error handling using FastAPI's exception mechanisms.
- Applied Dependency Injection to create reusable and maintainable API components while reducing code duplication.
- Managed product data using JSON-based persistence with efficient read/write operations, providing a lightweight backend suitable for rapid prototyping.
- Developed self-documented APIs through FastAPI's automatic OpenAPI/Swagger documentation, enabling easy API testing and integration.
- Structured the project following backend development best practices, including layered architecture, reusable services, and environment-based configuration.

