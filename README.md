# Simple Todo Application (React + Express)

This repository is organized as two separate workspaces:

- `simple-todo-application-245386-245400/todo_frontend`: React frontend (runs on port 3000)
- `simple-todo-application-245386-245401/backend`: Express backend (runs on port 3001)

The containers are expected to be started automatically by the preview system, so you typically do not need to manually start processes to preview the app.

## Features (current state)

Based on the current source code:

The frontend currently renders a basic React page with a light/dark theme toggle. The todo functionality described in the work item (add tasks, complete, delete, filter, localStorage persistence, retro UI) is not implemented yet in the checked-in frontend code.

The backend currently provides a health endpoint and Swagger UI documentation. It does not yet provide todo CRUD endpoints.

## Running / Preview

The environment this project is designed for provides URLs for the running containers:

- Frontend (React): `https://vscode-internal-41221-qa.qa01.cloud.kavia.ai:3000`
- Backend (Express Swagger UI): `https://vscode-internal-41221-qa.qa01.cloud.kavia.ai:3001/docs`
- Backend OpenAPI JSON: `https://vscode-internal-41221-qa.qa01.cloud.kavia.ai:3001/openapi.json`

If you are using the same preview system, the containers will start automatically and you can open the frontend URL directly.

## Local development (manual)

If you are running locally outside the managed preview environment, you can install dependencies and run each workspace separately.

### Prerequisites

- Node.js (LTS recommended)
- npm

### Frontend (React)

```bash
cd simple-todo-application-245386-245400/todo_frontend
npm install
npm start
```

The React dev server will start on port 3000 by default.

### Backend (Express)

```bash
cd simple-todo-application-245386-245401/backend
npm install
npm run dev
```

By default the backend listens on `0.0.0.0` and uses `PORT` from the environment (see `src/server.js`). In the managed environment it is exposed on port 3001.

## Environment variables

The container environment lists the following variables (typically provided via a `.env` in the runtime environment). Not all of these are necessarily used by the current code, but they are part of the runtime configuration surface.

### Frontend (React) env vars

React only exposes variables prefixed with `REACT_APP_` to the browser build.

- `REACT_APP_API_BASE`: Base URL for API calls from the frontend.
- `REACT_APP_BACKEND_URL`: Backend service URL.
- `REACT_APP_FRONTEND_URL`: Frontend service URL.
- `REACT_APP_WS_URL`: WebSocket URL (if used).
- `REACT_APP_NODE_ENV`: Runtime environment name (development/production).
- `REACT_APP_NEXT_TELEMETRY_DISABLED`: Telemetry toggle (if applicable in the environment).
- `REACT_APP_ENABLE_SOURCE_MAPS`: Toggle source map generation.
- `REACT_APP_PORT`: Port used by the frontend runtime (environment-specific).
- `REACT_APP_TRUST_PROXY`: Proxy trust configuration (environment-specific).
- `REACT_APP_LOG_LEVEL`: Logging verbosity.
- `REACT_APP_HEALTHCHECK_PATH`: Health check route path (environment-specific).
- `REACT_APP_FEATURE_FLAGS`: Feature flag configuration (string-encoded).
- `REACT_APP_EXPERIMENTS_ENABLED`: Toggle experimental features.

### Backend env vars

The backend code uses standard Node env vars (not `REACT_APP_*`), notably:

- `PORT`: Port for the Express server (defaults to `3000` in `backend/src/server.js`).
- `HOST`: Host interface (defaults to `0.0.0.0`).
- `NODE_ENV`: Reported by the health endpoint response (defaults to `development`).

## API

### Health endpoint

- `GET /`: Returns a JSON payload describing service status.

### Swagger UI

- `GET /docs`: Swagger UI (the server dynamically sets the OpenAPI server URL based on the incoming request host/protocol).

## Project structure

- `simple-todo-application-245386-245400/todo_frontend/src`: React source (`App.js` currently implements a theme toggle demo).
- `simple-todo-application-245386-245401/backend/src`: Express application, routes, controllers, services.
- `simple-todo-application-245386-245401/backend/interfaces/openapi.json`: Generated OpenAPI spec snapshot.
- `simple-todo-application-245386-245401/backend/swagger.js`: Swagger spec generator configuration.

## Notes

If you are looking for the actual todo app behavior described in the work item (task add/complete/delete/filter with localStorage persistence and a retro theme UI), those features will need to be implemented in the frontend (and optionally in the backend if persistence should move server-side). This README intentionally describes what is currently present in the repository so it stays accurate.
