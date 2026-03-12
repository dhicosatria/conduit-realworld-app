# Conduit RealWorld App (Monolith)

This branch contains the monolith version of the project:
- Frontend: React + Vite
- Backend: Express + Sequelize
- Database: PostgreSQL

## Runtime Modes

- Development:
  - `npm run dev`
  - Frontend: `:3000`
  - API: `:3001`

- Production (single port):
  - `npm run start`
  - Frontend + API served by backend on `:3001`

## Branch Plan

- `main`: monolith version (current)
- `microservice`: upcoming microservice version

Create the next branch later with:

```bash
git checkout -b microservice
```

## Quick Start

```bash
npm install
npm run dev
```

