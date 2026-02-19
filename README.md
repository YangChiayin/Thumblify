# Thumblify — AI Thumbnail Generator

Thumblify is a lightweight web application for generating polished thumbnail images using AI. It ships with a React + TypeScript frontend (Vite) and a Node + TypeScript backend (Express, MongoDB). The backend integrates with Google's Gemini (GenAI) to compose thumbnail content and supports user sessions and persisted thumbnail records.

**Status:** Prototype / Early

**Repository layout**
- `client/` — React + Vite frontend (TypeScript)
- `server/` — Express + TypeScript backend with MongoDB and AI integration

**Key Features**
- Generate AI-assisted thumbnails from prompts and presets
- User authentication + session management
- Persisted thumbnails and user history
- Cloud/media handling (Cloudinary integration present in server deps)
- Ready for local development and Vercel deployment

**Tech Stack**
- Frontend: React, TypeScript, Vite, Tailwind CSS
- Backend: Node.js, TypeScript, Express
- Database: MongoDB (via Mongoose)
- AI: Google Gemini (via @google/genai)
- Auth & sessions: `express-session` + `connect-mongo`

Table of contents
- Overview
- Quickstart (local)
- Environment variables
- Scripts
- Deployment notes
- Contributing

**Overview**

The app provides a friendly UI to compose and render thumbnails using AI. The frontend communicates with the backend API (`/api/*`) which is responsible for orchestrating AI requests, storing thumbnail metadata, and handling users.

**Quickstart (local)**

Prerequisites
- Node.js (v18+ recommended)
- npm or yarn
- MongoDB connection (Atlas or local)

Run the backend

1. Open a terminal and install dependencies:

```bash
cd server
npm install
```

2. Create a `.env` file in `server/` (see Environment variables below).

3. Start the server (development):

```bash
npm run server
```

Run the frontend

1. In a separate terminal:

```bash
cd client
npm install
```

2. Create a `.env` file in `client/` (see Environment variables below).

3. Start the dev server:

```bash
npm run dev
```

Open `http://localhost:5173` (or the port Vite reports) to view the app.

**Environment variables**

Server (`server/.env`)

```
MONGODB_URI=<your-mongodb-connection-string>
SESSION_SECRET=<strong-session-secret>
GEMINI_API_KEY=<your-google-gemini-api-key>
PORT=3000
NODE_ENV=development
```

Client (`client/.env`)

```
VITE_BASE_URL=http://localhost:3000
```

Notes
- The server expects `GEMINI_API_KEY` for the `@google/genai` client (see `server/configs/ai.ts`).
- Session storage uses MongoDB; ensure `MONGODB_URI` is reachable before starting the server.

**API (high level)**
- `GET /` — health check
- `POST /api/auth/*` — authentication routes
- `POST /api/thumbnail/*` — thumbnail creation and management
- `GET /api/user/*` — user-related endpoints

For exact routes and payloads, inspect `server/routes` and the controllers in `server/controllers`.

**Scripts**
- Server (dev): `cd server && npm run server` (uses `nodemon` + `tsx`)
- Server (start): `cd server && npm start`
- Client (dev): `cd client && npm run dev`
- Client (build): `cd client && npm run build`

**Deployment**

This repository includes `vercel.json` in both `client/` and `server/` indicating prior Vercel deployments. You can deploy the `client` to Vercel (or Netlify) and host the backend as a Node service (Vercel Serverless functions, a VPS, or a container). Ensure the environment variables are configured in your deployment target.

**Contributing**
- Feel free to open issues or PRs. Recommended workflow:
	1. Fork the repo
	2. Create a feature branch
	3. Run tests / lint (if added)
	4. Submit PR with description and screenshots

**Useful files to inspect**
- Frontend entry and routes: `client/src/`
- Server entry: `server/server.ts` — starts the Express app and mounts `server/routes`
- AI config: `server/configs/ai.ts`
- Thumbnail logic and controllers: `server/controllers/ThumbnailControllers.ts`

**License & Acknowledgements**
- Add a license file (`LICENSE`) if you want to open-source this project.
- Built with :heart: using React, Express, MongoDB, and Google Gemini.

---

If you'd like, I can also:
- Add examples of request/response payloads for the API
- Add a sample `.env.example` file in both `server/` and `client/`
- Add badges and CI config for tests and linting

