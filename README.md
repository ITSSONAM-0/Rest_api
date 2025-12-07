
# 📘 REST API – Complete Theory for MERN Stack (Placement Ready)

## 🔹 What is REST API?

REST API (Representational State Transfer) is a way for your frontend (React) to communicate with your backend (Node.js + Express) using simple HTTP requests.

React → API request → Express/Node → MongoDB → Response back to React.

---

## 🔹 REST Principles

Client–Server → React (client) and Express (server) work independently.
---

Stateless → Server does not store session data.

Resource-Based → /users, /products, /posts.

Uniform Interface → Same consistent structure.

Cacheable → Responses can be cached.

Layered Architecture → Middlewares, routers, controllers, database.

---

###🔹 HTTP Methods in REST
Method	Description
GET	Read data
POST	Create new data
PUT	Update full data
PATCH	Update partial data
DELETE	Delete data
---

## 🔹 REST API URL Design (Best Practices)

✔ Use nouns, not verbs
✔ Use plural names
✔ Keep URLs clean

❌ Bad	✅ Good
/getUsers	/users
/create-post	/posts
/deleteUser/55	/users/55

---
### 🔹 Important HTTP Status Codes
✔ Success
Code	Meaning
200 OK	Request successful
201 Created	New data created
204 No Content	Successful but no response body
---

### ❗ Errors
Code	Meaning
400 Bad Request	Wrong API input
401 Unauthorized	Token required
403 Forbidden	Access denied
404 Not Found	Resource not found
500 Internal Server Error	Server crashed

## 🔹 JSON – Standard Data Format
```{
  "name": "Sonam",
  "email": "sonam@example.com"
}```
```


### 🔹 CRUD Operations Example (Express + MongoDB)
```1️⃣ Create (POST /users)
router.post("/users", async (req, res) => {
  const user = await User.create(req.body);
  res.status(201).json(user);
});

```
```2️⃣ Read (GET /users)
router.get("/users", async (req, res) => {
  const users = await User.find();
  res.status(200).json(users);
});
```

```3️⃣ Update (PUT /users/:id)
router.put("/users/:id", async (req, res) => {
  const updated = await User.findByIdAndUpdate(req.params.id, req.body, { new: true });
  res.status(200).json(updated);
});
```

```4️⃣ Delete (DELETE /users/:id)
router.delete("/users/:id", async (req, res) => {
  await User.findByIdAndDelete(req.params.id);
  res.status(204).send();
});
```
# 🔹 Middlewares (Very Important)

Middleware → code that runs before the main API handler.

Examples:

express.json()

JWT Authentication

Error handling

Logging

app.use(express.json());

# 🔹 Authentication Using JWT
Client → sends token
Server → verifies token

Example header:

Authorization: Bearer <token>


# Express JWT middleware:

```import jwt from "jsonwebtoken";

function auth(req, res, next) {
  const token = req.headers.authorization?.split(" ")[1];
  if (!token) return res.status(401).json({ message: "Unauthorized" });

  jwt.verify(token, "secretkey", (err, user) => {
    if (err) return res.status(403).json({ message: "Invalid token" });
    req.user = user;
    next();
  });
}
```
# 🔹 Pagination in REST

Used when returning large lists.

Example:

GET /products?page=1&limit=10


# Express:

```const page = req.query.page || 1;
const limit = req.query.limit || 10;

const products = await Product.find()
  .skip((page - 1) * limit)
  .limit(limit);
```
# 🔹 Idempotency (Interview Favorite)
Method	Idempotent?
GET	✔ Yes
PUT	✔ Yes
DELETE	✔ Yes
POST	❌ No

POST creates new record each time → not idempotent.

# 🔹 REST vs GraphQL (MERN Interview Question)
REST	GraphQL
Multiple endpoints	Single endpoint
May over-fetch	Fetch only required data
Easy	Complex
Great for MERN	Also used with MERN
# 🔹 Suggested MERN Backend Folder Structure
backend/
 ├── controllers/
 ├── models/
 ├── routes/
 ├── middleware/
 ├── config/
 ├── server.js
 └── package.json

# ✔ Final Interview Summary

REST API is a stateless, resource-based architecture that uses HTTP methods
(GET, POST, PUT, DELETE) to perform CRUD operations on resources like /users
using JSON. In MERN, React acts as the client, Express + Node.js as the server,
and MongoDB as the database. REST APIs return proper status codes and follow clean URL design.
