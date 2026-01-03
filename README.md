<div align="center">

# RepoRoverAI

AI-assisted coding mentor with interactive lessons, quizzes, achievements, and GitHub repository analysis.

**Live:** https://reporoverai-chi.vercel.app/

</div>

## Overview

RepoRoverAI blends structured learning paths with AI explanations and hands-on practice. Learners progress through lessons, quizzes, and achievements while analyzing real GitHub repositories to see concepts applied in the wild.

## Core Features

- **AI tutor:** Gemini-powered explanations for code snippets and lessons.
- **Learning paths:** Guided tracks (JavaScript, Python, React) with lessons and quizzes.
- **Gamification:** XP, streaks, and achievements to keep momentum.
- **Progress insights:** Dashboard with progress charts and history.
- **GitHub analyzer:** Analyze public repos for language stats, stars, and activity; save findings to your profile.
- **Authentication:** Email/password auth with secure session handling.

## Tech Stack

- **Frontend:** Next.js 15 (App Router), React 19, TypeScript, Tailwind CSS 4, Radix UI + custom UI kit.
- **Data:** Drizzle ORM with Turso (libSQL); migrations live in `drizzle/`.
- **Auth:** better-auth with bcrypt hashing.
- **AI:** Google Gemini (`@google/generative-ai`).
- **Integrations:** GitHub API for repo analysis; charts via Recharts; forms via React Hook Form + Zod.

## Project Structure

- `src/app/` — App Router pages, API routes under `app/api/*` (auth, GitHub, lessons, quizzes, progress, repositories).
- `src/components/` — Shared UI (buttons, cards, navigation) built on Radix primitives.
- `src/db/` — Drizzle schema, seeds, and DB client.
- `drizzle/` — Generated SQL migrations and snapshots.
- `src/lib/` — Auth client and utilities.

## Prerequisites

- Node.js 18.18+ (Next.js 15 requirement)
- npm, pnpm, or yarn (examples use `npm`)

## Environment Variables

Create a `.env` file in the project root (never commit real secrets). Required keys:

| Key | Description |
| --- | --- |
| `TURSO_CONNECTION_URL` | Turso/libSQL connection string |
| `TURSO_AUTH_TOKEN` | Turso auth token |
| `BETTER_AUTH_SECRET` | Secret for better-auth sessions |
| `GEMINI_API_KEY` | Google Gemini API key |
| `GITHUB_TOKEN` | Token for GitHub API access (repo analysis) |
| `GITHUB_CLIENT_ID` | GitHub OAuth client ID |
| `GITHUB_CLIENT_SECRET` | GitHub OAuth client secret |
| `CHUNK_SIZE` | Text chunk size for content processing |
| `CHUNK_OVERLAP` | Overlap for text chunking |
| `CODE_CHUNK_SIZE` | Code chunk size for analysis |
| `CODE_CHUNK_OVERLAP` | Overlap for code chunking |

## Setup & Development

Install dependencies:

```bash
npm install
```

Run the dev server (Turbopack enabled by default):

```bash
npm run dev
```

Visit http://localhost:3000.

Lint the codebase:

```bash
npm run lint
```

## Database & Migrations (Turso)

- Ensure `TURSO_CONNECTION_URL` and `TURSO_AUTH_TOKEN` are set.
- Apply migrations to your Turso database:

```bash
npx drizzle-kit push
```

- Migration files live in `drizzle/`; schema definitions live in `src/db/schema.ts`.

## Production Build

```bash
npm run build
npm run start
```

The project is deployed on Vercel at https://reporoverai-chi.vercel.app/. For self-hosting, provide the same environment variables in your hosting platform and run the production commands above.

## Notes for Contributors

- Keep secrets out of version control; use `.env` locally and platform-specific secret managers in production.
- Favor type-safe utilities (Zod + TypeScript) for API contracts.
- UI components are shared; prefer composition over duplication when adding new screens.
