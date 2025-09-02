# ONNS (옷늘날씨)

A weather-driven outfit community platform that helps users decide what to wear today by combining real-time weather data with social sharing.

**Live**: [https://onns.vercel.app/](https://onns.vercel.app/)

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Monorepo Layout](#monorepo-layout)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Environment Variables](#environment-variables)
  - [Local Development](#local-development)
- [Database](#database)
- [Project Scripts](#project-scripts)
- [Coding Standards](#coding-standards)
- [Deployment](#deployment)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

ONNS (옷늘날씨, “Outfit for Today’s Weather”) is a community-driven platform where users:

1. View today’s weather and feels-like temperature.
2. Share their outfit choices and see what others are wearing.
3. Filter by season, style, or feels-like preference.
4. Engage with posts via comments and reactions.

The platform blends utility (weather data) with community (social sharing) to make outfit selection simple and social.

---

## Key Features

- **Weather + Feels-like Filters** – posts can be tagged with feels-like ranges and seasons.
- **Social Login** – easy authentication via providers.
- **Responsive Design** – optimized across devices with Tailwind CSS.
- **Real-time Feeds** – new posts and comments update instantly via Supabase Realtime.
- **Scalable Backend** – built with Clean Architecture for separation of concerns.
- **Community-first UX** – designed with Figma wireframes before coding to ensure smooth flows.

---

## Architecture

```
┌──────────────────────────────┐
│            App UI            │  Next.js (App Router), React, Tailwind
│  (app/*, components, hooks)  │
└──────────────┬───────────────┘
               │ API Routes / Server Actions (app/api/*)
┌──────────────▼───────────────┐
│         Application           │  Use cases, services, business logic
│   (backend/application/*)     │
└──────────────┬───────────────┘
               │ Calls into domain + adapters
┌──────────────▼───────────────┐
│            Domain            │  Entities, value objects
│     (backend/domain/*)       │
└──────────────┬───────────────┘
               │ Port interfaces
┌──────────────▼───────────────┐
│       Infrastructure         │  Supabase adapters (DB, storage, auth)
│  (backend/infrastructure/*)  │
└──────────────┬───────────────┘
               │
       ┌───────▼─────────┐     ┌───────────────┐
       │   Prisma ORM    │────▶│  PostgreSQL   │
       │  (prisma/*)     │     │  (DATABASE)   │
       └─────────────────┘     └───────────────┘
```

---

## Tech Stack

- **Web**: Next.js (App Router), React, TypeScript, Tailwind CSS
- **Auth**: NextAuth.js (social login)
- **DB/ORM**: PostgreSQL + Prisma
- **Backend**: Supabase (Database, Realtime, Storage)
- **State**: Zustand for client state management
- **Design**: Figma for wireframes and prototyping
- **Tooling**: ESLint, Prettier, commitlint, Husky

---

## Monorepo Layout

```
.
├─ app/                 # Next.js App Router pages, layouts, server actions, API routes
├─ backend/             # Domain / application / infrastructure (Clean Architecture)
├─ prisma/              # Prisma schema, migrations, seed
├─ public/              # Static assets
├─ hooks/ stores/       # Reusable React hooks, Zustand stores
├─ lib/ utils/          # Shared libs, helpers, validators
├─ constants/ types/    # Shared constants and TS types
├─ next.config.ts       # Next.js config
├─ middleware.ts        # Auth / routing middleware
└─ package.json         # Scripts and configs
```

---

## Getting Started

### Prerequisites

- **Node.js**: 18.x or 20.x LTS
- **Yarn** or **pnpm** (Yarn default)
- **PostgreSQL**: local or hosted (Supabase recommended)

### Environment Variables

Create a `.env` file at the project root:

| Name                   | Example                                      | Description                                     |
| ---------------------- | -------------------------------------------- | ----------------------------------------------- |
| `DATABASE_URL`         | `postgresql://user:pass@localhost:5432/onns` | Prisma connection string                        |
| `NEXTAUTH_URL`         | `http://localhost:3000`                      | NextAuth base URL                               |
| `NEXTAUTH_SECRET`      | `...`                                        | NextAuth secret (use `openssl rand -base64 32`) |
| `SUPABASE_URL`         | `https://xyzcompany.supabase.co`             | Supabase project URL                            |
| `SUPABASE_ANON_KEY`    | `...`                                        | Supabase anon key                               |
| `GOOGLE_CLIENT_ID`     | `...apps.googleusercontent.com`              | OAuth provider (if enabled)                     |
| `GOOGLE_CLIENT_SECRET` | `...`                                        | OAuth provider secret                           |

### Local Development

```bash
# 1) Install deps
$ yarn install

# 2) Generate Prisma client
$ npx prisma generate

# 3) Run migrations
$ npx prisma migrate dev --name init

# 4) Seed DB (optional)
$ npx prisma db seed

# 5) Start dev server
$ yarn dev
# http://localhost:3000
```

---

## Database

- Prisma schema in `prisma/schema.prisma`.
- Supabase provides hosted DB + realtime listeners.
- Use Prisma migrate and studio as usual.

Common commands:

```bash
npx prisma studio
npx prisma migrate dev --name <change>
npx prisma db push
```

---

## Project Scripts

- `dev` – start dev server
- `build` – build production assets
- `start` – start production server
- `lint` – run ESLint
- `format` – run Prettier
- `typecheck` – run TS compiler checks
- `prisma:*` – Prisma CLI helpers

---

## Coding Standards

- ESLint + Prettier enforced.
- Conventional commits enforced via Husky/commitlint.
- Modular folder-by-layer code organization.

---

## Deployment

- **Vercel** recommended for frontend and API routes.
- **Supabase** handles DB, realtime, and storage.
- Ensure env vars are configured in Vercel + Supabase dashboard.

TBD – if open-sourced, consider MIT; else update accordingly.

