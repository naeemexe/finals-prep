# Backlog

Build in this order. ✂️ = cut first if the day runs out.

## Today (MVP)
1. [ ] Scaffold Next.js + Tailwind, Supabase client, env vars (`GEMINI_API_KEY`, Supabase URL/keys)
2. [ ] Database schema + RLS migration, `materials` storage bucket
3. [ ] Auth: email magic link (Google OAuth when the client ID is ready)
4. [ ] Dashboard: course list with days left, new-course form
5. [ ] Upload files to Storage (20 MB check)
6. [ ] Extract with Gemini → `pages`, then the review/edit screen
7. [ ] Generate outline → chapters/topics
8. [ ] Topic page: generate when opened → notes, flashcards, questions (with quote checking)
9. [ ] Practice test (topic and mixed) that records answers, plus the results page
10. [ ] Weakness map tab (color + opacity)
11. [ ] `lib/plan.ts` multi-course plan + tests, shown on the dashboard
12. [ ] Daily-hours setting
13. [ ] Deploy to Vercel, run a smoke test with one real course
14. [ ] ✂️ Google OAuth
15. [ ] ✂️ Rename or delete topics
16. [ ] ✂️ Landing page beyond a sign-in button
17. [ ] ✂️ Mobile layout polish

## Later
- Map trend or history over time
- Spaced repetition
- Edit generated cards and questions
- Native .pptx upload
- Sharing / study with friends
- Audio or video lectures
