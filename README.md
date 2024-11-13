# THE LIBRARY

Welcome to the Library API documentation. This API allows you to register, authenticate, update, delete, and view user accounts. All sensitive actions are protected by JWT authentication.

## Base URL

### http://localhost:8000

## Endpoints

### 1. Register User

**POST** `/user/register`

***Payload:***
```json
{
  "username": "string",
  "password": "string"
}


 #### Response:

Success (200):
{
  "status": "success",
  "data": null
}

Fail (400):
{
  "status": "fail",
  "data": "Username already exists"
}

Fail (500):
{
  "status": "fail",
  "data": {
    "title": "Error message"
  }
}

### 2. Authenticate User (Login)

**POST** /user/auth

 Authenticates a user by verifying their username and password, and returns a JWT token.

Payload: 
{
  "username": "string",
  "password": "string"
}


### Response: 

Success (200):
{
  "status": "success",
  "token": "JWT_TOKEN",
  "data": null
}

Fail(400):
{
  "status": "fail",
  "data": {
    "title": "Invalid input data"
  }
}


Fail(404):

{
  "status": "fail",
  "data": {
    "title": "Incorrect username"
  }
}

Faile(401):
{
  "status": "fail",
  "data": {
    "title": "Incorrect password"
  }
}


### #. Update User Account

PUT /user/update

Allows a user to update their username and password.

Payload:
{
  "new_username": "string",
  "new_password": "string"
}

Response:
Success (200):

{
  "status": "success",
  "token": "JWT_TOKEN",
  "data": null
}

Fail (400):
{
  "status": "fail",
  "data": "Invalid input data"
}

Fail (404):
{
  "status": "fail",
  "data": "User not found"
}

Fail (500):
{
  "status": "fail",
  "data": {
    "title": "Error message"
  }
}

4. Delete User Account
DELETE /user/delete

Deletes a user account by providing the user_id.

Payload:
{
  "user_id": "integer"
}

Response:
Success (200):
{
  "status": "success",
  "data": "User account deleted"
}

Fail (400):
{
  "status": "fail",
  "data": "User ID not provided"
}

Fail (404):
{
  "status": "fail",
  "data": "User with the given user_id not found"
}

Fail (500):
{
  "status": "fail",
  "data": {
    "title": "Error message"
  }
}

##5. Show Users

GET /user/show

Displays a list of all users or a specific user by user_id.

Query Parameters:

user_id: (optional) Filter by user ID.

Response:
Success (200):

If a specific user is requested:
{
  "status": "success",
  "token": "JWT_TOKEN",
  "data": {
    "user_id": "integer",
    "username": "string"
  }
}

If all users are requested:
{
  "status": "success",
  "token": "JWT_TOKEN",
  "data": [
    {
      "user_id": "integer",
      "username": "string"
    },
    {
      "user_id": "integer",
      "username": "string"
    }
  ]
}
Fail (404):

json
Copy code
{
  "status": "fail",
  "data": "User not found"
}
Fail (500):
json
Copy code
{
  "status": "fail",
  "data": {
    "title": "Error message"
  }
}


Authentication
To access any endpoint except for user registration and authentication, you must include a JWT token in the Authorization header of your request:

Authorization: Bearer JWT_TOKEN