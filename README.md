# Blog App (Dockerized)

React frontend + Express/TypeScript/Prisma backend + PostgreSQL database.

## Project Structure
- frontend/  → React app (Vite), has its own Dockerfile
- backend/   → Express + Prisma API, has its own Dockerfile
- database/  → PostgreSQL image, has its own Dockerfile
- compose.yaml → ties the three services together

## Services
| Service  | Port | Role |
|----------|------|------|
| frontend | 4173 | Serves the built React app |
| backend  | 5000 | REST API, runs Prisma migrations on start |
| database | 5432 | PostgreSQL, data stored in a named volume |

## How to Run
1. Copy `.env.example` to `.env` and fill in the values.
2. Make sure Docker Desktop is running.
3. From the folder containing compose.yaml:

   docker compose up --build

4. Open http://localhost:4173

## Docker Concepts Used
- Dockerfile per service
- Named volume `postgres_data`: keeps DB data after `docker compose down`
- Bind mount `./backend/uploads:/app/uploads`: shares files between host and container
- healthcheck + depends_on (service_healthy): backend waits for the DB to be ready
- build args: pass VITE_BACKEND_SERVER_PROD to the frontend at build time
- .env: secrets stay out of Git

## Stopping
docker compose down        (keeps data)
docker compose down -v     (also deletes the database volume)