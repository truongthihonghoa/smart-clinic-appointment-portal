# Smart Clinic Appointment Portal

This repository follows the required monorepo structure for the clinic appointment system.

## Structure

- `frontend/` for the web client
- `backend/` for the API and business logic
- `vault/` for planning, research, and product artifacts
- `docs/` for product and engineering documentation
- `.github/workflows/` for CI/CD automation

## Local setup

1. Copy `.env.example` to `.env` and update secrets.
2. Start services with Docker Compose:
   ```bash
   docker compose up --build
   ```
3. Run the frontend and backend with their local development commands.

## Security

Never commit real API keys, database credentials, or GitHub tokens.
