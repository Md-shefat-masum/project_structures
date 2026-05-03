---

# ✅ PROJECT STRUCTURE MERN

```id="final_tree_001"
/
│
├── src/
│   │
│   ├── controllers/
│   │   └── user.controller.js
│   │
│   ├── services/
│   │   ├── user.service.js
│   │   ├── db.service.js
│   │   └── cache.service.js
│   │
│   ├── queries/
│   │   └── users.query.js
│   │
│   ├── models/
│   │   └── user.model.js
│   │
│   ├── routes/
│   │   └── user.routes.js
│   │
│   ├── middlewares/
│   │   └── errorHandler.js
│   │
│   ├── validators/
│   │   └── user.validator.js
│   │
│   ├── utils/
│   │   ├── logger.js
│   │   └── response.js
│   │
│   ├── config/
│   │   ├── db.js
│   │   └── redis.js
│   │
│   ├── seed/
│   │   └── users.seed.js
│   │
│   ├── constants/
│   │   └── app.constants.js
│   │
│   ├── views/
│   │   └── users.ejs
│   │
│   ├── public/
│   │
│   └── app.js
│
├── docker/
│   ├── Dockerfile
│   └── docker-compose.yml
│
├── ecosystem.config.js
├── .env
├── package.json
└── README.md
```

---

# 🧠 DEMO FILES (IMPORTANT PART)

---

## 📁 src/app.js

```js id="app_js"
const express = require("express");
const app = express();

const userRoutes = require("./routes/user.routes");

app.use(express.json());
app.use(express.urlencoded({ extended: true }));

app.set("view engine", "ejs");

app.use("/users", userRoutes);

// global error handler
const errorHandler = require("./middlewares/errorHandler");
app.use(errorHandler);

module.exports = app;
```

---

## 📁 routes/user.routes.js

```js id="user_routes"
const router = require("express").Router();
const userController = require("../controllers/user.controller");

router.get("/", userController.getUsers);
router.get("/:id", userController.getUserById);

module.exports = router;
```

---

## 📁 controllers/user.controller.js

```js id="user_controller"
const userService = require("../services/user.service");

module.exports = {
  getUsers: async (req, res) => {
    const data = await userService.getUsers(req.query);
    res.json(data);
  },

  getUserById: async (req, res) => {
    const data = await userService.getUserById(req.params.id);
    res.json(data);
  }
};
```

---

## 📁 services/user.service.js

```js id="user_service"
const userQuery = require("../queries/users.query");
const seedUsers = require("../seed/users.seed");

module.exports = {
  getUsers: async (filters) => {
    const dbData = await userQuery.get_users(filters);

    return dbData || seedUsers.get_users(filters);
  },

  getUserById: async (id) => {
    const dbData = await userQuery.get_public_user(id);

    return dbData || seedUsers.get_public_user(id);
  }
};
```

---

## 📁 queries/users.query.js

```js id="users_query"
module.exports = {
  get_users: async (filters) => {
    // MongoDB query (later)
    return null;
  },

  get_public_user: async (id) => {
    return null;
  }
};
```

---

## 📁 seed/users.seed.js

```js id="users_seed"
module.exports = {
  get_users: (filters) => {
    return [{ id: 1, name: "Seed User" }];
  },

  get_public_user: (id) => {
    return { id, name: "Seed Single User" };
  }
};
```

---

## 📁 config/db.js

```js id="db_config"
const mongoose = require("mongoose");

module.exports = async () => {
  try {
    await mongoose.connect(process.env.MONGO_URI);
    console.log("DB Connected");
  } catch (err) {
    console.log("DB Not Connected - running in fallback mode");
  }
};
```

---

## 📁 config/redis.js

```js id="redis_config"
const redis = require("redis");
const client = redis.createClient();

client.on("error", () => {
  console.log("Redis not available");
});

module.exports = client;
```

---

## 📁 middlewares/errorHandler.js

```js id="error_handler"
module.exports = (err, req, res, next) => {
  console.error(err);
  res.status(500).json({ message: "Server Error" });
};
```

---

## 📁 utils/logger.js

```js id="logger"
module.exports = {
  info: (msg) => console.log("[INFO]", msg),
  error: (msg) => console.log("[ERROR]", msg)
};
```

---

## 📁 views/users.ejs

```ejs id="users_ejs"
<h1>Users Page</h1>

<ul>
  <% users.forEach(user => { %>
    <li><%= user.name %></li>
  <% }) %>
</ul>
```

---

## 📁 ecosystem.config.js (PM2)

```js id="pm2"
module.exports = {
  apps: [
    {
      name: "app",
      script: "./src/app.js",
      instances: 2,
      exec_mode: "cluster"
    }
  ]
};
```

---

* MVC (clean separation)
* Query layer (DB abstraction)
* Service layer (business logic)
* Seed fallback (offline safety)
* Redis cache ready
* EJS frontend support
* PM2 cluster production
* Docker ready structure


