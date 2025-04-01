# User Registration Endpoint Documentation

## Endpoint
`POST /users/register`

## Description
This endpoint is used to register a new user in the system. It accepts user details, validates the input, and creates a new user in the database.

## Request Body
The request body must be in JSON format and include the following fields:

- `fullname.firstname` (string, required): The first name of the user. Must be at least 3 characters long.
- `fullname.lastname` (string, optional): The last name of the user. Must be at least 3 characters long if provided.
- `email` (string, required): The email address of the user. Must be a valid email format.
- `password` (string, required): The password for the user. Must be at least 6 characters long.

### Example Request Body
```json
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "johndoe@example.com",
  "password": "securepassword"
}
```

## Response

### Success Response
- **Status Code**: `201 Created`
- **Body**:
  ```json
  {
    "token": "jwt-token-here",
    "user": {
      "_id": "user-id",
      "fullname": {
        "firstname": "John",
        "lastname": "Doe"
      },
      "email": "johndoe@example.com",
      "date": "2023-01-01T00:00:00.000Z"
    }
  }
  ```

### Error Responses
- **Status Code**: `400 Bad Request`
  - **Description**: Validation errors in the input data.
  - **Example**:
    ```json
    {
      "errors": [
        {
          "msg": "First name must be at least 3 characters long",
          "param": "fullname.firstname",
          "location": "body"
        }
      ]
    }
    ```

- **Status Code**: `500 Internal Server Error`
  - **Description**: Server error while processing the request.

## Notes
- The `token` in the response is a JWT token that can be used for authentication in subsequent requests.
- Ensure that all required fields are provided and meet the validation criteria to avoid errors.
