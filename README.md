```markdown
# THE LIBRARY

This is a REST API for user management in a library system, providing functionality for user registration, authentication, updating, deleting, and retrieving user information.

---

## API Endpoints

### 1. **User Registration**
   - **Endpoint**: `/user/register`
   - **Method**: `POST`
   - **Payload**:
     ```json
     {
       "username": "string",
       "password": "string"
     }
     ```
   - **Response**:
     - **Success**:
       ```json
       {
         "status": "success",
         "data": null
       }
       ```
     - **Failure**:
       ```json
       {
         "status": "fail",
         "data": "Username already exists"
       }
       ```

### 2. **User Authentication**
   - **Endpoint**: `/user/auth`
   - **Method**: `POST`
   - **Payload**:
     ```json
     {
       "username": "string",
       "password": "string"
     }
     ```
   - **Response**:
     - **Success**:
       ```json
       {
         "status": "success",
         "token": "JWT_TOKEN",
         "data": null
       }
       ```
     - **Failure**:
       - Incorrect username or password:
         ```json
         {
           "status": "fail",
           "data": { "title": "Incorrect username/password" }
         }
         ```

### 3. **Update User Account**
   - **Endpoint**: `/user/update`
   - **Method**: `PUT`
   - **Headers**:
     - `Authorization`: `Bearer JWT_TOKEN`
   - **Payload**:
     ```json
     {
       "new_username": "string",
       "new_password": "string"
     }
     ```
   - **Response**:
     - **Success**:
       ```json
       {
         "status": "success",
         "token": "NEW_JWT_TOKEN",
         "data": null
       }
       ```
     - **Failure**:
       - User not found or invalid input:
         ```json
         {
           "status": "fail",
           "data": "User not found"
         }
         ```

### 4. **Delete User Account**
   - **Endpoint**: `/user/delete`
   - **Method**: `DELETE`
   - **Headers**:
     - `Authorization`: `Bearer JWT_TOKEN`
   - **Payload**:
     ```json
     {
       "user_id": "integer"
     }
     ```
   - **Response**:
     - **Success**:
       ```json
       {
         "status": "success",
         "data": "User account deleted"
       }
       ```
     - **Failure**:
       - User ID not provided or user not found:
         ```json
         {
           "status": "fail",
           "data": "User ID not provided / User not found"
         }
         ```

### 5. **Display Users**
   - **Endpoint**: `/user/show`
   - **Method**: `GET`
   - **Headers**:
     - `Authorization`: `Bearer JWT_TOKEN`
   - **Query Parameters**:
     - `user_id` (optional): Show a specific user's details.
   - **Response**:
     - **Success**:
       ```json
       {
         "status": "success",
         "token": "NEW_JWT_TOKEN",
         "data": [
           {
             "user_id": "integer",
             "username": "string"
           }
         ]
       }
       ```
     - **Failure**:
       - User not found or no users in the system:
         ```json
         {
           "status": "fail",
           "data": "User not found / No users found"
         }
         ```

---

### Note:
- JWT token is required for endpoints that involve updating, deleting, or displaying user information.
- Tokens are rotated with each request, and previous tokens are invalidated.
```