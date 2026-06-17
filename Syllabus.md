# 🚀 FastAPI Complete Learning Curriculum
> Validated against Udemy #1 Bestseller — *FastAPI: The Complete Course 2026 (Beginner + Advanced)*  
> Built for: Python backend engineering → Product companies (Chargebee, Razorpay, Freshworks)

---

## ✅ Pre-requisites (Already Done)
- [x] HTTP & REST fundamentals
- [x] Methods, Status Codes, Headers, URL design
- [x] REST principles & resource-based design
- [x] Python basics (in progress — W1/W2)

---

## 📦 Module 1 — FastAPI Foundations
> *Install, run, and understand your first real API*

- 1.1 What is FastAPI — and why it beats Flask & Django for APIs
- 1.2 Installation, virtual environment setup (`venv`), project structure
- 1.3 Your first endpoint — `GET /hello`
- 1.4 Path parameters — `/users/{id}`
- 1.5 Query parameters — `/restaurants?city=Chennai`
- 1.6 Combining path + query params
- 1.7 Automatic docs — Swagger UI (`/docs`) & ReDoc (`/redoc`)
- 1.8 How FastAPI uses Python type hints to do magic
- 1.9 **Mini Project:** Restaurant listing API

---

## 📦 Module 2 — Request & Response Control
> *Sending and receiving data the right way*

- 2.1 POST requests & reading JSON body
- 2.2 Pydantic models — your first `BaseModel`
- 2.3 Response models — controlling exactly what you return
- 2.4 Returning correct status codes — `201`, `404`, `400`
- 2.5 `HTTPException` — returning errors cleanly
- 2.6 Request headers & cookies
- 2.7 Form data & handling user input
- 2.8 **Mini Project:** Order placement API

---

## 📦 Module 3 — Data Validation with Pydantic
> *The superpower inside FastAPI — never trust raw input*

- 3.1 `BaseModel` deep dive — defining schemas
- 3.2 Field types, default values, constraints (`min_length`, `gt`, `le`)
- 3.3 Nested models — `Order` contains list of `Item`
- 3.4 Optional fields & partial updates for `PATCH`
- 3.5 Custom validators with `@validator` / `@field_validator`
- 3.6 Pydantic v2 differences (what changed, what to know)
- 3.7 **Mini Project:** User registration with full input validation

---

## 📦 Module 4 — Project Structure & Routers
> *How real production APIs are organized — not one giant file*

- 4.1 Why one file breaks at scale
- 4.2 `APIRouter` — splitting endpoints into feature modules
- 4.3 Industry folder structure (routers / models / schemas / services)
- 4.4 Dependency Injection — FastAPI's `Depends()`
- 4.5 Reusable dependencies (auth checks, DB sessions)
- 4.6 **Mini Project:** Refactor food delivery app into clean modules

---

## 📦 Module 5 — Database Integration
> *Persisting real data with SQLAlchemy + PostgreSQL*

- 5.1 Why dicts don't cut it — intro to relational DBs
- 5.2 SQLAlchemy setup & ORM models
- 5.3 Connecting FastAPI to PostgreSQL
- 5.4 Alembic — database migrations
- 5.5 CRUD operations — Create, Read, Update, Delete
- 5.6 Database relationships — User has many Orders (`CASCADE`)
- 5.7 Production DB setup (PostgreSQL)
- 5.8 **Mini Project:** Full DB-backed order management system

---

## 📦 Module 6 — Authentication & Authorization
> *The #1 topic in every backend interview*

- 6.1 How auth works in REST APIs (sessions vs tokens)
- 6.2 Password hashing with `bcrypt`
- 6.3 JWT tokens — create, sign, decode, verify
- 6.4 OAuth2 with Password Flow (FastAPI built-in)
- 6.5 Protected routes — login required (`Depends`)
- 6.6 Role-based access control — admin vs regular user
- 6.7 Token refresh strategy
- 6.8 **Mini Project:** Full auth system for food delivery app

---

## 📦 Module 7 — Advanced FastAPI
> *What separates junior from mid-level engineers*

- 7.1 `async def` vs `def` — when and why
- 7.2 Async database queries with `asyncpg`
- 7.3 Background tasks — fire and forget
- 7.4 File uploads — images, documents
- 7.5 Middleware — logging, timing, CORS
- 7.6 Rate limiting
- 7.7 WebSockets basics
- 7.8 **Mini Project:** Add async + middleware to food delivery app

---

## 📦 Module 8 — Testing
> *What product companies actually look for — tested code*

- 8.1 Why testing matters (and what it signals in interviews)
- 8.2 `pytest` setup for FastAPI
- 8.3 `httpx` — async test client
- 8.4 Unit tests vs integration tests
- 8.5 Test database setup (separate DB for tests)
- 8.6 Writing real test cases — happy path + edge cases
- 8.7 Coverage reports
- 8.8 **Mini Project:** Full test suite for your food delivery API

---

## 📦 Module 9 — Production & Deployment
> *Ship it — make your API live for the world*

- 9.1 Environment variables & `.env` files with `python-dotenv`
- 9.2 Docker — containerizing your FastAPI app
- 9.3 Docker Compose — app + DB together
- 9.4 CI/CD basics — GitHub Actions
- 9.5 Deploying to Railway / Render (free tier)
- 9.6 Monitoring & logging in production
- 9.7 **Capstone Project:** Full production-ready Food Delivery API

---

## 🏁 Capstone — Food Delivery API (Full Stack Backend)
> *Everything you built, combined into one deployable system*

```
Features:
✅ Restaurant & menu management
✅ User registration & login (JWT)
✅ Order placement & tracking
✅ Role-based access (admin / customer)
✅ PostgreSQL database
✅ Async endpoints
✅ Full test suite
✅ Dockerized & deployed
```

---

## 📊 Curriculum vs Udemy Comparison

| Topic | Udemy Course | This Curriculum |
|---|---|---|
| FastAPI basics & setup | ✅ | ✅ |
| Path & query params | ✅ | ✅ |
| Pydantic validation | ✅ | ✅ (deeper) |
| HTTP status codes | ✅ | ✅ |
| SQLAlchemy + DB | ✅ | ✅ |
| MySQL / PostgreSQL | ✅ | ✅ |
| bcrypt password hashing | ✅ | ✅ |
| JWT authentication | ✅ | ✅ |
| Routing / APIRouter | ✅ | ✅ |
| Unit & integration testing | ✅ | ✅ (deeper) |
| Full stack development | ✅ | ✅ |
| Deployment | ✅ | ✅ |
| Async / await | ❌ | ✅ |
| Middleware | ❌ | ✅ |
| Rate limiting | ❌ | ✅ |
| WebSockets | ❌ | ✅ |
| Docker + CI/CD | ❌ | ✅ |
| Dependency Injection deep dive | ❌ | ✅ |

---

## 🗓️ Suggested Pace
> *Alongside your Python curriculum (W4+ onwards)*

| Module | Start When |
|---|---|
| 1 — Foundations | Python W4 (libraries done) |
| 2–3 — Requests & Pydantic | Python W5 |
| 4 — Routers & Structure | Python W7 (OOP done) |
| 5 — Database | Python W8 |
| 6 — Auth | Python W9 |
| 7–9 — Advanced + Deploy | Python W11–W12 |

---

*Curriculum version 1.0 — Mohamed Salman | June 2026*
