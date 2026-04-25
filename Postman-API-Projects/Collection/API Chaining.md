# Test API Chaining Documentation

## 📌 Overview
This API collection demonstrates API chaining where responses from one request are used in subsequent requests.

---

## 🔹 POST - Create Resource

**Endpoint:**
```
POST /PostRequest
```

### Description
Creates a new resource and returns details including ID.

### Request Body
```json
{
  "name": "sample",
  "job": "tester"
}
```

### Response
```json
{
  "name": "sample",
  "job": "tester",
  "id": "123",
  "createdAt": "2026-03-21T17:00:00.000Z"
}
```

---

## 🔹 GET - Retrieve Resource

**Endpoint:**
```
GET /get/{id}
```

### Description
Fetches resource using ID from previous request.

### Path Parameter

| Parameter | Type   | Description        |
|----------|--------|--------------------|
| id       | string | Resource ID        |

### Response
```json
{
  "id": "123",
  "name": "sample",
  "job": "tester"
}
```

---

## 🔹 PUT - Update Resource

**Endpoint:**
```
PUT /put/{id}
```

### Description
Updates existing resource using ID.

### Request Body
```json
{
  "name": "updated name",
  "job": "updated job"
}
```

### Response
```json
{
  "name": "updated name",
  "job": "updated job",
  "updatedAt": "2026-03-21T17:10:00.000Z"
}
```

---

## 🔹 PATCH - Partial Update

**Endpoint:**
```
PATCH /patch/{id}
```

### Description
Partially updates resource fields.

### Request Body
```json
{
  "job": "partially updated"
}
```

### Response
```json
{
  "job": "partially updated",
  "updatedAt": "2026-03-21T17:15:00.000Z"
}
```

---

## 🔹 DELETE - Remove Resource

**Endpoint:**
```
DELETE /delete/{id}
```

### Description
Deletes the resource using ID.

### Response
```
204 No Content
```

---

## 🔄 API Chaining Flow

1. Create resource using **POST**
2. Extract `id` from response
3. Use `id` in:
   - GET
   - PUT
   - PATCH
   - DELETE

---

## 🛠 Tools Used

- Postman
- REST API
- JSON

---

## 📌 Notes

- Ensure correct environment variables are set
- Handle dynamic IDs using Postman scripts
- Validate responses using test scripts

---
