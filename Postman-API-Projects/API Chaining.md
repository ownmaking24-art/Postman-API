# Test API Chaining Documentation

## 📌 Overview
This API collection demonstrates API chaining where responses from one request are used in subsequent requests.

Host: https://gorest.co.in
---

## 🔹 POST - Create Resource

**Endpoint:**
```
POST /public/v2/users
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
## ✅ Test Assertions

### Fetch response data and stores ID in "Chaining_ID" variable
Pre-Request
```javascript
var random= Math.random().toString(32).substring(2);

var newUser = "Sham"+random;
var email_="sham"+random+"@gmail.com";

pm.environment.set("User_email",email_);
pm.environment.set("User_name",newUser);
```
Post-Response
```javascript
 const jsonData= pm.response.json();
 pm.environment.set("Chaining_ID",jsonData.id);
```

---
## 🔹 GET - Retrieve Resource

**Endpoint:**
```
GET /public/v2/users/{{Chaining_ID}}
```

### Description
Fetches resource using ID from previous request.

### Path Parameter

| Parameter | Type   | Description        |
|----------|--------|--------------------|
| Chaining_ID       | string | Resource ID        |

### Response
```json
{
  "id": "123",
  "name": "sample",
  "job": "tester"
}
```


## ✅ Test Assertions

### Checks whether the Provided ID and the Response ID are same.
Post-Response
```javascript
var responseBody = pm.response.json();
pm.test("Posted data and retrived data are the same", ()=>{
    pm.expect(responseBody.id).to.eql(pm.environment.get("Chaining_ID"));
    
});
```

```

## 🔹 PUT - Update Resource

**Endpoint:**
```
PUT /public/v2/users/{{Chaining_ID}}
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
## ✅ Test Assertions

### Generates random string and appends it in the variable. 
Pre-Request
```javascript
console.log(pm.environment.get("Chaining_ID"));
var random= Math.random().toString(32).substring(2);
var newUser = "Sham"+random;
var email_="sham"+random+"@gmail.com";

pm.environment.set("User_email",email_);
pm.environment.set("User_name",newUser);
```
### Unset the User_email and User_name environment variable
Post-Response
```javascript
pm.environment.unset("User_email");
pm.environment.unset("User_name");
```

---

## 🔹 DELETE - Remove Resource

**Endpoint:**
```
DELETE /public/v2/users/{{Chaining_ID}}
```

### Description
Deletes the resource using ID.

### Response
```
204 No Content
```
## ✅ Test Assertions

### Unset the Environment Variable
Post-Response
```javascript
pm.environment.unset("Chaining_ID");
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
