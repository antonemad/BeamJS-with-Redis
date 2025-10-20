# How to Contribute to BeamJS: Adding Redis Support

## Introduction

**BeamJS** is an enterprise-grade, full-stack web development framework built on top of **Backend-JS**.  
It’s designed for building **modular**, **behavior-driven**, and **scalable** systems that can connect to multiple types of databases — both SQL and NoSQL.  
Currently, BeamJS supports databases such as **MongoDB** and **SQL (via Sequelize)** through its unified **data controller** system.  

In this article, we’ll go through a simple, practical guide on how to contribute by adding support for a new database: **Redis**.

---

## 1. Understanding the Idea Behind the Contribution

Before contributing, it’s important to understand how BeamJS handles database logic.  
BeamJS uses something called a **data controller** — a middle layer between the framework and the database.  

So instead of directly connecting to MongoDB or SQL, BeamJS interacts with a controller, and that controller takes care of database operations.  
That means if we want to add **Redis**, we just need to create a new controller (let’s call it `RedisController`) that follows the same pattern as the existing ones.

---

## 2. Steps to Add Redis Support

### Step 1: Fork and Set Up the Project

1. Go to the [BeamJS repository](https://github.com/QuaNode/beamjs).
2. Click on **Fork** to create your own copy.
3. Clone your fork and install dependencies:

```bash
git clone https://github.com/<your-username>/beamjs.git
cd beamjs
npm install
```

---

### Step 2: Explore Existing Controllers

Inside the project, open this folder:

```bash
src/database/controllers/
```

You’ll find files like:

- `MongoController.js`
- `SQLController.js`

These files define how BeamJS connects to each type of database.  
Read through them to understand the structure, function names, and logic — this will help you design your own Redis version.

---

### Step 3: Create a Redis Controller

Create a new file:

```bash
src/database/controllers/RedisController.js
```

This file will handle reading and writing data in Redis.  
For example:

- To **get** data → use Redis commands like `HGETALL`
- To **add** data → use `HSET` or `SET`
- To **delete** data → use `DEL`

The idea is to make Redis work just like MongoDB or SQL from BeamJS’s point of view.

---

### Step 4: Register Your Controller

After creating the file, you’ll need to **register** your new controller so that BeamJS recognizes it.

Look for the part of the code where the framework chooses which controller to use (it usually checks something like `DB_TYPE` or `databaseKey` in the configuration).  
Add an entry for `"redis"` so that BeamJS knows to use your new controller when Redis is selected.

---

### Step 5: Test the Integration

You can easily test Redis locally using Docker:

```bash
docker run -p 6379:6379 --name beamjs-redis -d redis
```

Then try running basic operations from your controller to ensure everything connects correctly and data can be saved, retrieved, and deleted.

---

## 3. Writing Documentation

Once the Redis controller works, you can add a short documentation file to explain how to use it.

Example path:

```bash
docs/usage/redis.md
```

Inside that file, include:

- How to enable Redis in BeamJS.
- Example environment variables (`REDIS_URL`).
- Any known limitations (for example, Redis is a key-value store, not relational).

This makes it easier for other developers to use or improve your contribution.

---

## 4. Submitting Your Contribution

When everything is ready:

1. Commit your changes:
   ```bash
   git add .
   git commit -m "Add Redis support to BeamJS"
   ```
2. Push them to your fork:
   ```bash
   git push origin main
   ```
3. Open a **Pull Request (PR)** to the main BeamJS repository.

In your PR description, you can write something like:

> This PR introduces Redis support for BeamJS by adding a new RedisController.  
> It allows BeamJS to connect to Redis through the unified data controller API, similar to MongoDB and SQL.

---

## 5. Conclusion

Contributing to **BeamJS** is a great opportunity to learn about backend architecture, database abstraction, and open-source collaboration.  
Contributing to BeamJS is part of my ongoing journey to improve my backend development skills and apply what I learn in real projects.
By exploring how BeamJS handles databases and working on adding Redis support, I’m trying to turn my learning into something practical and useful for others too.

My goal isn’t just to add a new feature, but to understand how real-world frameworks are built and maintained — and to keep growing through hands-on experience and open-source collaboration.

---

### Author

**Anton Emad**  
Contributor – BeamJS Framework  
GitHub: [@AntonEmad](https://github.com/AntonEmad)
