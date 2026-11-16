# Dead by Daylight Character Directory API

FastAPI service backed by a Supabase (Postgres) database.

## Setup

1. In Supabase, open the SQL Editor and run `supabase/schema.sql`, then `supabase/seed.sql`.
2. Copy `.env.example` to `.env` and fill in the values. `.env` is ignored by Git.
3. Install and run:

```
pip install -r requirements.txt
uvicorn api.index:app --reload
```

Docs are at `http://127.0.0.1:8000/docs`.

## Environment variables

| Name | Purpose |
|---|---|
| `SUPABASE_URL` | Project URL |
| `SUPABASE_SERVICE_KEY` | service_role key, server-side only |
| `API_KEY` | Read key, sent as `x-api-key` (the web apps use this) |
| `ADMIN_API_KEY` | Write key, sent as `x-admin-key` for POST, PATCH, DELETE |

On Vercel, add the same four under Project Settings > Environment Variables.

## Endpoints

| Method | Path | Key | Purpose |
|---|---|---|---|
| GET | `/health` | none | API is running |
| GET | `/health/db` | read | Runs a real query against Supabase |
| GET | `/api/v1/` | none | Welcome and counts |
| GET | `/api/v1/characters` | read | List with role filter, sort, paging |
| GET | `/api/v1/characters/search?q=` | read | Keyword search |
| GET | `/api/v1/characters/{id}` | read | One character |
| POST | `/api/v1/characters` | admin | Create |
| PATCH | `/api/v1/characters/{id}` | admin | Partial update |
| DELETE | `/api/v1/characters/{id}` | admin | Delete |
