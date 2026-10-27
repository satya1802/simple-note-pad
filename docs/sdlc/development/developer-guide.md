# Developer Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start status -->
_Up to date._
<!-- sdlc:auto:end status -->

<!-- sdlc:auto:start source -->
Generated from commit `6b3b0dd` · model `claude-sonnet-5`
<!-- sdlc:auto:end source -->

<!-- sdlc:auto:start overview -->
Simple note pad is a Quorq-generated project containing two independently run apps in one repo: a Vite + React 19 SPA (frontend/) whose screens were already reviewed and approved, currently rendering seeded sample data rather than calling a real API; and a FastAPI 0.115 backend (backend/) that has no approved architecture yet, so it only exposes a health check and a SQLAlchemy/Pydantic scaffold ready for real routes, models and schemas to be added. The backend defaults to a local SQLite file so it runs with no database server, though a Postgres 16 container is provided via docker-compose for the eventually-approved stack.
<!-- sdlc:auto:end overview -->

<!-- sdlc:auto:start prerequisites -->
- Node.js (for Vite 6 / React 19 frontend tooling)
- Python 3.12
- Docker and Docker Compose (optional, for the Postgres 16 service)
<!-- sdlc:auto:end prerequisites -->

<!-- sdlc:auto:start setup -->
1. Copy .env.example to .env and fill in values as needed
2. cd backend && pip install -r requirements.txt
3. uvicorn app.main:app --reload   # starts the API on http://localhost:8000
4. cd frontend && npm install
5. npm run dev   # starts the Vite dev server (default http://localhost:5173)
6. Optional: from the repo root, docker-compose up -d to start the Postgres 16 database, then set DATABASE_URL to point the backend at it
<!-- sdlc:auto:end setup -->

<!-- sdlc:auto:start run -->
| Name | Command | Description |
|---|---|---|
| backend dev | `uvicorn app.main:app --reload` | Runs the FastAPI app with auto-reload from backend/ |
| frontend dev | `npm run dev` | Starts the Vite dev server for the React SPA from frontend/ |
| frontend build | `npm run build` | Bundles the SPA with Vite (does not typecheck) |
| frontend preview | `npm run preview` | Serves the production build locally |
| db up | `docker-compose up -d` | Starts the Postgres 16 service defined in docker-compose.yml |
<!-- sdlc:auto:end run -->

<!-- sdlc:auto:start structure -->
| Path | Purpose |
|---|---|
| `backend/app` | FastAPI application: main.py entrypoint, database.py (engine/session), models.py (SQLAlchemy Base, currently empty), schemas.py (Pydantic stub response), routers/ (empty, one router per future component) |
| `backend/tests` | Pytest suite; currently just the health check test |
| `frontend/src` | React SPA source: lib/api.ts (API client), lib/ui.tsx and lib/icons.tsx (shared component/icon vocabulary), main.tsx entrypoint, index.css |
| `frontend/e2e` | Playwright end-to-end specs (e.g. example.spec.ts) |
| `.quorq` | Platform metadata (handoff.json) used by the Quorq SDLC tooling |
<!-- sdlc:auto:end structure -->

<!-- sdlc:auto:start conventions -->
- Backend follows one router per approved architecture component, one route per spec'd endpoint; unimplemented routes return a typed StubResponse rather than raising, keeping the OpenAPI doc complete
- SQLAlchemy models all inherit from the shared Base in app/database.py; main.py imports models before calling Base.metadata.create_all so no migration tooling is needed yet
- Backend config (DATABASE_URL, ALLOWED_ORIGINS) is read via os.getenv with safe local defaults (SQLite, localhost CORS origins)
- Frontend reads backend location/secret via Vite env vars VITE_API_BASE_URL and VITE_API_SECRET_KEY, consumed through the single apiFetch helper in src/lib/api.ts
- Generated screens currently render seeded sample data and have not yet been wired to apiFetch/the backend
- Frontend uses ESLint + Prettier for style/lint and Tailwind CSS (via @tailwindcss/vite) for styling
- Backend uses ruff for linting/formatting
<!-- sdlc:auto:end conventions -->

<!-- sdlc:auto:start testing -->
| Name | Command | Description |
|---|---|---|
| backend tests | `pytest` | Runs the backend test suite from backend/ (pythonpath=. so `import app` resolves) |
| backend lint | `ruff check .` | Lints the backend code |
| backend format | `ruff format .` | Formats the backend code |
| frontend unit tests | `npm test` | Runs Vitest component tests under src/ with jsdom |
| frontend lint | `npm run lint` | Runs ESLint over the whole frontend app |
| frontend format check | `npm run format:check` | Checks formatting with Prettier |
| frontend typecheck | `npm run typecheck` | Runs tsc --noEmit (not run by build) |
| e2e install | `npm run test:e2e:install` | Installs the Chromium browser Playwright needs |
| e2e tests | `npm run test:e2e` | Runs Playwright specs in e2e/; without E2E_BASE_URL it boots the backend (pip install + uvicorn) and the built/previewed frontend itself |
<!-- sdlc:auto:end testing -->

<!-- sdlc:auto:start troubleshooting -->
| Problem | Solution |
|---|---|
| Frontend calls to the backend are blocked by CORS | Set ALLOWED_ORIGINS on the backend (comma-separated) to include the frontend's origin; defaults only allow http://localhost:5173 and http://127.0.0.1:5173 |
| `npm run build` succeeds but deployment/typecheck fails | Run `npm run typecheck` (tsc --noEmit) separately, since `vite build` does not typecheck |
| Playwright e2e tests hang or fail to start a browser | Run `npm run test:e2e:install` first to fetch Chromium, and ensure the backend's requirements install cleanly since the e2e webServer runs `pip install -q -r requirements.txt` before starting uvicorn |
| Backend can't connect to Postgres | Start it with `docker-compose up -d` and set DATABASE_URL (e.g. postgresql+psycopg://app:app@localhost:5432/app); otherwise the backend falls back to a local sqlite:///./app.db file |
<!-- sdlc:auto:end troubleshooting -->
