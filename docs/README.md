# Quasar + Express Full-Stack Demo

A full-stack application with Quasar (Vue 3) frontend and Express backend, orchestrated with Docker Compose.

## Project Structure

- `frontend/`: Quasar SPA
- `backend/`: Express API
- `docker-compose.yml`: Solution orchestration

## Getting Started

### Prerequisites

- Node.js (v18+)
- Docker & Docker Compose

### Run Locally (Development)

1. **Backend**:
   ```bash
   cd backend
   npm install
   node server.js
   ```
   Server runs at `http://localhost:3000`.

2. **Frontend**:
   ```bash
   cd frontend
   npm install
   npm run dev
   ```
   App runs at `http://localhost:9000` (or similar).

### Run with Docker

Build and run both services:

```bash
docker compose up --build -d
```

- Frontend: [http://localhost:8080](http://localhost:8080)
- Backend: [http://localhost:3000/api/demo](http://localhost:3000/api/demo)

## Features

- **Frontend**: API integration using Axios, Quasar UI components.
- **Backend**: Express REST API, CORS support, file logging (`logs/access.log`), health checks.
- **Docker**: Multi-stage builds, volume persistence, health monitoring.
