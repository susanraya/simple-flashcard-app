# Developer Guide

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start status -->
_Up to date._
<!-- sdlc:auto:end status -->

<!-- sdlc:auto:start source -->
Generated from commit `789ae06` · model `claude-sonnet-5`
<!-- sdlc:auto:end source -->

<!-- sdlc:auto:start overview -->
This is a generated scaffold for a simple flashcard app, built as two independent applications in one repo. The frontend is a Vite + React 19 single-page app (TypeScript, Tailwind CSS, React Router) whose screens were approved from a design and currently render seeded sample data rather than calling a real API. The backend is a FastAPI service with SQLAlchemy models and Pydantic schemas; no architecture had been approved yet, so it currently exposes only a `/health` endpoint and a `StubResponse` shape for future routes. The backend defaults to a local SQLite file so it runs with no external database, while a docker-compose file provisions a Postgres container for when `DATABASE_URL` is pointed at it.
<!-- sdlc:auto:end overview -->

<!-- sdlc:auto:start prerequisites -->
- Node.js (for npm/Vite/React 19 toolchain)
- Python 3.12
- pip
- Docker and docker-compose (optional, for the Postgres service)
<!-- sdlc:auto:end prerequisites -->

<!-- sdlc:auto:start setup -->
1. Clone the repository
2. cd frontend && npm install
3. cd backend && pip install -r requirements.txt
4. (Optional) Copy .env.example to .env and set DATABASE_URL, ALLOWED_ORIGINS, VITE_API_BASE_URL, VITE_API_SECRET_KEY as needed
5. (Optional) docker-compose up db -- to run Postgres locally instead of the default SQLite file
6. Start the backend: cd backend && uvicorn app.main:app --reload
7. Start the frontend: cd frontend && npm run dev
<!-- sdlc:auto:end setup -->

<!-- sdlc:auto:start run -->
| Name | Command | Description |
|---|---|---|
| frontend dev | `npm run dev` | Starts the Vite dev server for the React SPA (run from frontend/) |
| frontend build | `npm run build` | Bundles the frontend for production; does not typecheck (run from frontend/) |
| frontend preview | `npm run preview` | Serves the production build locally (run from frontend/) |
| frontend typecheck | `npm run typecheck` | Runs tsc --noEmit to catch type errors not caught by the build (run from frontend/) |
| backend dev | `uvicorn app.main:app --reload` | Runs the FastAPI service with auto-reload (run from backend/) |
| backend docker build | `docker build -t flashcard-backend .` | Builds the backend container image (run from backend/, uses backend/Dockerfile) |
| db up | `docker-compose up db` | Starts the Postgres 16 container defined in docker-compose.yml |
<!-- sdlc:auto:end run -->

<!-- sdlc:auto:start structure -->
| Path | Purpose |
|---|---|
| `frontend/` | Vite + React SPA with approved screens, running on seeded sample data |
| `frontend/src` | Application source: main.tsx entry, lib/ (api client, UI/icon vocabulary, navigation), styles |
| `frontend/e2e` | Playwright end-to-end acceptance test specs |
| `backend/` | FastAPI service scaffold |
| `backend/app` | Application code: main.py entrypoint/health route, database.py (engine/session), models.py (SQLAlchemy models), schemas.py (Pydantic models), routers/ (per-component routers) |
| `backend/tests` | Pytest tests, currently covering the health check |
| `.quorq/` | Platform handoff metadata (handoff.json) for the Quorq AI SDLC platform |
<!-- sdlc:auto:end structure -->

<!-- sdlc:auto:start conventions -->
- Backend: one router per architecture component that owns endpoints, one route per spec'd endpoint
- Unimplemented backend routes return a typed StubResponse (status='not_implemented') rather than failing, keeping the service startable and OpenAPI complete
- SQLAlchemy models inherit from the shared Base in app/database.py; models.py is imported in main.py before create_all so tables register
- Backend uses a request-scoped DB session via the get_db dependency, closed in a finally block
- Frontend component tests (Vitest) live beside the components they cover under src/
- Playwright e2e specs live in frontend/e2e/, separate from Vitest's src/**/*.test.* scope
- Frontend API access is centralized in src/lib/api.ts (apiFetch), reading VITE_API_BASE_URL / VITE_API_SECRET_KEY at build time
- CORS origins are configured via the ALLOWED_ORIGINS env var, defaulting to the local Vite dev server origins
- Ruff is used for backend linting/formatting; ESLint + Prettier for the frontend
<!-- sdlc:auto:end conventions -->

<!-- sdlc:auto:start testing -->
| Name | Command | Description |
|---|---|---|
| frontend unit tests | `npm run test` | Runs Vitest component tests (run from frontend/) |
| frontend e2e tests | `npm run test:e2e` | Runs Playwright acceptance tests from e2e/; builds/serves the app and boots the backend locally unless E2E_BASE_URL is set (run from frontend/) |
| install e2e browser | `npm run test:e2e:install` | Installs the Chromium browser Playwright needs (run from frontend/) |
| frontend lint | `npm run lint` | Runs ESLint over the frontend app; used as a gate during development (run from frontend/) |
| backend tests | `pytest` | Runs backend tests (run from backend/, requires pytest.ini's pythonpath=. to import app) |
| backend lint | `ruff check .` | Lints the backend code (run from backend/) |
<!-- sdlc:auto:end testing -->

<!-- sdlc:auto:start troubleshooting -->
| Problem | Solution |
|---|---|
| Frontend calls to the API fail with CORS errors | Ensure the backend's ALLOWED_ORIGINS env var includes the frontend's origin, or rely on the default dev origins (http://localhost:5173) |
| `pytest` fails with ImportError for `app` | Run pytest from the backend/ directory so pytest.ini's `pythonpath = .` takes effect |
| Playwright e2e tests fail to start the backend | The config expects backend/.venv/bin/python with dependencies installed; create that venv and install backend/requirements.txt before running npm run test:e2e locally, or set E2E_BASE_URL to point at a running deployment |
| Frontend screens don't reflect real backend data | This is expected: approved screens currently render seeded sample data, not live API calls; wiring a screen to apiFetch in src/lib/api.ts is the next step |
| `npm run build` succeeds but deployment fails on type errors | Run `npm run typecheck` (tsc --noEmit) separately, since build does not typecheck |
<!-- sdlc:auto:end troubleshooting -->
