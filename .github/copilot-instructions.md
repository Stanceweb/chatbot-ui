# Copilot Instructions for Someni AI

This guide enables AI coding agents to be productive in the Someni AI codebase. It covers architecture, workflows, conventions, and integration points unique to this project.

## Architecture Overview
- **Monorepo Structure:** Organized by feature and domain. Key folders: `app/` (Next.js pages/routes), `components/` (UI and logic), `db/` (database logic), `lib/` (utilities), `supabase/` (backend config/migrations), `types/` (TypeScript types).
- **Next.js App Router:** Uses `[locale]` and `[workspaceid]` dynamic routes for internationalization and multi-workspace support.
- **Supabase Integration:** All persistent data is managed via Supabase (Postgres). Local development uses Docker and Supabase CLI. See `supabase/config.toml` and `supabase/migrations/`.
- **State Management:** React context is used for global state (`context/context.tsx`).
- **Styling:** Tailwind CSS (`tailwind.config.ts`, `globals.css`).

## Developer Workflows
- **Install:** `npm install` in project root.
- **Local Dev:**
  - Start Supabase: `supabase start` (requires Docker)
  - Run app: `npm run chat` (Next.js dev server)
- **Update:** `npm run update` (syncs codebase), `npm run db-push` (applies DB migrations)
- **Testing:**
  - Unit: `jest` (see `jest.config.ts`, tests in `__tests__/`)
  - E2E: Playwright (`playwright-test/`)
- **Environment Variables:** Copy `.env.local.example` to `.env.local` and fill values from `supabase status`.

## Project-Specific Conventions
- **Feature Folders:** UI, logic, and hooks for each feature are grouped (e.g., `components/chat/`, `components/chat/chat-hooks/`).
- **Type Safety:** All data models and API contracts are defined in `types/` and `db/`.
- **API Routes:** Serverless functions in `app/api/` follow Next.js conventions.
- **Secrets Handling:** If an env variable is set, related UI input is disabled.
- **Migration Customization:** First migration file (`supabase/migrations/20240108234540_setup.sql`) requires manual edits for `project_url` and `service_role_key`.

## Integration Points
- **Supabase:** All CRUD and auth flows use Supabase client. See `lib/supabase/` and `db/`.
- **Ollama:** Optional local model support; configure via `NEXT_PUBLIC_OLLAMA_URL`.
- **External APIs:** Keys for OpenAI, Azure, etc. are set via env vars and referenced in UI and backend logic.

## Patterns & Examples
- **Dynamic Routing:**
  - `app/[locale]/[workspaceid]/page.tsx` for workspace-specific pages
- **Context Usage:**
  - `context/context.tsx` for global state
- **Testing:**
  - `__tests__/openapi-conversion.test.ts` for unit tests
  - `playwright-test/tests/` for E2E
- **Database Logic:**
  - `db/` for all DB access patterns

## References
- **README.md:** Setup, deployment, and environment details
- **supabase/migrations/:** DB schema and customization
- **.env.local.example:** Full list of required environment variables

---

For unclear or missing sections, please provide feedback to improve these instructions.