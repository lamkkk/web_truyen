# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)
- **Frontend**: React + Vite + TailwindCSS + shadcn/ui

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.

## Project: Truyen Hay — Vietnamese Story Reading Platform

### Architecture
- **Frontend**: `artifacts/story-platform/` — React + Vite + TailwindCSS
- **Backend**: `artifacts/api-server/` — Express 5 + Drizzle ORM
- **Database**: PostgreSQL (Replit managed)

### Features
- Story listing with categories, search, featured stories
- Chapter reading with dark mode and font size controls
- Content locking system (scroll 70% triggers unlock popup)
- Affiliate link monetization (Shopee integration via popup)
- Admin dashboard (create/edit stories, chapters, categories)
- JWT-based admin authentication (admin/admin123)

### Database Schema
- `categories` — story categories
- `stories` — main story table with viewCount, isFeatured, status
- `chapters` — chapter content with isLocked, affiliateLink
- `unlock_logs` — tracks user unlock events per session
- `admins` — admin users with bcrypt passwords

### Default Admin
- Username: `admin`
- Password: `admin123`

### API Routes (all under `/api`)
- `GET/POST /stories` — list/create stories
- `GET/PUT/DELETE /stories/:id` — story detail/update/delete
- `GET /stories/:id/chapters` — list chapters for story
- `GET /stories/top` — top stories by views
- `GET/POST /chapters` — chapter detail/create
- `PUT/DELETE /chapters/:id` — update/delete chapter
- `GET/POST/PUT/DELETE /categories` — category CRUD
- `POST /admin/login` — admin auth (returns JWT)
- `GET /admin/stats` — dashboard statistics
- `POST /unlock/log` — log unlock event
- `GET /unlock/check/:chapterId` — check unlock status
