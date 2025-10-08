# ONNS (옷늘날씨)

A weather-driven outfit community platform that helps users decide what to wear today by combining real-time weather data with social sharing.

**Live**: [https://onns.vercel.app/](https://onns.vercel.app/)

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Environment Variables](#environment-variables)
  - [Local Development](#local-development)
- [Database](#database)
- [Project Scripts](#project-scripts)
- [Coding Standards](#coding-standards)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

ONNS (옷늘날씨, "Outfit for Today's Weather") is a community-driven platform where users:

1. View today's weather and feels-like temperature.
2. Share their outfit choices and see what others are wearing.
3. Filter by season, style, or feels-like preference.
4. Engage with posts via comments and reactions.

The platform blends utility (weather data) with community (social sharing) to make outfit selection simple and social.

---

## Key Features

- **Weather + Feels-like Filters** – posts can be tagged with feels-like ranges and seasons.
- **Social Login** – easy authentication via OAuth providers.
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
│         Application          │  Use cases, services, business logic
│   (backend/application/*)    │
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
       ┌───────▼─────────┐
       │    Supabase     │  PostgreSQL + Realtime + Storage + Auth
       │   (Database)    │
       └─────────────────┘
```

---

## Tech Stack

- **Web**: Next.js (App Router), React, TypeScript, Tailwind CSS
- **Backend**: Supabase (Database, Realtime, Storage, Authentication)
- **State Management**: Zustand for client state
- **Design**: Figma for wireframes and prototyping
- **Tooling**: ESLint, Prettier, commitlint, Husky

---

## Project Structure

```
.
├─ app/                 # Next.js App Router pages, layouts, server actions, API routes
├─ backend/             # Domain / application / infrastructure (Clean Architecture)
│  ├─ application/      # Use cases and business logic
│  ├─ domain/           # Entities and value objects
│  └─ infrastructure/   # Supabase adapters and external services
├─ components/          # Reusable React components
├─ hooks/               # Custom React hooks
├─ stores/              # Zustand stores
├─ lib/                 # Shared libraries and utilities
├─ utils/               # Helper functions
├─ constants/           # Application constants
├─ types/               # TypeScript type definitions
├─ public/              # Static assets
├─ next.config.ts       # Next.js configuration
├─ middleware.ts        # Auth and routing middleware
└─ package.json         # Dependencies and scripts
```

---

## Getting Started

### Prerequisites

- **Node.js**: 18.x or 20.x LTS
- **Yarn** or **pnpm** (Yarn recommended)
- **Supabase account**: for database, authentication, and storage

### Environment Variables

Create a `.env.local` file at the project root:

| Name                   | Example                          | Description                      |
| ---------------------- | -------------------------------- | -------------------------------- |
| `NEXT_PUBLIC_SUPABASE_URL`         | `https://xyzcompany.supabase.co` | Supabase project URL             |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY`    | `eyJhbG...`                      | Supabase anonymous key           |
| `SUPABASE_SERVICE_ROLE_KEY`        | `eyJhbG...`                      | Supabase service role key (server-side) |
| `GOOGLE_CLIENT_ID`     | `...apps.googleusercontent.com`  | OAuth provider ID (if enabled)   |
| `GOOGLE_CLIENT_SECRET` | `...`                            | OAuth provider secret            |

### Local Development

```bash
# 1) Install dependencies
$ yarn install

# 2) Set up environment variables
$ cp .env.example .env.local
# Edit .env.local with your Supabase credentials

# 3) Start development server
$ yarn dev
# App runs on http://localhost:3000
```

---

## Database

The application uses **Supabase** for database management:

- PostgreSQL database hosted on Supabase
- Real-time subscriptions for live updates
- Row-level security (RLS) for data protection
- Built-in authentication and storage

### Supabase Setup

1. Create a new project on [Supabase](https://supabase.com)
2. Set up your database tables using the Supabase dashboard or SQL editor
3. Configure Row Level Security policies for data access control
4. Copy your project URL and anon key to `.env.local`

---

## Project Scripts

Run scripts with `yarn <script>`:

- `dev` – start Next.js development server
- `build` – build production assets
- `start` – start production server
- `lint` – run ESLint checks
- `format` – run Prettier formatting
- `typecheck` – run TypeScript compiler checks

---

## Coding Standards

- **ESLint + Prettier** enforced for code quality and consistency
- **Conventional Commits** enforced via Husky and commitlint
- **Clean Architecture** with modular folder-by-layer organization
- **TypeScript** for type safety across the application

Commit message format: `type(scope): description`
- Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

---

## Deployment

### Recommended Stack

- **Frontend & API**: Vercel (optimal for Next.js)
- **Database & Services**: Supabase (PostgreSQL + Realtime + Auth + Storage)

### Deployment Steps

1. Push your code to GitHub
2. Connect your repository to Vercel
3. Add environment variables in Vercel dashboard
4. Deploy automatically on push to main branch

Ensure all environment variables are configured in your hosting provider.

---

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes using conventional commits
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## License

TBD – if open-sourced, consider MIT; else update accordingly.
