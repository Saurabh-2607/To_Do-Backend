# To-Do Application with User Authentication

This repository contains a simple To-Do application implemented using Express.js, MongoDB, and JWT authentication. Users can sign up, log in, and manage their tasks securely.

## Features
- **User Signup**: Create a new account with a name, email, and password.
- **User Signin**: Log in using email and password to receive a JWT token.
- **Authentication Middleware**: Secure routes using JWT-based authentication.
- **CRUD Operations on To-Dos**:
  - Create a new to-do.
  - Update an existing to-do.
  - Delete a to-do.
  - Retrieve all to-dos for the authenticated user.

## Prerequisites
- Node.js (v14 or higher)
- MongoDB instance (local or cloud-based, e.g., MongoDB Atlas)

## Environment Variables
Create a `.env` file in the root directory and add the following:
```env
DB_URL=<Your MongoDB Connection URL>
JWT_SECRET=<Your Secret Key for JWT>
PORT=3000
```

## Installation
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the server:
   ```bash
   node app.js
   ```

4. The application will run on `http://localhost:3000`.

## API Endpoints

### User Authentication

#### Signup
- **POST** `/signup`
- **Request Body**:
  ```json
  {
    "name": "<user_name>",
    "email": "<user_email>",
    "password": "<user_password>"
  }
  ```
- **Response**:
  ```json
  {
    "message": "You are signed up"
  }
  ```

#### Signin
- **POST** `/signin`
- **Request Body**:
  ```json
  {
    "email": "<user_email>",
    "password": "<user_password>"
  }
  ```
- **Response**:
  ```json
  {
    "token": "<JWT Token>"
  }
  ```

### To-Do Management

#### Create a To-Do
- **POST** `/todo`
- **Headers**:
  ```json
  {
    "Authorization": "Bearer <JWT Token>"
  }
  ```
- **Request Body**:
  ```json
  {
    "title": "<todo_title>",
    "description": "<todo_description>",
    "done": false
  }
  ```
- **Response**:
  ```json
  {
    "todoId": "<created_todo_id>",
    "message": "Todo created"
  }
  ```

#### Update a To-Do
- **PUT** `/todo`
- **Headers**:
  ```json
  {
    "Authorization": "Bearer <JWT Token>"
  }
  ```
- **Request Body**:
  ```json
  {
    "todoId": "<todo_id>",
    "done": true
  }
  ```
- **Response**:
  ```json
  {
    "message": "Todo updated"
  }
  ```

#### Delete a To-Do
- **DELETE** `/todo`
- **Headers**:
  ```json
  {
    "Authorization": "Bearer <JWT Token>"
  }
  ```
- **Request Body**:
  ```json
  {
    "todoId": "<todo_id>"
  }
  ```
- **Response**:
  ```json
  {
    "message": "Todo deleted"
  }
  ```

#### Retrieve All To-Dos
- **GET** `/todo`
- **Headers**:
  ```json
  {
    "Authorization": "Bearer <JWT Token>"
  }
  ```
- **Response**:
  ```json
  {
    "todos": [
      {
        "_id": "<todo_id>",
        "userId": "<user_id>",
        "title": "<todo_title>",
        "description": "<todo_description>",
        "done": false
      }
    ]
  }
  ```

## Dependencies
- `express`
- `mongoose`
- `bcrypt`
- `jsonwebtoken`
- `dotenv`

Install all dependencies using:
```bash
npm install express mongoose bcrypt jsonwebtoken dotenv
```

## Security Note
Ensure that sensitive information (e.g., `JWT_SECRET`, `DB_URL`) is stored securely and not hardcoded in your application.

## License
This project is licensed under the MIT License.
