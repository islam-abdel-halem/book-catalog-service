# Book Catalog Service API  
## Software Architecture Design Document

---

## 1. Introduction

This document defines the proposed software architecture and development approach for the **Book Catalog Service API**.  
The service is designed to provide a scalable and maintainable RESTful API for managing a catalog of books.

The document covers:
- Selected Software Development Lifecycle (SDLC)
- Core API endpoint definitions
- High-level system architecture
- Application of core software design principles
- Component and sequence diagram descriptions

---

## 2. Software Development Lifecycle (SDLC)

### 2.1 Selected SDLC Model: Agile

The **Agile** development model is selected for the Book Catalog Service API.

### 2.2 Justification

Agile is suitable for this project because:
- API requirements may evolve over time
- It supports incremental feature delivery
- Continuous feedback improves design quality
- Frequent testing and refactoring enhance maintainability

Development will be organized into short iterations (sprints), each delivering incremental improvements to the API.

---

## 3. System Architecture Overview

The Book Catalog Service API follows a **layered architecture** that separates responsibilities across components.  
The system communicates using RESTful HTTP endpoints with JSON payloads.

### Core Components:
- Client
- API Gateway
- Book Catalog Service (Service Layer)
- Database

This architecture supports scalability, modularity, and future extensibility.

---

## 4. API Design

### 4.1 Base URL
```
/api/v1
```

### 4.2 Core API Endpoints

#### 4.2.1 Get All Books
**Endpoint**
```
GET /books
```

**Response (200 OK)**
```json
[
  {
    "isbn": "9780132350884",
    "title": "Clean Code",
    "author": "Robert C. Martin",
    "publishedYear": 2008,
    "category": "Software Engineering"
  }
]
```

---

#### 4.2.2 Get Book by ISBN
**Endpoint**
```
GET /books/{isbn}
```

**Response (200 OK)**
```json
{
  "isbn": "9780132350884",
  "title": "Clean Code",
  "author": "Robert C. Martin",
  "publishedYear": 2008,
  "category": "Software Engineering"
}
```

**Error (404 Not Found)**
```json
{
  "error": "Book not found"
}
```

---

#### 4.2.3 Add a New Book
**Endpoint**
```
POST /books
```

**Request Body**
```json
{
  "isbn": "9780132350884",
  "title": "Clean Code",
  "author": "Robert C. Martin",
  "publishedYear": 2008,
  "category": "Software Engineering"
}
```

**Response (201 Created)**
```json
{
  "message": "Book added successfully",
  "isbn": "9780132350884"
}
```

---

#### 4.2.4 Delete a Book
**Endpoint**
```
DELETE /books/{isbn}
```

**Response (200 OK)**
```json
{
  "message": "Book deleted successfully"
}
```

---

## 5. Software Design Principles

### 5.1 Separation of Concerns

Responsibilities are clearly divided:
- **Client**: User interaction
- **API Gateway**: Request routing and validation
- **Service Layer**: Business logic
- **Database**: Data persistence

This separation improves maintainability and reduces coupling.

---

### 5.2 Modularity

Each component is designed as an independent module with a specific responsibility.  
This allows easier testing, scaling, and future enhancements without impacting the entire system.

---

## 6. Component Diagram (Textual Description)

### Title
**Book Catalog Service – Component Diagram**

### Components
- **Client**  
  Web or mobile application sending REST requests

- **API Gateway**  
  Entry point handling routing and validation

- **Book Catalog Service**  
  Business logic and CRUD operations

- **Database**  
  Stores book data (ISBN, title, author, year, category)

### Relationships
- Client → API Gateway  
- API Gateway → Book Catalog Service  
- Book Catalog Service → Database  

---

## 7. Sequence Diagram (Textual Description)

### Title
**Sequence Diagram – Add New Book (POST /books)**

### Actors
- Client
- API Gateway
- Book Catalog Service
- Database

### Interaction Flow
1. Client sends `POST /books` request with book data
2. API Gateway validates and forwards the request
3. Book Catalog Service validates input and checks ISBN
4. Service inserts the book into the database
5. Database confirms successful insertion
6. Service creates success response
7. API Gateway returns `201 Created` to the client

---

## 8. Conclusion

This document presents a complete architectural design for the Book Catalog Service API.  
By applying Agile development practices and core software engineering principles such as **Separation of Concerns** and **Modularity**, the proposed architecture ensures scalability, maintainability, and clarity.

This design provides a strong foundation for future development and enhancement of the service.
