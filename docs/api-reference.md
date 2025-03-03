# Devity API Reference

Welcome to the **Devity API Reference**. This document outlines the core API endpoints for managing UI specs, retrieving configurations, and interacting with the Devity Backend.

## Base URL
The Devity API is served at:
```
http://localhost:8000/api/v1
```
Replace `localhost` with the production server when deployed.

## Authentication
All API requests must be authenticated using an API key or OAuth tokens. Include the token in the `Authorization` header:
```sh
Authorization: Bearer YOUR_ACCESS_TOKEN
```

## Endpoints

### 1. UI Spec Management
#### Create a New Spec
```http
POST /specs
```
**Request Body:**
```json
{
  "name": "My Spec",
  "description": "A sample UI spec",
  "version": "1.0.0",
  "components": []
}
```
**Response:**
```json
{
  "id": "123456",
  "status": "created"
}
```

#### Get a Spec by ID
```http
GET /specs/{spec_id}
```
**Response:**
```json
{
  "id": "123456",
  "name": "My Spec",
  "components": [...]
}
```

#### Update a Spec
```http
PUT /specs/{spec_id}
```
**Request Body:** *(Partial updates allowed)*
```json
{
  "name": "Updated Spec Name"
}
```
**Response:**
```json
{
  "status": "updated"
}
```

#### Delete a Spec
```http
DELETE /specs/{spec_id}
```
**Response:**
```json
{
  "status": "deleted"
}
```

### 2. Publishing Specs
#### Publish a Spec to CDN
```http
POST /specs/{spec_id}/publish
```
**Response:**
```json
{
  "status": "published",
  "cdn_url": "https://cdn.devity.com/specs/123456.json"
}
```

### 3. Fetching UI Configuration
#### Get All Published Specs
```http
GET /specs/published
```
**Response:**
```json
[
  {
    "id": "123456",
    "name": "My Spec",
    "cdn_url": "https://cdn.devity.com/specs/123456.json"
  }
]
```

### 4. User Authentication
#### User Login
```http
POST /auth/login
```
**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "securepassword"
}
```
**Response:**
```json
{
  "access_token": "your.jwt.token",
  "token_type": "bearer"
}
```

#### Get Current User Info
```http
GET /auth/me
```
**Response:**
```json
{
  "id": "user_123",
  "email": "user@example.com",
  "role": "admin"
}
```

## Error Handling
Devity API returns standard HTTP status codes:
- `200 OK` – Request successful
- `201 Created` – Resource successfully created
- `400 Bad Request` – Invalid request data
- `401 Unauthorized` – Authentication failed
- `404 Not Found` – Resource does not exist
- `500 Internal Server Error` – Server error

## Webhooks
Devity supports webhooks for real-time notifications on spec updates and publishing events. Configure webhooks via `POST /webhooks`.

For further details, refer to the [Devity Docs](https://github.com/your-org/devity_docs).

