# plan-engine

`plan-engine` is the core agent workflow module of the Routine‑Ops system. It ingests structured nutrition and routine plans, orchestrates task‑specific agents (skeleton chains, variant chains, ingredient tools, scheduling agents, etc.), and emits a unified DSL representation that can be stored, queried, or rendered by downstream services (UI, notifications, reports).

---

## Key Features

* **Agent Orchestration**: Coordinates multiple LangChain/ADK agents to parse, validate, expand, and store user plans.
* **DSL Generation**: Produces a machine‑readable DSL describing daily/weekly/monthly routines, ingredient lists, and time‑based checklists.
* **Persistence**: Saves DSL outputs to a PostgreSQL database for backend querying and history tracking.
* **Extensible Tools**: Pluggable ingredient list generator, schedule optimizer, nutritional analysis, and notification scheduler.
* **API Endpoints**: Exposes a FastAPI service for plan submission, status polling, and result retrieval.

---

## Architecture Overview

```
+--------------+        +----------------+        +--------------+
|  Input Layer |  --->  | Agent Orchestrator |  --->  | Persistence  |
| (JSON, PDF,  |        | (LangChain / ADK)  |        | (PostgreSQL) |
|  UI, API)    |        +----------------+        +--------------+
+--------------+                 |
                                 v
                           +-------------+
                           | DSL Output  |
                           +-------------+
```

1. **Input Layer**: Accepts raw plans via REST, file upload, or direct JSON payload.
2. **Agent Orchestrator**: Core workflow using LangChain (chains & agents) or Google’s ADK:

   * **Skeleton Chain**: High‑level plan structure (monthly, weekly, daily slots).
   * **Variant Chain**: Meal variants, ingredients, substitutions.
   * **Ingredient Tool**: Generates weekly and daily ingredient lists.
   * **Scheduler Agent**: Converts timings into calendar events or notifications.
3. **Persistence**: Uses SQLAlchemy + Alembic to store DSL and metadata in PostgreSQL.
4. **API Layer**: FastAPI endpoints for submission (`POST /plans`), status (`GET /plans/{id}/status`), and retrieval (`GET /plans/{id}`).

---

## Tech Stack

* **Language**: Python 3.10+
* **Frameworks**: LangChain (or Google ADK), FastAPI
* **Database**: PostgreSQL (via SQLAlchemy + Alembic)
* **Task Queue**: Celery + Redis (for long‑running plan processing)
* **Dependency Management**: Poetry (recommended) or pip + venv
* **Containerization**: Docker + docker‑compose
* **CI/CD**: GitHub Actions

---

## Getting Started

### Prerequisites

* Python 3.10+
* PostgreSQL 14+
* Redis
* Docker & Docker Compose (for local dev)

### Clone the Repository

```bash
git clone https://github.com/your-org/plan-engine.git
cd plan-engine
```

### Install Dependencies

Using Poetry (recommended):

```bash
poetry install
poetry shell
```

Or using pip:

```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### Configure Environment

Copy `.env.example` to `.env` and set:

```ini
DATABASE_URL=postgresql://user:pass@localhost:5432/plan_engine
REDIS_URL=redis://localhost:6379/0
SECRET_KEY=your-secret-key
```

### Database Setup

```bash
alembic upgrade head
```

### Running Locally

Start Redis, Postgres (via Docker Compose):

```bash
docker-compose up -d
```

Launch Celery worker:

```bash
celery -A plan_engine.worker worker --loglevel=info
```

Start FastAPI server:

```bash
uvicorn plan_engine.app:app --reload
```

Open docs at [http://localhost:8000/docs](http://localhost:8000/docs)

---

## Project Structure

```
plan-engine/
├── plan_engine/          # Main Python package
│   ├── agents/           # LangChain / ADK agent definitions
│   ├── api/              # FastAPI routes & schemas
│   ├── core/             # Orchestrator, chains, tools
│   ├── db/               # SQLAlchemy models & migrations
│   ├── worker.py         # Celery worker entrypoint
│   └── app.py            # FastAPI application entrypoint
├── tests/                # Unit & integration tests
├── docker-compose.yml    # Local dev stack
├── Dockerfile            # Service container image
├── alembic.ini           # DB migrations config
├── .env.example          # Sample environment variables
├── pyproject.toml        # Poetry config
└── README.md
```

---

## Contributing

1. Fork the repo & create a feature branch
2. Run tests: `pytest --maxfail=1 --disable-warnings -q`
3. Commit & open a PR against `main` branch

Please follow our [Code of Conduct](CODE_OF_CONDUCT.md) and [Contributing Guide](CONTRIBUTING.md).

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
