# Kinesis

Video upload + async transcoding pipeline with `backend` (API), `worker` (queue processor), and `frontend` (UI).

Refer to [architecture.jpeg](./architecture.jpeg) for architecture.

## Requirements

- Node.js 18+
- Bun
- Docker + Docker Compose
- AWS S3 credentials

## Environment

Create these files first:

```bash
cp backend/.env.example backend/.env
cp worker/.env.example worker/.env
```

Required values:

- `DATABASE_URL`
- `REDIS_URL`
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY`
- `AWS_REGION`
- `S3_BUCKET`

## Run Locally

Start services in separate terminals.

1) Worker dependencies + worker container

```bash
cd worker
docker compose up -d --build
```

2) Backend (`:8000`)

```bash
cd backend
bun install
bun dev
```

3) Frontend (`:3000`)

```bash
cd frontend
npm install
npm run dev
```

Open `http://localhost:3000`.

## Notes

- Worker runs FFmpeg inside the worker container (no Docker socket mount).
- Processed files and original upload are deleted from S3 after 1 hour.
- Download links endpoint: `GET /api/v1/videos/:videoId/downloads`


