# Library API Documentation

## Overview

The Library API allows users to manage books, authors, and accounts with various endpoints for registration, authentication, and data manipulation. Below are the details of the available API endpoints.

---

## Endpoints

### User Management

#### 1. Register a New User
- **Method:** `POST`
- **Endpoint:** `/user/register`
- **Description:** Registers a new user with a unique username.
- **Request Headers:** 
  - `Content-Type: application/json`
- **Request Body Parameters:** 
  - `username` (string): Desired username.
  - `password` (string): Account password.
- **Responses:** 
  - **200 OK:** 
    ```json
    { "status": "success", "data": null }
    ```
  - **200 OK (Username Taken):** 
    ```json
    { "status": "fail", "data": { "title": "Username already exists" } }
    ```
  - **500 Internal Server Error:** 
    ```json
    { "status": "fail", "data": { "title": "<error message>" } }
    ```

#### 2. Authenticate User
- **Method:** `POST`
- **Endpoint:** `/user/auth`
- **Description:** Authenticates a user and generates a token upon success.
- **Request Headers:** 
  - `Content-Type: application/json`
- **Request Body Parameters:** 
  - `username` (string): User's username.
  - `password` (string): User's password.
- **Responses:** 
  - **200 OK:** 
    ```json
    { "status": "success", "token": "<token>", "data": null }
    ```
  - **200 OK (Invalid Credentials):** 
    ```json
    { "status": "fail", "data": { "title": "Incorrect username or password" } }
    ```
  - **500 Internal Server Error:** 
    ```json
    { "status": "fail", "data": { "title": "<error message>" } }
    ```

#### 3. Show All Users
- **Method:** `GET`
- **Endpoint:** `/user/show`
- **Description:** Lists all registered users. Requires authorization.
- **Request Headers:** 
  - `Authorization: Bearer <token>`
- **Responses:** 
  - **200 OK:** 
    ```json
    { "status": "success", "data": [ { "user_id": 1, "username": "user1" }, ... ] }
    ```
  - **401 Unauthorized:** 
    ```json
    { "status": "fail", "data": { "title": "Invalid or missing token" } }
    ```
  - **500 Internal Server Error:** 
    ```json
    { "status": "fail", "data": { "title": "<error message>" } }
    ```

#### 4. Update User
- **Method:** `PUT`
- **Endpoint:** `/user/update`
- **Description:** Updates user details. Requires authorization.
- **Request Headers:** 
  - `Authorization: Bearer <token>`
  - `Content-Type: application/json`
- **Request Body Parameters:** 
  - `username` (string): New username.
  - `password` (string): New password.
- **Responses:** 
  - **200 OK:** 
    ```json
    { "status": "success", "data": null }
    ```
  - **400 Bad Request:** 
    ```json
    { "status": "fail", "data": { "title": "Invalid input data" } }
    ```
  - **401 Unauthorized:** 
    ```json
    { "status": "fail", "data": { "title": "Invalid or missing token" } }
    ```
  - **500 Internal Server Error:** 
    ```json
    { "status": "fail", "data": { "title": "<error message>" } }
    ```

#### 5. Delete User
- **Method:** `DELETE`
- **Endpoint:** `/user/delete`
- **Description:** Deletes a user account. Requires authorization.
- **Request Headers:** 
  - `Authorization: Bearer <token>`
  - `Content-Type: application/json`
- **Request Body Parameters:** 
  - `user_id` (integer): ID of the user to delete.
- **Responses:** 
  - **200 OK:** 
    ```json
    { "status": "success", "data": null }
    ```
  - **400 Bad Request:** 
    ```json
    { "status": "fail", "data": { "title": "Invalid input data" } }
    ```
  - **401 Unauthorized:** 
    ```json
    { "status": "fail", "data": { "title": "Invalid or missing token" } }
    ```
  - **500 Internal Server Error:** 
    ```json
    { "status": "fail", "data": { "title": "<error message>" } }
    ```

