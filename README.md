# ONNS

> “What should I wear today?”  
> ONNS is a weather OOTD community where you can share and reference temperature-based outfit ideas based on real-time feels-like temperature and users’ outfit data.

---

## Table of Contents
- [Project Goals](#project-goals)  
  - [User Perspective](#user-perspective)  
  - [Developer Perspective](#developer-perspective)  
- [Team Members](#team-members)  
- [Tech Stack](#tech-stack)  
- [Core Features Summary](#core-features-summary)  
- [Directory Structure](#directory-structure)  
- [Installation & Running](#installation--running)  
- [Environment Variables](#environment-variables)  
- [API Documentation](#api-documentation)

---

## Project Goals

> Build **“a community where users share and discover real-life outfits according to feels-like temperature.”**

### User Perspective
- Quickly browse **actual outfits** suitable for today’s weather  
- Build a **temperature-based style reference** from user outfit data  
- Narrow the **gap between feels-like temperature and real outfit choices**

### Developer Perspective
- Apply a **collaborative, maintainable architecture** (Clean Architecture, Git Flow)  
- Strengthen core skills in **Next.js 15 / TypeScript / Tailwind CSS / Supabase**  
- Experience team workflows: **PR reviews**, **Issue-based task assignment**  
- Implement a UI matching Figma designs and document a **REST API specification**

---

## Team Members

| Name        | GitHub       | Role                                                                 |
|-------------|--------------|----------------------------------------------------------------------|
| Gaeun Song  | gn-ioeo      | Login / User creation & deletion / Notifications / Likes             |
| David J Song  | jaino-song   | My Page / Conditional post queries / API design / User update & read |
| Joohyun Shin   | Shin363      | Main page / Comment management / OpenWeather & Geolocation API integration |
| Daehee Hyung    | HyungDaehee  | OOTD & post retrieval / Filtering / Post features                    |

---

## Tech Stack

| Area         | Technologies                                                     |
|--------------|------------------------------------------------------------------|
| Frontend     | Next.js 15 (App Router), React, TypeScript, Tailwind CSS, Axios, Zustand |
| Backend      | Supabase (PostgreSQL, Storage), OpenWeather API, GeoLocation API |
| Styling      | Tailwind CSS                                                     |
| Dev Tools    | ESLint, Prettier, Husky, Commitlint, Git Flow                   |
| Deployment   | Vercel                                                          |

---

## Core Features Summary

| System     | Main Features                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------|
| **User**   | Sign up, Login, Account deletion                                                                         |
| **OOTD**   | Create/Update/Delete posts; List & detail views; Display weather info; Sort (Newest / Most Liked); Filter (Season / Feels-Like Temp) |
| **Likes**  | Add/Remove like; View liked posts                                                                        |
| **Comments** | Add/View/Edit/Delete comments                                                                            |
| **Weather** | Fetch external API → Store feels-like temperature; Show today’s weather on the main page                  |
| **My Page** | View & edit profile; List of your posts & liked posts                                                   |

---

## Directory Structure

```plaintext
ONNS/
├── (backend)/                  # Clean-Architecture backend layer (DTOs, Use Cases, etc.)
├── .github/                    # GitHub workflows & issue templates
├── .husky/                     # Git hooks
├── app/                        # Next.js App Router (pages & components)
│   ├── ootd/                   # OOTD-related pages & components
│   ├── mypage/                 # My Page components
│   └── …  
├── hooks/                      # Custom React Hooks
├── lib/                        # Shared utilities
├── public/                     # Static assets (images, icons)
│   └── assets/
├── stores/                     # Zustand global state
├── types/                      # TypeScript type definitions
├── utils/                      # Axios instance & API helpers
├── OOTD-Permissions-Test.postman_collection.json  # Postman API collection
├── next.config.ts              # Next.js config
├── middleware.ts               # Next.js middleware
├── vercel.json                 # Vercel deployment config
├── package.json                # Dependencies & scripts
└── tsconfig.json               # TypeScript config
```

---

## Installation & Running

### Clone the Repository
```bash
git clone https://github.com/FRONT-END-BOOTCAMP-PLUS-5/ONNS.git
cd ONNS
```

### Install Dependencies
```bash
yarn install  # or npm install
```

### Set Environment Variables
Create a `.env.local` file at the project root with:
```env
NEXT_PUBLIC_SUPABASE_URL=your_supabase_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
WEATHER_API_KEY=your_openweather_api_key
```

### Start Development Server
```bash
yarn dev  # or npm run dev
```

### Build & Start Production Server
```bash
yarn build && yarn start  # or npm run build && npm start
```

---

## Environment Variables

| Variable Name                 | Description                                  |
|-------------------------------|----------------------------------------------|
| `NEXT_PUBLIC_SUPABASE_URL`    | Your Supabase project URL                    |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Your Supabase anonymous API key             |
| `WEATHER_API_KEY`             | External weather API key (e.g. OpenWeather)  |

---

## API Documentation
- **Postman Collection:** `./OOTD-Permissions-Test.postman_collection.json`  
- **Main Endpoints:**  
  - `GET    /api/posts`  
  - `POST   /api/posts`  
  - `PATCH  /api/posts/:id`  
  - `DELETE /api/posts/:id`  
  - `POST   /api/posts/:id/like`  
  - `POST   /api/posts/:id/comments`  
