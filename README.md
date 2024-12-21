# Blog Platform Backend

This repository contains the backend code for a blogging platform that supports user authentication, role-based access control, and CRUD operations for blogs. The platform features two roles: **Admin** and **User**, each with specific permissions.

## Table of Contents

- [Features](#features)
- [Technologies Used](#technologies-used)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [API Endpoints](#api-documentation)
  - [Authentication](#authentication)
  - [Blog Management](#blog-management)
  - [Admin Actions](#admin-actions)


## Features

### User Roles

#### Admin:
- Can delete any blog.
- Can block users by updating the `isBlocked` property.
- Cannot update blogs.

#### User:
- Can register and log in.
- Can create, update, and delete their own blogs.
- Cannot perform admin actions.

### Authentication & Authorization
- **Authentication:** Users must log in to perform write, update, and delete operations.
- **Authorization:** Role-based access control to secure endpoints.

### Public Blog API
- Provides blog data with options for **search**, **sort**, and **filter** functionalities.

---

## Technologies Used

- **TypeScript**
- **Node.js**
- **Express.js**
- **MongoDB** with Mongoose

---

## Getting Started

### Prerequisites

- Node.js installed (v14 or later)
- MongoDB database connection string

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/blog-platform-backend.git
   cd blog-platform-backend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Set up environment variables by creating a `.env` file:
   ```plaintext
   PORT=5000
   MONGO_URI=your_mongodb_connection_string
   JWT_SECRET=your_jwt_secret
   ```

4. Start the server:
   ```bash
   npm start
   ```

5. Access the API at `http://localhost:5000`.

---

## API Documentation

### Authentication

#### 1. Register User
**POST** `/api/auth/register`

Request Body:
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securepassword"
}
```
Response:
```json
{
  "success": true,
  "message": "User registered successfully",
  "statusCode": 201,
  "data": {
    "_id": "string",
    "name": "string",
    "email": "string"
  }
}
```

#### 2. Login User
**POST** `/api/auth/login`

Request Body:
```json
{
  "email": "john@example.com",
  "password": "securepassword"
}
```
Response:
```json
{
  "success": true,
  "message": "Login successful",
  "statusCode": 200,
  "data": {
    "token": "string"
  }
}
```

---

### Blog Management

#### 1. Create Blog
**POST** `/api/blogs`

Request Header:
```
Authorization: Bearer <token>
```
Request Body:
```json
{
  "title": "My First Blog",
  "content": "This is the content of my blog."
}
```
Response:
```json
{
  "success": true,
  "message": "Blog created successfully",
  "statusCode": 201,
  "data": {
    "_id": "string",
    "title": "string",
    "content": "string",
    "author": { "details" }
  }
}
```

#### 2. Update Blog
**PATCH** `/api/blogs/:id`

Request Header:
```
Authorization: Bearer <token>
```
Request Body:
```json
{
  "title": "Updated Blog Title",
  "content": "Updated content."
}
```
Response:
```json
{
  "success": true,
  "message": "Blog updated successfully",
  "statusCode": 200,
  "data": {
    "_id": "string",
    "title": "string",
    "content": "string",
    "author": { "details" }
  }
}
```

#### 3. Delete Blog
**DELETE** `/api/blogs/:id`

Request Header:
```
Authorization: Bearer <token>
```
Response:
```json
{
  "success": true,
  "message": "Blog deleted successfully",
  "statusCode": 200
}
```

#### 4. Get All Blogs (Public)
**GET** `/api/blogs`

Query Parameters:
- `search`: Search blogs by title or content 
- `sortBy`: Sort blogs by fields 
- `sortOrder`: Define sorting order
- `filter`: Filter blogs by author ID 

Response:
```json
{
  "success": true,
  "message": "Blogs fetched successfully",
  "statusCode": 200,
  "data": [
    {
      "_id": "string",
      "title": "string",
      "content": "string",
      "author": { "details" }
    }
  ]
}
```

---

### Admin Actions

#### 1. Block User
**PATCH** `/api/admin/users/:userId/block`

Request Header:
```
Authorization: Bearer <admin_token>
```
Response:
```json
{
  "success": true,
  "message": "User blocked successfully",
  "statusCode": 200
}
```

#### 2. Delete Blog
**DELETE** `/api/admin/blogs/:id`

Request Header:
```
Authorization: Bearer <admin_token>
```
Response:
```json
{
  "success": true,
  "message": "Blog deleted successfully",
  "statusCode": 200
}
```

---