---

### Author Management

#### 1. Register a New Author
- **Method:** `POST`
- **Endpoint:** `/author/register`
- **Description:** Registers a new author with a unique name.
- **Request Headers:** 
  - `Authorization: Bearer <token>`
  - `Content-Type: application/json`
- **Request Body Parameters:** 
  - `name` (string): Name of the author.
- **Responses:** 
  - **200 OK:** 
    ```json
    { "status": "success", "data": null }
    ```
  - **400 Bad Request (Name Missing):** 
    ```json
    { "status": "fail", "data": { "title": "Author name missing" } }
    ```
  - **400 Bad Request (Name Exists):** 
    ```json
    { "status": "fail", "data": { "title": "Author name already exists" } }
    ```
  - **401 Unauthorized:** 
    ```json
    { "status": "fail", "data": { "title": "Invalid or missing token" } }
    ```
  - **500 Internal Server Error:** 
    ```json
    { "status": "fail", "data": { "title": "<error message>" } }
    ```

#### 2. Show All Authors
- **Method:** `GET`
- **Endpoint:** `/author/show`
- **Description:** Fetches a list of all authors in the library database.
- **Request Headers:** 
  - `Authorization: Bearer <token>`
- **Responses:** 
  - **200 OK:** 
    ```json
    { "status": "success", "data": [ { "author_id": 1, "name": "Author Name" }, ... ] }
    ```
  - **401 Unauthorized:** 
    ```json
    { "status": "fail", "data": { "title": "Invalid or missing token" } }
    ```
  - **404 Not Found (No Authors Found):** 
    ```json
    { "status": "fail", "message": "No authors found" }
    ```
  - **500 Internal Server Error:** 
    ```json
    { "status": "fail", "message": "<error message>" }
    ```

#### 3. Update Author
- **Method:** `PUT`
- **Endpoint:** `/author/update`
- **Description:** Updates the name of an existing author.
- **Request Headers:** 
  - `Authorization: Bearer <token>`
  - `Content-Type: application/json`
- **Request Body Parameters:** 
  - `author_id` (integer): ID of the author to update.
  - `name` (string): New name for the author.
- **Responses:** 
  - **200 OK:** 
    ```json
    { "status": "success", "data": null }
    ```
  - **400 Bad Request (Author ID or Name Missing):** 
    ```json
    { "status": "fail", "data": { "title": "Author ID or name missing" } }
    ```
  - **401 Unauthorized:** 
    ```json
    { "status": "fail", "data": { "title": "Invalid or missing token" } }
    ```
  - **404 Not Found (Author Not Found):** 
    ```json
    { "status": "fail", "data": { "title": "Author not found" } }
    ```
  - **500 Internal Server Error:** 
    ```json
    { "status": "fail", "data": { "title": "<error message>" } }
    ```

#### 4. Delete Author
- **Method:** `DELETE`
- **Endpoint:** `/author/delete`
- **Description:** Deletes an author by ID.
- **Request Headers:** 
  - `Authorization: Bearer <token>`
  - `Content-Type: application/json`
- **Request Body Parameters:** 
  - `author_id` (integer): ID of the author to delete.
- **Responses:** 
  - **200 OK:** 
    ```json
    { "status": "success", "data": null }
    ```
  - **400 Bad Request (Author ID Missing):** 
    ```json
    { "status": "fail", "data": { "title": "Author ID missing" } }
    ```
  - **401 Unauthorized:** 
    ```json
    { "status": "fail", "data": { "title": "Invalid or missing token" } }
    ```
  - **404 Not Found (Author Not Found):** 
    ```json
    { "status": "fail", "data": { "title": "Author not found" } }
    ```
  - **500 Internal Server Error:** 
    ```json
    { "status": "fail", "data": { "title": "<error message>" } }
    ```

---

## Developed By:
- Mark Lydrion RIvera 4-B
