# ZepCode — Vercel + Ubuntu 22.04

## Architecture
- `frontend/`: VS Code-style UI, deploy this folder to Vercel.
- `backend/`: Docker Ubuntu 22.04 runtime with a real WebSocket terminal.
- The container shell runs as **root** by default.

## 1. Backend
On a Docker-capable VPS/server:

```bash
cd backend
docker build -t zepcode .
docker run -d --name zepcode -p 8080:8080 -e ZEPVM_PASSWORD='CHANGE_THIS_LONG_PASSWORD' zepcode
```

The backend exposes:
`/health`

Do not expose a root shell publicly without authentication and network restrictions.

## 2. Frontend on Vercel
Import `frontend/` as the Vercel project.

Build:
`npm run build`

Output:
`dist`

Environment variable:
`VITE_API_URL=https://YOUR-BACKEND-DOMAIN`

Then redeploy.

## 3. Local full test
From the project root:

```bash
docker compose up -d --build
```

The Ubuntu container persists `/workspace` in a Docker volume.

## Important
Vercel itself does not provide a persistent Ubuntu container. Vercel hosts the frontend; the Ubuntu 22.04 Docker backend must run on a VPS/container host.
