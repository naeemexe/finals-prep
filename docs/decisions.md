# Decisions

Each entry is marked **Confirmed** (the owner chose it) or **Assumed** (Claude's guess, not yet confirmed; change it freely).

## 2026-11-18

| # | Decision | Status |
|---|----------|--------|
| 1 | Deadline: usable today, for the owner's own finals | Confirmed |
| 2 | Login: Google OAuth + email magic link via Supabase | Confirmed |
| 3 | Study plan covers all courses in the MVP (multi-course) | Confirmed |
| 4 | Weakness map shows current state only, with no trend or history | Confirmed |
| 5 | Stack: Next.js + Supabase + Gemini (Flash) + Vercel, no change, since switching costs time today | Assumed |
| 6 | Gemini reads PDFs and photos directly, so there's no separate OCR service | Assumed |
| 7 | Upload limit 20 MB per file, about 15 files per course; PDF and images only (slides exported to PDF) | Assumed |
| 8 | Content is generated per topic when first opened, then cached | Assumed |
| 9 | About 10 flashcards and 10 multiple-choice questions per topic; tests are 10 questions (topic) or 15 (mixed) | Assumed |
| 10 | Every card and question stores a verbatim source quote and page, checked against the page text | Assumed |
| 11 | Weakness = (wrong+1)/(attempts+2); faded under 5 attempts; grey if never practiced | Assumed |
| 12 | Plan: daily hours (default 3) split by weakness ÷ days left; at least one test per day; recalculated on view | Assumed |
| 13 | No sketches exist (`docs/sketches/` missing), so the UI is a plain, clean desktop-first layout | Assumed |
| 14 | Cut first if behind: Google OAuth, topic editing, landing page, mobile polish | Assumed |
