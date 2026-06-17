# 🌐 HTTP & REST — Complete Course Notes
> Mohamed Salman | June 2026  
> Pre-requisite module before FastAPI curriculum

---

## Chapter 1 — The Mental Model

### What is HTTP?
HTTP (HyperText Transfer Protocol) is the **agreed language** that clients and servers use to communicate. It is a **stateless request-response protocol** — meaning every request is brand new, and the server has zero memory of you between requests.

```
You (Client)                        Server
    │                                  │
    │  ──── HTTP Request ──────────►   │   "Give me your homepage"
    │                                  │
    │  ◄─── HTTP Response ──────────   │   "Here it is"
    │                                  │
```

### Client vs Server

| Role | Who | Does what |
|---|---|---|
| **Client** | Browser, mobile app, Python script | Sends requests |
| **Server** | FastAPI, Django, Node.js app | Responds to requests |

> The server **never speaks first**. It only responds when asked.

### The Restaurant Analogy

```
Client   =  Customer
Server   =  Kitchen
HTTP     =  The menu & ordering system
Request  =  Placing an order
Response =  Food arriving at your table
```

### Key rule — Stateless
The server processes your request and **immediately forgets you exist**.  
This is why **JWT tokens** exist — to remind the server who you are on every single request.

---

## Chapter 2 — Anatomy of an HTTP Request

Every request has **4 parts:**

```
┌─────────────────────────────────────────┐
│  1. METHOD     → What do you want?      │
│  2. URL        → Where are you sending? │
│  3. HEADERS    → Meta info about you    │
│  4. BODY       → Data you're sending    │
└─────────────────────────────────────────┘
```

---

### Part 1 — HTTP Methods

| Method | Meaning | Example |
|---|---|---|
| `GET` | Fetch something | Load a restaurant list |
| `POST` | Create something | Place a new order |
| `PUT` | Replace something entirely | Update entire user profile |
| `PATCH` | Update part of something | Change only phone number |
| `DELETE` | Remove something | Delete an account |

> **Rule:** `GET` never has a body. You don't send data when you're only fetching.

---

### Part 2 — URL Structure

```
https://api.razorpay.com/v1/payments/pay_123?expand=card

  │         │                │    │      │         │
scheme     host            path  ver  resource  query param
```

- **Scheme** → `https` (secure HTTP)
- **Host** → the server's address
- **Path** → which resource you want
- **Query params** → optional filters (`?city=Chennai`)

---

### Part 3 — Headers

Key-value metadata attached to every request.

```
GET /v1/payments HTTP/1.1
Host: api.razorpay.com
Authorization: Bearer rzp_live_abc123
Content-Type: application/json
Accept: application/json
```

| Header | Purpose |
|---|---|
| `Authorization` | Proves who you are — always sent in headers, never in URL |
| `Content-Type` | Tells server what format your body is in |
| `Accept` | Tells server what format you want back |

> **Security rule:** Never put your token in the URL — it gets logged in server logs and exposed to anyone with log access.

---

### Part 4 — Body

Only `POST`, `PUT`, `PATCH` have a body. It carries the actual data.

```json
POST /v1/orders
{
  "amount": 50000,
  "currency": "INR",
  "receipt": "order_rcpt_001"
}
```

---

## Chapter 3 — Anatomy of an HTTP Response

Every response has **3 parts:**

```
┌──────────────────────────────────────────┐
│  1. STATUS CODE  → Did it work?          │
│  2. HEADERS      → Meta about response   │
│  3. BODY         → The actual data back  │
└──────────────────────────────────────────┘
```

### Status Codes

```
2xx  ✅  Success
3xx  🔀  Redirect
4xx  ❌  Your fault (client error)
5xx  💥  Server's fault
```

| Code | Meaning | When |
|---|---|---|
| `200` | OK | Request succeeded |
| `201` | Created | New resource made after POST |
| `204` | No Content | Success but nothing to return |
| `400` | Bad Request | You sent invalid data |
| `401` | Unauthorized | No token / wrong token |
| `403` | Forbidden | Token valid, but no permission |
| `404` | Not Found | Resource doesn't exist |
| `422` | Unprocessable | FastAPI validation failed |
| `500` | Internal Server Error | Backend crashed |

### 401 vs 403 — The Interview Trap

| Code | Meaning |
|---|---|
| `401` | "I don't know who you are" |
| `403` | "I know who you are, but you can't do this" |

---

## Chapter 4 — REST Principles

REST = **Representational State Transfer**  
6 rules the whole industry agreed on. Most APIs claim to be REST. Most are faking it.

### Core Idea — Resources, Not Actions

```
❌  Bad (action in URL)          ✅  Good (resource in URL)
/getUser                          /users/1
/createOrder                      /orders
/deletePayment?id=5               /payments/5
/getUserOrders?userId=3           /users/3/orders
```

> The **method** carries the action. The **URL** carries the resource.

---

### The 6 REST Constraints

#### 1. Client-Server Separation
Client and server are completely independent. FastAPI doesn't care if the caller is a browser, mobile app, or curl command.

#### 2. Stateless
Every request must contain everything the server needs. No memory between requests.

```python
# Token sent on EVERY request — server doesn't remember you
headers = {"Authorization": "Bearer eyJhbGci..."}
requests.get("/orders", headers=headers)
```

#### 3. Uniform Interface
All resources follow the same predictable CRUD pattern:

```
GET    /users          → list all users
POST   /users          → create a user
GET    /users/1        → get user 1
PATCH  /users/1        → update user 1
DELETE /users/1        → delete user 1
```

#### 4. Cacheable
Responses declare if they can be cached. `GET` responses often are. `POST` responses never are.

```
Cache-Control: max-age=3600   ← fresh for 1 hour
```

