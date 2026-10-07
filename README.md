# AVRIXON V14 — Render Ready

This repository is prepared for deployment on Render using Docker.

## GitHub → Render

1. Upload **all files in this folder** to a new GitHub repository. Do not upload `.env` or any SQLite database file.
2. In Render, choose **New → Blueprint** and select the GitHub repository.
3. Render reads `render.yaml` automatically.
4. Enter values when prompted for:
   - `ADMIN_EMAIL` — the email you will use for the AVRIXON admin login.
   - `ADMIN_PASSWORD` — a strong admin password.
5. Deploy.

Render automatically generates `JWT_SECRET`.

## Important: database persistence

The service uses SQLite and `render.yaml` attaches a 1 GB persistent disk at `/var/lib/avrixon`. The app stores the database at `/var/lib/avrixon/avrixon.db`.

The Blueprint uses the Render **Starter** web-service plan because persistent disks are required for this SQLite deployment. Do not remove the disk unless you intentionally move the database to another persistent database service.

## Public routes

- `/` — public site
- `/admin` — admin panel
- `/advertiser` — advertiser panel
- `/privacy.html` — privacy page
- `/terms.html` — terms page
- `/support.html` — support page
- `/refund.html` — refund page
- `/api/health` — health check

## Local run

```bash
npm install
npm start
```

For production-like local testing, set `NODE_ENV`, `JWT_SECRET`, `ADMIN_EMAIL`, and `ADMIN_PASSWORD` in `.env` first.

## Security notes

- Never commit `.env`, passwords, JWT secrets, or SQLite database files.
- Use a unique strong admin password.
- Keep the Render persistent disk attached.
