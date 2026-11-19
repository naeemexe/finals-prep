# MVP Spec

## User
A college student with 1–3 weeks before finals, several courses, and a pile of slides, PDFs and handwritten notes.

## Flows

### 1. Sign up / log in
- Google OAuth and email magic link (Supabase Auth).
- Email login works on its own until the Google OAuth client is configured.

### 2. Dashboard
- List of my courses, each showing the number of days until its exam.
- "New course" form with name and exam date (date and optional time).
- Setting for daily study hours (default 3).
- Today's study plan across all courses (see 8).

### 3. Upload
- File types: PDF, JPG/PNG/HEIC photos, slides exported to PDF.
- Max 20 MB per file and about 15 files per course.
- Files are stored in Supabase Storage under the user's folder.

### 4. Review extracted text
- Gemini extracts each file to text (markdown), page by page.
- Each page appears in an editable text box, with a "Save" button.
- A "Generate outline" button runs once the review is done.

### 5. Outline
- Gemini builds chapters → topics from the reviewed text.
- Each topic links back to the page ranges it came from.
- ✂️ Rename or delete topics.

### 6. Topic content (generated when the topic is first opened, then cached)
- **Notes:** finals-focused key ideas, definitions, formulas and common traps.
- **Flashcards:** about 10 per topic, flipped one at a time.
- **Question bank:** about 10 multiple-choice questions per topic (4 options, 1 correct, with an explanation).
- Every card and question shows its source quote and its file and page.

### 7. Practice test
- Modes: one topic (10 questions) or mixed across the course (15 questions, weighted toward weak topics).
- Every answer is recorded (question, chosen option, correct or not, time).
- The results page shows the score, each wrong answer with its explanation and source, and the topics that changed.

### 8. Weakness map (course page tab, plus a summary on the dashboard)
- Chapters → topics grid, where each topic is a colored tile.
- Color = weakness score: green (strong) → red (weak).
- Opacity = how much the topic has been practiced: faded under 5 attempts, solid at 5 or more. Never-practiced topics are grey.
- Shows current state only, with no history or trend.

### 9. Study plan (multi-course)
- Day by day from today until the last exam.
- Each day's hours are split across courses. A course gets more time the nearer its exam is and the weaker its topics are. A course drops out of the plan after its exam date.
- Inside each course: weakest and least-practiced topics first. Each block is either "Read notes / flashcards for topic X" or "Test on X".
- Every study day includes at least one short test.
- The plan is recalculated on every view, so it adapts as answers come in.

## Out of scope (MVP)
Sharing or live study, spaced repetition, audio or video lectures, payments, editing generated cards, offline use, native .pptx, and trend or history on the map.
