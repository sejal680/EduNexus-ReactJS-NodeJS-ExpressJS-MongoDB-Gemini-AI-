# EduNexus — AI-Powered E-Learning Platform

**EduNexus** is a starter full-stack project showcasing an AI-enhanced e-learning platform using React, Node/Express, MongoDB and Google Gemini models.

## Features
- AI-driven quiz & summary generation (Gemini integration)
- Personalized course recommendations (starter patterns)
- Instructor dashboards with engagement stats (starter)
- Scalable backend patterns (optimized queries, pagination, `lean()` responses)

## Tech stack
- Frontend: React (Vite)
- Backend: Node.js, Express
- Database: MongoDB (Mongoose)
- AI: Google Gemini (server-side REST integration)
- Dev & deployment: Docker, docker-compose

---

## Quickstart — Local (development)

1. Unzip the project and `cd` into the project folder:
   ```bash
   unzip EduNexus_Fullstack_Project_updated.zip -d edunexus && cd edunexus
   ```
2. Server: copy example env and install dependencies
   ```bash
   cd server
   cp .env.example .env
   # Edit .env and set GOOGLE_API_KEY and MONGO_URI if needed
   npm install
   npm run dev
   ```
3. Client: install and run
   ```bash
   cd ../client
   npm install
   npm run dev
   ```
4. Open the client (usually at http://localhost:5173) and the server at http://localhost:4000.

## Quickstart — Docker (single command)
```bash
docker-compose up --build
```
This will run `mongo`, `server`, and `client` containers defined in the included `docker-compose.yml`.

---

## Gemini AI integration
- The server uses a small wrapper (`server/src/services/geminiClient.js`) that calls the Google Generative Language REST endpoint (example pattern: `models/<MODEL>:generateContent`).
- Add your Gemini / Google API key to `server/.env` as `GOOGLE_API_KEY`. **Keep the key server-side only** — do not embed in client bundles.
- For production-grade usage consider Vertex AI, proper key rotation, rate limiting and monitoring.

---

## Important files & folders
- `server/` — Express app, routes, Mongoose models, Gemini client wrapper.
  - `server/src/routes/gemini.js` — endpoints to generate quizzes and summaries.
  - `server/src/services/geminiClient.js` — example server-side call to Gemini.
  - `server/.env.example` — environment variables (copy to `.env`).
- `client/` — React (Vite) app with a simple `QuizGenerator` component that calls the server.
- `docker-compose.yml` — local development compose that brings up Mongo, server, client.

---

## Performance & scaling notes
- Index frequently queried fields (e.g. `Course.tags`, `Course.instructor`).
- Use `.lean()` on read-only Mongoose queries to reduce memory overhead.
- Parallelize count & page queries with `Promise.all` (example included).
- Cache heavy / repeated Gemini responses with Redis; offload heavy AI tasks to background workers.
- Add API-level rate limits and autoscaling policies for the Node service.
- Monitor with Prometheus + Grafana for production readiness.

---

## TODOs / Suggested improvements
- Add authentication (JWT flows, password reset).
- Add Redis caching and background workers for heavy AI tasks.
- Add unit & integration tests and CI pipeline (GitHub Actions).
- Add an instructor analytics microservice for aggregated metrics.
- Harden Gemini integration: streaming, retry/backoff, and usage logging.

---

## License
MIT

---

## Notes
If anything else is missing (example: full auth skeleton, CI config, or a sample `.env` for Mongo running locally), tell me what you want and I’ll add it to the repo and rezip for you.
