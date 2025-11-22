# test_go

A simple Go backend API server with RESTful endpoints for user management.

## Features

- RESTful API endpoints for CRUD operations
- JSON request/response handling
- In-memory data storage
- Thread-safe operations with mutex locks
- Proper error handling and HTTP status codes

## Prerequisites

- Go 1.24.10 or higher

## Installation

1. Clone the repository:
```bash
git clone https://github.com/fshrr/test_go.git
cd test_go
```

2. Install dependencies:
```bash
go mod download
```

3. Build the application:
```bash
go build -v .
```

## Running the Server

Start the server:
```bash
./test_go
```

Or run directly with Go:
```bash
go run main.go
```

The server will start on port 8080.

## API Endpoints

### Health Check

**GET** `/health`

Returns the health status of the server.

**Example:**
```bash
curl http://localhost:8080/health
```

**Response:**
```json
{
  "success": true,
  "message": "Server is running",
  "data": {
    "status": "healthy"
  }
}
```

### Get All Users

**GET** `/api/users`

Returns a list of all users.

**Example:**
```bash
curl http://localhost:8080/api/users
```

**Response:**
```json
{
  "success": true,
  "data": [
    {
      "id": 1,
      "name": "John Doe",
      "email": "john@example.com"
    },
    {
      "id": 2,
      "name": "Jane Smith",
      "email": "jane@example.com"
    }
  ]
}
```

### Get User by ID

**GET** `/api/users/{id}`

Returns a specific user by ID.

**Example:**
```bash
curl http://localhost:8080/api/users/1
```

**Response:**
```json
{
  "success": true,
  "data": {
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com"
  }
}
```

### Create User

**POST** `/api/users`

Creates a new user.

**Request Body:**
```json
{
  "name": "Alice Johnson",
  "email": "alice@example.com"
}
```

**Example:**
```bash
curl -X POST http://localhost:8080/api/users \
  -H "Content-Type: application/json" \
  -d '{"name":"Alice Johnson","email":"alice@example.com"}'
```

**Response:**
```json
{
  "success": true,
  "message": "User created successfully",
  "data": {
    "id": 3,
    "name": "Alice Johnson",
    "email": "alice@example.com"
  }
}
```

### Update User

**PUT** `/api/users/{id}`

Updates an existing user.

**Request Body:**
```json
{
  "name": "Alice Williams",
  "email": "alice.w@example.com"
}
```

**Example:**
```bash
curl -X PUT http://localhost:8080/api/users/3 \
  -H "Content-Type: application/json" \
  -d '{"name":"Alice Williams","email":"alice.w@example.com"}'
```

**Response:**
```json
{
  "success": true,
  "message": "User updated successfully",
  "data": {
    "id": 3,
    "name": "Alice Williams",
    "email": "alice.w@example.com"
  }
}
```

### Delete User

**DELETE** `/api/users/{id}`

Deletes a user by ID.

**Example:**
```bash
curl -X DELETE http://localhost:8080/api/users/3
```

**Response:**
```json
{
  "success": true,
  "message": "User with ID 3 deleted successfully"
}
```

## Error Handling

The API returns appropriate HTTP status codes and error messages:

- `200 OK` - Successful GET, PUT, DELETE operations
- `201 Created` - Successful POST operation
- `400 Bad Request` - Invalid request data
- `404 Not Found` - Resource not found

**Example Error Response:**
```json
{
  "success": false,
  "message": "User not found"
}
```

## Project Structure

```
test_go/
├── main.go        # Main application with API endpoints
├── go.mod         # Go module file
├── go.sum         # Go dependencies checksum
└── README.md      # This file
```

## Dependencies

- [Gorilla Mux](https://github.com/gorilla/mux) v1.8.1 - HTTP router and URL matcher

## License

This project is open source and available under the MIT License.