#### 5. Layered System
The client doesn't know (or care) if it's talking to FastAPI directly, or through Nginx, or a load balancer.

```
Client → Nginx → Load Balancer → FastAPI Instance 1
                              → FastAPI Instance 2
```

#### 6. Code on Demand *(optional)*
Server can send executable code (like JS) to the client. Rarely used.

---

### Resource Nesting Rule

When one resource *belongs to* another — nest it:

```
/users/3/orders          → all orders of user 3
/users/3/orders/99       → order 99 of user 3
/restaurants/5/menu      → menu of restaurant 5
```

---

### Food Delivery API — REST Design

```
GET    /restaurants              → list all restaurants
GET    /restaurants/5/menu       → menu for restaurant 5
POST   /orders                   → place a new order
GET    /orders/99                → track order 99
PATCH  /orders/99                → update order status (cancel, prepare, deliver)
```

> Why `PATCH` and not `DELETE` to cancel an order?  
> Because cancelled orders must stay in the DB — for refunds, audit trails, and business analytics. `DELETE` removes the record. `PATCH` preserves it with a `"status": "cancelled"` field.

---

### Common REST Anti-Patterns (What NOT to do)

```
❌ POST /updateUserEmail           → action in URL
❌ GET  /deleteOrder?id=5          → GET doing destructive work
❌ POST /user/getOrders            → should be GET /users/3/orders
❌ Returning 200 OK on an error    → status and body must agree
```

The last one is a crime against REST:

```json
// WRONG — lying in the status code
HTTP 200 OK
{ "error": "User not found" }

// CORRECT
HTTP 404 Not Found
{ "detail": "User not found" }
```

---

## Chapter 5 — Python `requests` Library

### Setup

```bash
pip install requests
```

---

### GET — Fetch a resource

```python
import requests

response = requests.get("https://jsonplaceholder.typicode.com/users/1")

print(response.status_code)              # 200
print(response.headers["Content-Type"]) # application/json
print(response.json())                  # Python dict of user data
```

---

### POST — Create a resource

```python
import requests

new_order = {
    "userId": 1,
    "title": "Chicken Biryani x2",
    "body": "Deliver to 14B, Chennai"
}

response = requests.post(
    "https://jsonplaceholder.typicode.com/posts",
    json=new_order  # auto sets Content-Type: application/json
)

print(response.status_code)  # 201
print(response.json())       # echoes back the created resource with new id
```

---

### PATCH — Update part of a resource

```python
import requests

response = requests.patch(
    "https://jsonplaceholder.typicode.com/posts/1",
    json={"status": "cancelled"}
)

print(response.status_code)  # 200
print(response.json())
```

---

### PUT — Replace an entire resource

```python
import requests

response = requests.put(
    "https://jsonplaceholder.typicode.com/posts/1",
    json={
        "id": 1,
        "title": "Updated Title",
        "body": "Entire body replaced",
        "userId": 1
    }
)

print(response.status_code)  # 200
print(response.json())
```

---

### DELETE — Remove a resource

```python
import requests

response = requests.delete(
    "https://jsonplaceholder.typicode.com/posts/1"
)

print(response.status_code)  # 200
print(response.json())       # {} — empty, resource is gone
```

---

### Sending Headers — Auth tokens

```python
import requests

headers = {
    "Authorization": "Bearer fake_token_123",
    "Accept": "application/json"
}

response = requests.get(
    "https://jsonplaceholder.typicode.com/users",
    headers=headers
)

print(response.status_code)
print(len(response.json()), "users found")  # 10 users found
```

---

### Error Handling — What senior devs always do

```python
import requests

def get_user(user_id: int):
    response = requests.get(
        f"https://jsonplaceholder.typicode.com/users/{user_id}"
    )

    if response.status_code == 200:
        return response.json()
    elif response.status_code == 404:
        print(f"User {user_id} not found")
        return None
    else:
        print(f"Unexpected error: {response.status_code}")
        return None

print(get_user(1))    # returns user dict
print(get_user(999))  # "User 999 not found"
```

> Junior devs skip error handling.  
> Senior devs **always** check status codes before calling `.json()`.

---

## Chapter 6 — Quiz Results

**Score: 10 / 10** ✅

| # | Topic | Result |
|---|---|---|
| 1 | Client vs Server | ✅ |
| 2 | Stateless definition | ✅ |
| 3 | Correct REST URL for DELETE | ✅ |
| 4 | 401 vs 403 | ✅ |
| 5 | Nested resource URL | ✅ |
| 6 | Query params for GET filters | ✅ |
| 7 | Status code for POST (201) | ✅ |
| 8 | Authorization token placement | ✅ |
| 9 | PUT vs PATCH | ✅ |
| 10 | 200 on error anti-pattern | ✅ |

---

## Quick Reference Card

```
METHOD    USE WHEN                         HAS BODY?
GET       Fetching data                    No
POST      Creating a new resource          Yes
PUT       Replacing entire resource        Yes
PATCH     Updating part of a resource      Yes
DELETE    Removing a resource              No

STATUS    MEANING
200       OK — worked
201       Created — new resource born
400       Bad Request — invalid data sent
401       Unauthorized — no/wrong token
403       Forbidden — valid token, no permission
404       Not Found — resource doesn't exist
422       Unprocessable — validation failed (FastAPI)
500       Server Error — backend crashed

REST RULES
1. URLs are resources (nouns), methods are actions (verbs)
2. Always plural — /users not /user
3. Nest related resources — /users/3/orders
4. Status code and body must agree — never 200 on an error
5. Token always goes in Authorization header — never in URL
6. Every request is stateless — carry everything the server needs
```

---

*Notes compiled: June 2026 | Next: FastAPI Module 1 — Foundations*
