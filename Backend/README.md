# `/users/register` Endpoint Documentation

## **Endpoint Description:**
The `/users/register` endpoint allows users to register by providing their full name, email, and password. The server hashes the password and stores the user details in the database.

---

## **HTTP Method:**
POST

---

## **Request URL:**
```
http://localhost:4000/users/register
```

---

## **Request Body:**
The endpoint expects a JSON object with the following fields:

```json
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.doe@example.com",
  "password": "your_secure_password"
}
```

### **Field Descriptions:**
- **fullname.firstname** (String, required): Minimum 3 characters.
- **fullname.lastname** (String, optional): Minimum 3 characters.
- **email** (String, required): Must be unique and at least 5 characters long.
- **password** (String, required): Must be provided.

---

## **Response Codes and Descriptions:**

- **201 Created:** User registered successfully.
  ```json
  {
    "message": "User registered successfully!",
    "user": {
      "id": "60d0fe4f5311236168a109ca",
      "fullname": { "firstname": "John", "lastname": "Doe" },
      "email": "john.doe@example.com"
    }
  }
  ```

- **400 Bad Request:** Validation error (e.g., missing fields, invalid input).
  ```json
  { "error": "First name must be at least 3 characters long" }
  ```

- **409 Conflict:** Email already exists.
  ```json
  { "error": "Email already exists" }
  ```

- **500 Internal Server Error:** Unexpected server error.
  ```json
  { "error": "Something went wrong! Please try again later." }
  ```

---

## **Example Usage in Postman:**
- **Method:** POST
- **URL:** `http://localhost:4000/users/register`
- **Headers:**
  - Content-Type: `application/json`
- **Body (raw JSON):**
  ```json
  {
    "fullname": {
      "firstname": "Jane",
      "lastname": "Smith"
    },
    "email": "jane.smith@example.com",
    "password": "securepassword123"
  }
  ```

---

## **Notes:**
- Ensure MongoDB is running and `.env` file contains the necessary `JWT_SECRET`.
- Make sure the backend server is started using `nodemon server.js` or `node server.js`.
- Use a tool like Postman or cURL to test the endpoint.

---

# User Registration and Login Endpoint Documentation

## Endpoint: `/users/register`

### **Description:**
This endpoint allows users to register by providing their full name, email, and password. The provided password will be securely hashed before saving in the database.

---

### **Method:** `POST`

### **Request Body:**
The request body should be in JSON format:

```json
{
  "fullname": {
    "firstname": "Ramesh",
    "lastname": "Verma"
  },
  "email": "ramesh@gmail.com",
  "password": "password123"
}
```

**Required Fields:**
- `fullname.firstname` (String, min 3 characters) – **Required**
- `fullname.lastname` (String, min 3 characters) – Optional
- `email` (String, min 5 characters) – **Required**, must be unique
- `password` (String) – **Required**

---

### **Response Codes:**

- **201 Created:**
  ```json
  {
    "message": "User registered successfully",
    "user": {
      "_id": "unique_user_id",
      "email": "ramesh@gmail.com"
    }
  }
  ```

- **400 Bad Request:** Missing required fields or validation errors.
- **409 Conflict:** Email already exists.
- **500 Internal Server Error:** Server-side issue during registration.

---

## Endpoint: `/users/login`

### **Description:**
This endpoint allows users to log in by providing their email and password. On successful authentication, a JWT token is generated and returned.

---

### **Method:** `POST`

### **Request Body:**
```json
{
  "email": "ramesh@gmail.com",
  "password": "password123"
}
```

**Required Fields:**
- `email` (String) – **Required**
- `password` (String) – **Required**

---

### **Response Codes:**

- **200 OK:**
  ```json
  {
    "message": "Login successful",
    "token": "jwt_token_here"
  }
  ```

- **400 Bad Request:** Missing required fields or invalid credentials.
- **401 Unauthorized:** Incorrect email or password.
- **500 Internal Server Error:** Server-side issue during login.

---

### **Dependencies:**
- `express`
- `mongoose`
- `bcrypt`
- `jsonwebtoken`
- `express-validator`

