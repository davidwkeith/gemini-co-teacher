# Co-Teacher Gem for Gemini

Grading student work with meaningful, personalized feedback is one of the highest-impact things a teacher can do — but it's also one of the most time-consuming. This project uses a [Gemini Gem](https://gemini.google.com) to act as a co-teacher that grades student submissions with constructive, growth-mindset-oriented feedback aligned to your curriculum.

While the sample data here targets a high-school Python/OOP course, the same approach works for any subject — swap the curriculum document and adjust the prompt.

For the full motivation and walkthrough, see the blog post: [Using Gemini to Give the Feedback You Know You Should Write](https://pulletsforever.com/using-gemini-to-give-the-feedback-you-know-you-should-write/).

## Repository Contents

| File | Description |
|------|-------------|
| `co-teacher-prompt.md` | Instructions pasted into the Gem's prompt field |
| `python-oop-curriculum.md` | Curriculum reference uploaded as Gem knowledge |
| `unit6-frq-animal-shelter.md` | Sample FRQ (free-response question) for testing |
| `unit6-frq-student-responses.csv` | Sample student responses for testing |

## Setup

1. Go to [gemini.google.com](https://gemini.google.com)
2. On the left, click **Gems >** and then **+ New Gem** (not the labs version)
3. Name the gem and add a description
4. Paste the contents of `co-teacher-prompt.md` into the **Instructions** field
5. Upload `python-oop-curriculum.md` to the Gem's **Knowledge**
6. Save

## Testing

1. Open a new chat **with your Gem** (click the Gem's name, not a regular chat)
2. Upload `unit6-frq-animal-shelter.md` and `unit6-frq-student-responses.csv`
3. Ask Gemini to grade the FRQs

This works equally well with a Google Form export and a PDF of your question/rubric for your own students.

## Adapting for Your Subject

1. **Replace the curriculum document** — Write or upload a curriculum outline for your course in place of `python-oop-curriculum.md`. This could be a Google Doc or PDF.
2. **Edit the prompt** — In `co-teacher-prompt.md`, update the subject, grade level, and any tool/environment references (e.g., Chromebooks, VSCode.dev) to match your classroom.
3. **Upload to Knowledge** — Swap the knowledge file in the Gem settings to your new curriculum document.

The grading format, feedback philosophy, and linking conventions in the prompt are subject-agnostic and should work as-is.

## License

This work is licensed under a [Creative Commons Attribution 4.0 International License](https://creativecommons.org/licenses/by/4.0/).
