# Finals Prep App

Turns course materials (PDFs, slides, handwritten-note photos) into finals notes, flashcards and multiple-choice tests, tracks weak topics on a map, and builds a daily study plan across all courses.

**Deadline: usable today (2026-11-18) for the owner's own finals.** Scope is cut to fit, so pick the simplest thing that works.

## Docs
- `docs/brief.md`: the owner's original notes (don't edit)
- `docs/spec.md`: what the MVP does
- `docs/architecture.md`: stack, data model, AI pipeline
- `docs/backlog.md`: ordered build list, with ✂️ items cut first
- `docs/decisions.md`: decisions log (confirmed vs assumed)

## Stack
Next.js (App Router, TypeScript) · Supabase (Auth, Postgres, Storage) · Gemini API (Flash) · Vercel

## Subagents (`.claude/agents/`): each writes only in its folders and reports in ≤10 lines
| Agent | Owns |
|-------|------|
| `database` | `supabase/`, `lib/db/`, `lib/types.ts`, `lib/scoring/` |
| `ui` | `app/` (except `app/api/`), `components/`, `styles/`, `public/` |
| `ai` | `lib/ai/`, `app/api/` |
| `testing` | `tests/`, `e2e/` (never fixes app code) |
| `reviewer` | read-only: Read/Grep/Glob tools only |

Root config files (`package.json`, `next.config.*`, `.env.example`, `tsconfig.json`) belong to the main session. Agents ask for changes there in their reports.

## Rules
- Every flashcard and question stores and shows its source quote and page.
- Record every test answer. Weakness and the study plan are computed from answers, never stored as their own state.
- Generate content one topic at a time when the user opens it, not all upfront.
- Gemini calls run server-side only, and the API key never reaches the client.
- Use Row Level Security on every table: users see only their own rows.
- If a feature threatens the deadline, cut it (see backlog ✂️) and note it in `docs/decisions.md`.
