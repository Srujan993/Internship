# Email Digest Service - Quick Runbook

## What This App Does

This project is an admin-style Email Digest Service with:

- JWT authentication (register/login)
- Email log management (create, update, soft delete, detail view)
- Search, filters, pagination, and analytics
- CSV export and CSV upload
- Audit logging for create/update/delete operations
- Swagger/OpenAPI documentation

Tech stack:

- Backend: Spring Boot (Java 17), PostgreSQL, Flyway
- Frontend: React + Vite
- Infra: Docker Compose

---

## Local URLs

- Frontend UI: `http://localhost:5173`
- Backend API: `http://localhost:8080`
- Swagger UI: `http://localhost:8080/swagger-ui/index.html`
- OpenAPI JSON: `http://localhost:8080/v3/api-docs`

Note: opening `http://localhost:8080` directly may show `403` (expected for secured API root).

---

## How To Run
BACKEND----
From project root:

```powershell
docker compose up --build
```

If you ever hit DB compatibility/state issues, reset and rebuild:

```powershell
docker compose down -v
docker compose up --build
```

---
FRONTEND---
front frontend directory:
```powershell
1.cd frontend
2.npm install
3.npx vite --host 0.0.0.0 --port 5173
```


## 3-5 Minute Demo Flow

1. Open `http://localhost:5173`
2. Register a new user, then login
3. Dashboard: show KPI cards and charts
4. List page: show search/filter/pagination
5. Create a new email log
6. Open detail page, update the record
7. Soft delete the record
8. Export CSV, then upload CSV
9. Open Swagger and show documented endpoints

---

## Core API Endpoints

Auth:

- `POST /api/users/register`
- `POST /api/users/login`

Email logs:

- `GET /api/email/logs/all`
- `GET /api/email/logs/{id}`
- `POST /api/email/logs/create`
- `PUT /api/email/logs/{id}`
- `DELETE /api/email/logs/{id}`
- `GET /api/email/logs/search?q=...`
- `GET /api/email/logs/stats`
- `GET /api/email/logs/export`
- `POST /api/email/logs/upload`

---

## Troubleshooting

- Frontend works, backend `403` at root:
  - Expected behavior for secured API root.
  - Use `http://localhost:5173` for UI and Swagger URL for docs.
- Registration/login fails with connection refused:
  - Backend is not running; check `docker compose ps`.
- If containers are up but behavior looks stale:
  - Run `docker compose down -v` then `docker compose up --build`.
