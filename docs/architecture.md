# Architecture

## Stack
- **Next.js** (App Router, TypeScript, Server Actions and Route Handlers), deployed on **Vercel**.
- **Supabase:** Auth (Google and magic link), Postgres with Row Level Security (RLS), and Storage (private bucket `materials`, path `{user_id}/{course_id}/{file}`).
- **Gemini API** (Flash model): reads PDFs and images natively (this covers handwriting), returns structured JSON output, and is called from the server only.
- UI: Tailwind CSS.

## Data model (Postgres)
```
profiles      (id = auth.uid, daily_hours int default 3)
courses       (id, user_id, name, exam_at timestamptz)
files         (id, course_id, user_id, storage_path, mime, status: uploaded|extracted|failed)
pages         (id, file_id, page_no, text, edited bool)
chapters      (id, course_id, title, position)
topics        (id, chapter_id, course_id, title, position, source_page_ids uuid[], generated_at)
notes         (id, topic_id, markdown)
flashcards    (id, topic_id, front, back, source_page_id, source_quote)
questions     (id, topic_id, stem, options jsonb, correct_index, explanation, source_page_id, source_quote)
tests         (id, user_id, course_id, mode: topic|mixed, created_at)
answers       (id, test_id, question_id, topic_id, user_id, chosen_index, correct bool, answered_at)
```
Every table has a `user_id` (directly or through its course), and RLS uses `user_id = auth.uid()`.

## AI pipeline
1. **Extract** (one call per file): upload the file to Gemini → prompt asks for JSON `[{page_no, text}]` in markdown → stored in `pages`.
2. **Outline** (one call per course): send all reviewed page text with page ids → JSON `{chapters:[{title, topics:[{title, page_ids}]}]}`.
3. **Topic content** (one call when a topic is first opened): send that topic's pages → JSON `{notes, flashcards[], questions[]}`, where each card and question includes `page_id` and a verbatim `quote`. Quotes are checked server-side against the page text, and failing items are dropped.
4. Long calls run in Route Handlers with `maxDuration` raised, and the UI polls `status` or shows a spinner.

## Weakness score (computed, not stored)
For each topic, `attempts = n` and `wrong = w`:
- `weakness = (w + 1) / (n + 2)`: one miss can't turn a topic full red, and an unpracticed topic sits at 0.5.
- `confidence = min(n / 5, 1)`, which drives the tile's opacity. When n = 0 the tile is grey.

## Study plan (computed on each view)
- `days_left(c) = days until exam_at`. The plan only includes courses whose exam hasn't passed.
- Course weight for a day: `w(c) = avg_weakness(c) / max(days_left(c), 1)`. The day's `daily_hours` are split in proportion to these weights (in 30-minute blocks, at least 1 block per active course).
- Inside each course, topics are ranked by `weakness × (1.5 − confidence)` and fill the blocks: a topic never studied gets "notes + flashcards", one already studied gets "test". Each day includes at least one test block.
- The plan is a pure function in `lib/plan.ts` with unit tests.

## Limits
- Supabase free tier: 50 MB per file and 1 GB storage. The app enforces 20 MB per file on both client and server.
- Gemini free tier rate limits: content is generated per topic when opened, cached, and never regenerated automatically.
