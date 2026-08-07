<div align="center">

# 📝 Prisma Blog App

### A lightweight, type-safe blog API backend built with Express, TypeScript & Prisma

*Posts&nbsp;•&nbsp;Nested Comments&nbsp;•&nbsp;Authentication&nbsp;•&nbsp;Role-Based Access*

![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Express](https://img.shields.io/badge/Express-5.2-000000?style=for-the-badge&logo=express&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-7.2-2D3748?style=for-the-badge&logo=prisma&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white)

</div>

<br>

---

## 📖 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Database Schema](#-database-schema)
- [Getting Started](#-getting-started)
- [Environment Variables](#-environment-variables)
- [Available Scripts](#-available-scripts)
- [API Endpoints](#-api-endpoints)
- [Roadmap](#-roadmap)
- [License](#-license)

---

## 📌 Overview

**Prisma Blog App** is a minimal, production-ready backend for a blogging platform. It's built with **Express** and **TypeScript**, uses **Prisma ORM** on top of **PostgreSQL**, and ships with **Better Auth** for secure, session-based authentication out of the box.

The API supports posts with tags, featured/draft states and view tracking, plus a fully **threaded (nested) comment system** — all protected by clean, reusable role-based middleware.

---

## ✨ Features

- 🔐 **Authentication** — session-based auth via Better Auth, with email verification support
- 👥 **Role-Based Access Control** — `USER` / `ADMIN` roles enforced through middleware
- 📰 **Post Management** — create, tag, and organize posts with `DRAFT` / `PUBLISHED` / `ARCHIVED` states
- ⭐ **Featured Posts** — highlight selected posts
- 👁️ **View Tracking** — automatic view counting per post
- 💬 **Threaded Comments** — nested replies with `APPROVED` / `REJECT` moderation status
- 🏷️ **Tagging System** — flexible string-array tags per post
- 🖼️ **Thumbnails** — optional post thumbnail support
- 🌐 **CORS Ready** — configurable origin via environment variable
- ⚡ **Fast Dev Loop** — hot-reload with `tsx watch`

---

## 🧰 Tech Stack

<div align="left">

**Core**

![Express](https://img.shields.io/badge/Express-5.2.1-000000?style=flat-square&logo=express&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5.9.3-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-7.2.0-2D3748?style=flat-square&logo=prisma&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-8.16.3_(pg)-336791?style=flat-square&logo=postgresql&logoColor=white)

**Auth & Middleware**

![Better Auth](https://img.shields.io/badge/Better_Auth-1.4.9-6366F1?style=flat-square)
![CORS](https://img.shields.io/badge/CORS-2.8.5-FF6B6B?style=flat-square)

**Tooling**

![tsx](https://img.shields.io/badge/tsx-4.21.0-F7DF1E?style=flat-square)
![pnpm](https://img.shields.io/badge/pnpm-10.20.0-F69220?style=flat-square&logo=pnpm&logoColor=white)
![Nodemailer](https://img.shields.io/badge/Nodemailer-7.0.12-1B4E5A?style=flat-square)

</div>

---

## 🗂️ Project Structure

```
prisma-blog-app/
├── src/
│   ├── lib/                 # Core libraries (Prisma client, Better Auth config)
│   ├── middlewares/         # Auth & role-based access middleware
│   ├── modules/
│   │   └── post/            # Post module (controller, service, router)
│   ├── app.ts                # Express app configuration
│   └── server.ts             # Entry point — connects DB & starts server
├── prisma/
│   └── schema.prisma          # Database schema
├── package.json
└── tsconfig.json
```

---

## 🗃️ Database Schema

| Model | Description |
|---|---|
| **Post** | Blog posts with title, content, tags, thumbnail, view count, and status |
| **Comment** | Threaded comments with self-relation for nested replies |
| **User** | Managed by Better Auth — includes role & account status |
| **Session** | Better Auth session tracking |
| **Account** | Better Auth linked accounts / credentials |
| **Verification** | Email verification tokens |

**Post statuses:** `DRAFT` · `PUBLISHED` · `ARCHIVED`
**Comment statuses:** `APPROVED` · `REJECT`

---

## 🚀 Getting Started

### Prerequisites

- Node.js 20+
- pnpm `10.20.0`
- A running PostgreSQL instance

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/your-username/prisma-blog-app.git
cd prisma-blog-app

# 2. Install dependencies
pnpm install

# 3. Set up environment variables
cp .env.example .env

# 4. Push the Prisma schema to your database
npx prisma db push

# 5. Generate the Prisma client
npx prisma generate

# 6. Start the dev server
pnpm dev
```

The server will start at **http://localhost:3000** 🎉

---

## 🔑 Environment Variables

Create a `.env` file in the project root:

```env
PORT=3000
DATABASE_URL=postgresql://user:password@localhost:5432/prisma_blog_app
APP_URL=http://localhost:3000

# Better Auth
BETTER_AUTH_SECRET=your_secret_key
BETTER_AUTH_URL=http://localhost:3000

# Nodemailer (email verification)
SMTP_HOST=
SMTP_PORT=
SMTP_USER=
SMTP_PASS=
```

---

## 📜 Available Scripts

| Command | Description |
|---|---|
| `pnpm dev` | Start development server with hot-reload |
| `npx prisma db push` | Sync Prisma schema with database |
| `npx prisma generate` | Generate Prisma client |
| `npx prisma studio` | Open Prisma Studio (visual DB browser) |

---

## 🔌 API Endpoints

### Auth
| Method | Endpoint | Description |
|---|---|---|
| `ALL` | `/api/auth/*` | Handled by Better Auth (sign up, sign in, sessions, etc.) |

### Posts
| Method | Endpoint | Access | Description |
|---|---|---|---|
| `GET` | `/posts` | Public | Get all posts |
| `POST` | `/posts` | Auth required | Create a new post |

> 📌 Extend `postRouter` to add endpoints for single post retrieval, updates, deletion, and comment management following the same pattern.

### Health Check
| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/` | Returns `"Hello, World!"` — server health check |

---

## 🗺️ Roadmap

- [ ] Full CRUD for posts (`GET /posts/:id`, `PATCH`, `DELETE`)
- [ ] Comment endpoints (create, reply, moderate)
- [ ] Post search & filtering by tag/status
- [ ] Pagination for post listings
- [ ] Image upload for thumbnails
- [ ] Admin moderation dashboard endpoints

---

## 📄 License

This project is licensed under the **ISC License**.

<div align="center">

Made with ❤️ using Express, Prisma & TypeScript

</div>
