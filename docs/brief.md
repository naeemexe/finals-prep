Project Brief

My own notes before any prompting

Problem: College students have 1–3 weeks before finals who have a pile of slides, pdfs and handwritten notes and no idea what they're actually weak at. Studying is unfocused. Slides are usually messy. Reading everything equally doesn’t help, make flashcards by hand, and don't know which chapters are harder for them until the exam.

What I want to build: turns your course materials: PDFs, slides, even photos of handwritten notes into finals notes, flashcards and practice tests. Every answer you get wrong shades that topic red on a chapter map, so you can see exactly what to re-read. A study plan counts down to your exam and puts your weakest topics first. And given the exam dates for all the courses you can also make a plan to study and take tests daily.

Must-have features in MVP
Sign up /log in
Create a course with an exam date
Upload PDFs and photos of handwritten notes
Review and fix the extracted text before generating
Auto outline: chapters → topics
Per topic: finals-focused notes + flashcards (every card cites the source text)
Practice tests (multiple choice) that record every answer
Weakness map in main dashboard : topics turn redder the more I get wrong, faded when I've barely practiced
Study plan: day-by-day until the exam, weakest topics first

Not building for now:
Sharing with friends or live study and testing
Spaced repetition scheduling
Audio or video lectures


Stack I’m leaning toward:
Next.js + Supabase (auth, database, file storage) + Gemini API + Vercel. Open to pushback.

Screens (sketch on paper, photo in docs/sketches/)
Landing + sign up
Dashboard: my courses, days until each exam
Course page: upload, notes, flashcards, test, map tabs
Practice test + results
Weakness map + study plan

Some questions:
Max upload size? thinking 20 MB per file. Not sure about supabase limits
How many questions per topic is enough?
Should the map show trend over time
Google login or email?
