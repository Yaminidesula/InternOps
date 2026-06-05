# InternOps

Enterprise Workforce Management & Intern Operations Platform

[![Node.js](https://img.shields.io/badge/node-%E3%80%8E18.0.0-brightgreen.svg)](https://nodejs.org/)
[![PostgreSQL](https://img.shields.io/badge/postgres-%E3%80%8E14.0-blue.svg)](https://www.postgresql.org/)
[![Fastify](https://img.shields.io/badge/fastify-4.x-000000.svg))(https://www.fastify.io/)
[![React](https://img.shields.io/badge/react-18.x-61DAFB.svg)](https://react.dev/)
[![License](https://img.shields.io/badge/license-Proprietary-blue.svg)](LICENSE)

Production-grade workforce management with five-tier hierarchy, immutable records, proof-verified tasks, meetings, analytics, audit logs, and full security. Built on Node.js + Fastify + PostgreSQL (raw SQL) with a React + Vite frontend.

## Key Features

- **Hierarchy**: Admin → Senior TL → TL → Captain → Intern; recursive ownership
- **Auth**: JWT access/refresh tokens, Argon2id, brute-force lockout, password reset
- **Attendance**: single/bulk, monthly stats, remarks, immutable records
- **Ratings**: historical, never overwritten; only direct manager can rate
- **Social Tasks**: create tasks, upload screenshot proof, verify, auto-delete 24h
- **Meetings**: schedule with attendees, hierarchy-based visibility
- **Notifications**: in-app alerts, pagination, read/unread, bulk actions
- **Reports & Analytics**: attendance summaries, trends, task completion, CSV export
- **Sessions**: view/revoke own; admin can revoke any user's sessions
- **Audit**: immutable logs with old/new values, IP, user-agent for every action
- **Security**: Helmet, CORS, CSRF, rate limiting, input sanitisation, soft deletes

## Technology

| Layer     | Technology |
|------------|------------|
| Backend   | Node.js 18+, Fastify v4  |
| Database  | PostgreSQL (raw SQL via `pg`)  |
| Frontend  | React 18, Vite 5, TailwindCSS 3, Axios  |
| Auth      | JWT, Argon2id, Zod  |
| State     | Zustand, TanStack Query  |
| Security  | Helmet, CORS, CSRF, Rate Limiting  |
| Docs      | Swagger (OpenAPI)  |

## Database

13 tables: users, departments, attendance, ratings, social_tasks,
proof_submissions, notifications, meetings, meeting_attendees, audit_logs,
refresh_tokens, password_reset_tokens, login_attempts.

UUID PKs, foreign keys, indexes, soft deletes, JSON audit, transactions.

## API

| Module        | Prefix              | Purpose |
|----------------|-----------------------|---------|
| Auth          | /api/auth           | Login, register, refresh, logout, password reset, CSRF |
| Users         | /api/users          | CRUD, profile, password, suspend/activate |
| Departments   | /api/departments    | Create & list |
| Hierarchy     | /api/hierarchy      | Direct reports, full team, upward chain |
| Attendance    | /api/attendance     | Mark, bulk, view, monthly stats |
| Ratings       | /api/ratings        | Submit (manager), view history |
| Tasks         | /api/tasks          | Create, list social tasks |
| Proofs        | /api/proofs         | Submit (intern), verify (captain+) |
| Notifications | /api/notifications  | List, mark read, delete, bulk read |
| Audit         | /api/audit          | View logs (admin only) |
| Uploads       | /api/uploads       | Avatar upload |
| Analytics     | /api/analytics      | Overview, dept attendance, top performers |
| Meetings      | /api/meetings       | CRUD, attendees |
| Sessions      | /api/sessions       | List own, revoke, admin revoke |
| Reports       | /api/reports        | Summaries, task completion, CSV export |
| Uptoskills    | /api/uptoskills     | Placeholder for integration |

## Quick Start

```bash
git clone https://github.com/rajat-wyrm/InternOps.git
cd InternOps
cd backend && npm install && cd ../frontend && npm install
cp backend/.env.example backend/.env   # edit with your config
cd backend && npm run migrate && npm run seed
npm run dev                           # backend on :5000
cd ../frontend && npm run dev         # frontend on :5173
```

Swagger UI: `http://localhost:5000/docs` – admin@internops.com / Admin@123

## Environment

`DATABASE_URL`, `JWT_SECRET`, `PORT`, `NODE_ENV`, `CORS_ORIGIN`, `UPSTASH_REDIS_REST_URL`, `UPTOSKILLS_BASE_URL`, `UPTOSKILLS_API_KEYc

## Deployment

```bash
NODE_ENV=production npm start
pm2 start backend/src/app.js --name internops   # with PM2 + Nginx
```

## License

Proprietary. All rights reserved.

## Maintainer

**Rajat Wyrm** – [GitHub](https://github.com/rajat-wyrm)