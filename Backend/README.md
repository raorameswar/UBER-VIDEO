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

