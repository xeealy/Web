# API Documentation

## Base URL

```
http://localhost:3000/api/v1
```

## Authentication

All endpoints (except /auth) require JWT token in Authorization header:

```
Authorization: Bearer {token}
```

## Error Responses

All errors follow this format:

```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Error description",
    "details": {}
  }
}
```

## Endpoints

### Authentication

#### Register

```
POST /auth/register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "securepassword123",
  "first_name": "John",
  "last_name": "Doe"
}

Response: 201
{
  "success": true,
  "data": {
    "id": 1,
    "email": "user@example.com",
    "first_name": "John",
    "last_name": "Doe",
    "role": "user"
  },
  "token": "eyJhbGc..."
}
```

#### Login

```
POST /auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "securepassword123"
}

Response: 200
{
  "success": true,
  "data": {
    "id": 1,
    "email": "user@example.com",
    "first_name": "John",
    "last_name": "Doe",
    "role": "user"
  },
  "token": "eyJhbGc..."
}
```

### Contacts

#### List Contacts

```
GET /contacts?page=1&limit=10&status=lead&search=john

Response: 200
{
  "success": true,
  "data": [
    {
      "id": 1,
      "first_name": "John",
      "last_name": "Doe",
      "email": "john@example.com",
      "phone": "+1234567890",
      "company": "Acme Corp",
      "job_title": "Sales Manager",
      "status": "lead",
      "source": "web",
      "owner_id": 1,
      "created_at": "2026-06-01T10:00:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 100,
    "pages": 10
  }
}
```

#### Create Contact

```
POST /contacts
Content-Type: application/json

{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@example.com",
  "phone": "+1234567890",
  "company": "Acme Corp",
  "job_title": "Sales Manager",
  "status": "lead",
  "source": "web"
}

Response: 201
{
  "success": true,
  "data": {
    "id": 1,
    "first_name": "John",
    "last_name": "Doe",
    "email": "john@example.com",
    "phone": "+1234567890",
    "company": "Acme Corp",
    "job_title": "Sales Manager",
    "status": "lead",
    "source": "web",
    "owner_id": 1,
    "created_at": "2026-06-01T10:00:00Z"
  }
}
```

#### Get Contact

```
GET /contacts/{id}

Response: 200
{
  "success": true,
  "data": { ... }
}
```

#### Update Contact

```
PUT /contacts/{id}
Content-Type: application/json

{
  "first_name": "Jane",
  "status": "customer"
}

Response: 200
{
  "success": true,
  "data": { ... }
}
```

#### Delete Contact

```
DELETE /contacts/{id}

Response: 204
```

### Opportunities

#### List Opportunities

```
GET /opportunities?page=1&limit=10&stage=prospecting

Response: 200
{
  "success": true,
  "data": [
    {
      "id": 1,
      "name": "Big Deal",
      "contact_id": 1,
      "amount": 50000,
      "stage": "prospecting",
      "probability": 30,
      "expected_close_date": "2026-07-01",
      "owner_id": 1,
      "created_at": "2026-06-01T10:00:00Z"
    }
  ],
  "pagination": { ... }
}
```

#### Create Opportunity

```
POST /opportunities
Content-Type: application/json

{
  "name": "Big Deal",
  "contact_id": 1,
  "amount": 50000,
  "stage": "prospecting",
  "probability": 30,
  "expected_close_date": "2026-07-01"
}

Response: 201
{
  "success": true,
  "data": { ... }
}
```

### Activities

#### List Activities

```
GET /activities?type=meeting&status=pending

Response: 200
{
  "success": true,
  "data": [
    {
      "id": 1,
      "type": "meeting",
      "title": "Client Meeting",
      "description": "Discuss Q3 strategy",
      "contact_id": 1,
      "opportunity_id": 1,
      "owner_id": 1,
      "due_date": "2026-06-10",
      "status": "pending",
      "priority": "high",
      "created_at": "2026-06-01T10:00:00Z"
    }
  ],
  "pagination": { ... }
}
```

#### Create Activity

```
POST /activities
Content-Type: application/json

{
  "type": "meeting",
  "title": "Client Meeting",
  "description": "Discuss Q3 strategy",
  "contact_id": 1,
  "opportunity_id": 1,
  "due_date": "2026-06-10",
  "priority": "high"
}

Response: 201
{
  "success": true,
  "data": { ... }
}
```

### Reports

#### Dashboard

```
GET /reports/dashboard

Response: 200
{
  "success": true,
  "data": {
    "total_contacts": 150,
    "total_opportunities": 45,
    "total_revenue": 1250000,
    "open_activities": 23,
    "conversion_rate": 30,
    "average_deal_size": 27777
  }
}
```

## Status Codes

- `200` - OK
- `201` - Created
- `204` - No Content
- `400` - Bad Request
- `401` - Unauthorized
- `403` - Forbidden
- `404` - Not Found
- `500` - Internal Server Error
