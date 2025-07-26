## Core Dependencies

| Purpose             | Dependency                     | TL;DR Use                         |
| ------------------- | ------------------------------ | --------------------------------- |
| React framework     | `next`, `react`, `react-dom`   | Build frontend & backend in one   |
| Styling             | `tailwindcss`                  | Build clean UI fast               |
| Type safety         | `typescript`                   | Avoid bugs, get autocomplete      |
| Global state        | `zustand`                      | Track UI state (e.g., toggles)    |
| Fullstack API layer | `@trpc/server`, `@trpc/client` | Define and use APIs type-safely   |
| Data fetching       | `@tanstack/react-query`        | Handle API loading/error/caching  |
| DB ORM              | `prisma`, `@prisma/client`     | Define and query your Postgres DB |
| Authentication      | `next-auth`                    | Login, sessions, secure pages     |



## Fullstack Habit Tracker Architecture
                  ┌──────────────────────────────┐
                  │          Browser UI          │
                  │       (React + Next.js)      │
                  └─────────────┬────────────────┘
                                │
                                ▼
          ┌─────────────────────────────────────────────┐
          │          Frontend Client (App Router)       │
          │                                             │
          │ - TailwindCSS for styling                   │
          │ - Zustand for UI state                      │
          │ - trpc.useQuery()/useMutation()             │
          │   ⟶ calls typed backend procedures          │
          │ - Auth.js useSession() for user state       │
          └──────────────┬──────────────────────────────┘
                         │
                         ▼
     ┌────────────────────────────────────────────────────────────┐
     │          API Route Handler (Next.js App Router)            │
     │                                                            │
     │  /api/trpc/[trpc]/route.ts                                 │
     │  - Receives request from tRPC hooks                        │
     │  - Creates context (auth, Prisma, session, etc.)           │
     └──────────────┬─────────────────────────────────────────────┘
                    │
                    ▼
        ┌────────────────────────────────────────────┐
        │         tRPC Router (Backend Logic)        │
        │                                            │
        │ - Procedures: createHabit, getHabits, etc. │
        │ - Calls Prisma to read/write DB            │
        └──────────────┬─────────────────────────────┘
                       │
                       ▼
          ┌──────────────────────────────────────┐
          │            Prisma ORM                │
          │ - Talks to your PostgreSQL DB        │
          │ - Auto-generates types for models    │
          └──────────────┬───────────────────────┘
                         │
                         ▼
              ┌────────────────────────────┐
              │     PostgreSQL Database    │
              │  Hosted via Railway/Supabase │
              └────────────────────────────┘

