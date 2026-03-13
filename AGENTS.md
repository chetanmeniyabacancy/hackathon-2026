# Agent instructions (AGENTS.md)

This file gives AI agents and contributors context for the hackathon-2026 repo.

## Project overview

- **Framework**: Next.js 14 with App Router.
- **Backend / DB**: Supabase (PostgreSQL). Client in `lib/supabaseClient.ts`.
- **Main surface**: Home page lists rows from the `products` table and has an “Add Test Product” button that inserts a test row via a Server Action.

## Conventions

- Use the existing Supabase client from `@/lib/supabaseClient.ts`; do not create alternate Supabase clients unless needed for middleware/auth.
- Env: `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY` (see `.env.example` and README).
- Prefer Server Components and Server Actions; add `"use client"` only when interactivity or browser APIs are required.
- TypeScript throughout; use the `Product` type from `lib/supabaseClient.ts` for product rows.

## Important paths

- `app/page.tsx` – Home page: fetches products and renders the “Add Test Product” form (server action).
- `app/layout.tsx` – Root layout and metadata.
- `lib/supabaseClient.ts` – Supabase client and `Product` type.
- `README.md` – Local run, env setup, creating the `products` table, and testing the connection.

## Database

- Table: `products` with `id` (uuid, PK), `name` (text), `created_at` (timestamptz). SQL to create it and a permissive RLS policy is in the README.

## When making changes

- Keep the app minimal and Vercel-ready (no custom build/output config required).
- After changing env or Supabase schema, ensure README and AGENTS.md stay in sync.
- Do not commit `.env` or `.env.local`; only document required variables in `.env.example` and README.
