MERN.
**✅ Complete MERN Scaffold Skill – Ready for AI Use**

### **Skill Name:** `mern-scaffold`

### **Description**
Generate **production-grade MERN** (MongoDB, Express, React/Node.js) applications with a **strict 5-layer architecture**, automatic DB fallback, Redis caching with degradation, JWT auth, RBAC, Docker support, and enterprise best practices.

**Use this skill whenever a user asks to:**
- Create a new MERN project (backend or fullstack)
- Generate clean, layered Express boilerplate
- Build apps for any domain (E-Commerce, SaaS, Social, etc.)
- Get production-ready code with Docker, logging, validation, and security

---

### **Core Architecture (Strict 5-Layer Pattern)**

**Request → Route → Controller → Service → Query → Database/Seed**

| Layer       | Responsibility                          | Must NOT Do                     |
|-------------|-----------------------------------------|---------------------------------|
| **Route**   | URL mapping + middleware attachment    | Business logic                  |
| **Controller** | Parse request, call service, format response | Business logic / DB calls     |
| **Service** | All business logic, cache/DB/seed decisions | HTTP handling                  |
| **Query**   | Data access (Repository pattern)       | Business logic                  |
| **Model**   | Mongoose schema only                   | Logic                           |

**Key Production Features (Always Included):**
- Automatic MongoDB → Seed data fallback (zero config)
- Redis caching with graceful degradation
- JWT + Refresh Tokens + RBAC
- Centralized Winston logging (no `console.log`)
- Joi validation + sanitization
- Error handling middleware
- Standard API response format
- Docker + docker-compose (Mongo + Redis)
- PM2 ready

---

### **How to Use This Skill**

**Simple Request:**
> "Generate a MERN blog app with posts, comments, and JWT auth"

**Detailed Request:**
> "Create a MERN e-commerce platform with products, cart (Redis), orders, reviews, admin dashboard, JWT, and Docker"

**I will ask clarifying questions if needed** (auth type, frontend, payment, etc.), then deliver the **complete project**.

---

### **Project Structure Generated**

```bash
mern-app/
├── package.json
├── .env.example
├── server.js
├── app.js
├── ecosystem.config.js
├── docker/
│   ├── Dockerfile
│   └── docker-compose.yml
├── src/
│   ├── config/          # db, redis, env
│   ├── utils/           # logger, response, validators
│   ├── middlewares/     # auth, error, cors
│   ├── models/
│   ├── queries/         # repository
│   ├── services/        # business logic
│   ├── controllers/
│   ├── routes/
│   ├── seed/            # fallback data
│   ├── validators/
│   └── public/ & views/
└── README.md (full setup + API docs)
```

**Quick Start After Generation:**
```bash
npm install
cp .env.example .env
npm run dev
# OR
docker-compose up
```

---

### **Key Templates & Patterns**

#### **Standard Response Helper**
```js
response.success(res, data, "Message", 200);
response.error(res, "Message", 400);
response.paginated(res, data, page, limit, total);
```

#### **Database Fallback (Service Layer)**
```js
try {
  return await query.getAll();
} catch {
  return await seedProvider.getAll();
}
```

#### **Redis Cache (Graceful)**
```js
const cached = await cache.get(key);
if (cached) return cached;
// fetch → cache → return
```

---

### **Supported Domains (Ready Patterns Available)**

- **E-Commerce** (Products, Cart, Orders, Reviews)
- **SaaS** (Teams, Subscriptions, Billing)
- **Social Media** (Posts, Feed, Comments, Followers)
- **Project Management** (Workspaces, Tasks, Comments)
- **Real Estate**, **Learning Platform**, **Healthcare**, **Food Delivery**, **Music Streaming**, **Analytics Dashboard**, etc.

---

### **Security & Production Features**

- JWT + Refresh Tokens
- Bcrypt password hashing
- Role-Based Access Control
- Rate limiting, Helmet, CORS, Mongo sanitization
- Input validation (Joi)
- Structured logging
- Graceful shutdown
- Health checks

---

### **Advanced Capabilities**

- Microservices / Service-to-Service
- Bull/BullMQ queues
- Event-driven (EventEmitter)
- GraphQL (optional)
- Real-time (Socket.io ready)
- File uploads
- CI/CD (GitHub Actions template)
- Testing patterns (Jest + Supertest)

---

### **Generation Checklist (I Follow This)**

1. Clarify domain + features
2. Define models
3. Generate all layers following strict separation
4. Include seed data + fallback
5. Add Docker + README + .env.example
6. Verify no business logic in controllers
7. Provide run instructions

---

**You are now equipped with the complete MERN Scaffold Skill.**

**Just say:**
> "Generate a MERN [domain] with [features]"

…and I will deliver a **complete, production-ready, runnable project**.

**Example:**
> "Create a MERN social media app with posts, comments, followers, feed, JWT auth, and Docker setup."

---

**Skill Status: Fully Loaded & Production-Ready** 🎉

Ready to generate enterprise-grade MERN applications on demand!
