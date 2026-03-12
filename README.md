# Conduit RealWorld Example App (Monolith)

Fullstack RealWorld Conduit implementation using:
- React + Vite (frontend)
- Express + Sequelize (backend)
- PostgreSQL (database)

This repository is the **monolith baseline** branch. A future `microservice` branch can be created from this stable base.

## Architecture

- `frontend/`: React SPA
- `backend/`: REST API, auth, articles, comments, profiles, tags
- Root workspace: runs frontend and backend together during development

## Features

- User authentication (JWT)
- Article CRUD
- Comments
- Favorites
- Follow profiles
- Tag feed and pagination

## Tech Stack

- Node.js (18+ recommended)
- npm workspaces
- React 19
- Vite 7
- Express 5
- Sequelize 6
- PostgreSQL
- Vitest

## Project Structure

```text
.
├── backend
│   ├── config
│   ├── controllers
│   ├── models
│   ├── routes
│   └── index.js
├── frontend
│   ├── src
│   ├── public
│   └── vite.config.js
├── package.json
└── .env
```

## Prerequisites

- Git
- Node.js and npm
- PostgreSQL server running

## Environment Variables

Create `.env` at project root.

```env
PORT=3001
JWT_KEY=your_secret_key

# Development DB
DEV_DB_USERNAME=postgres
DEV_DB_PASSWORD=postgres
DEV_DB_NAME=database_development
DEV_DB_HOSTNAME=127.0.0.1
DEV_DB_DIALECT=postgres
DEV_DB_LOGGING=true

# Test DB
TEST_DB_USERNAME=postgres
TEST_DB_PASSWORD=postgres
TEST_DB_NAME=database_testing
TEST_DB_HOSTNAME=127.0.0.1
TEST_DB_DIALECT=postgres
TEST_DB_LOGGING=true

# Production DB
PROD_DB_USERNAME=postgres
PROD_DB_PASSWORD=postgres
PROD_DB_NAME=database_production
PROD_DB_HOSTNAME=127.0.0.1
PROD_DB_DIALECT=postgres
PROD_DB_LOGGING=false
```

## Install

```bash
npm install
```

## Database Setup

Create databases:

```bash
npm run sqlz -- db:create
```

Run migrations/seeders if needed:

```bash
npm run sqlz -- db:migrate
npm run sqlz -- db:seed:all
```

## Run Modes

### Development (2 ports)

```bash
npm run dev
```

- Frontend: `http://<VM_IP>:3000`
- API: `http://<VM_IP>:3001/api`

### Production (single port)

```bash
npm run start
```

What this does:
1. Builds frontend (`frontend/dist`)
2. Runs backend with `NODE_ENV=production`
3. Serves SPA + API from one port (`3001`)

- App: `http://<VM_IP>:3001`
- API: `http://<VM_IP>:3001/api`

## Environment Switching Logic

- `development`: default when `NODE_ENV` is unset (used by `npm run dev`)
- `production`: explicitly set by backend start script
- `test`: used when `NODE_ENV=test`

Database selection follows `NODE_ENV`:
- development -> `DEV_DB_*`
- test -> `TEST_DB_*`
- production -> `PROD_DB_*`

## VM Networking Notes (Bridged)

- Access from host must use VM IP, not `localhost`
- Ensure firewall allows required port(s):
  - Dev: `3000`, `3001`
  - Production single-port: `3001`

Example:

```bash
sudo ufw allow 3001
```

## Testing

```bash
npm test
```

## Branch Strategy

- `main`: monolith (this branch)
- `microservice`: create later for service-split architecture

Create future branch:

```bash
git checkout -b microservice
git push -u origin microservice
```

## API Reference

RealWorld API spec:
- https://realworld-docs.netlify.app/docs/specs/backend-specs/endpoints

## License

MIT

