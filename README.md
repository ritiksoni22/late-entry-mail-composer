# Late Entry Mail Composer

A single-page tool for drafting late-entry permission emails to the campus security desk — pick the students going out and their expected return time, and it opens a pre-filled email in your default mail client.

## Usage

Open `index.html` in a browser. No build step or server required.

1. **Students going out** — search and multi-select from the student list; selections appear as removable chips below the dropdown.
2. **Expected return time** — pick a time in 15-minute increments (11:00 PM – 5:00 AM range).
3. **Send Email** — builds the request body, then opens it via a `mailto:` link:
   - **To:** `csa.security@iimu.ac.in`
   - **Cc:** `security@iimu.ac.in` + each selected student's email
   - **Subject:** `Request for late entry`

Review the drafted email in your mail client before sending — this tool only prepares it.

## Files

| File | Purpose |
|---|---|
| `index.html` | Page structure/markup |
| `index.css` | Styling (design system: warm yellow accent, Playfair Display + Poppins) |
| `index.js` | Dropdown, time picker, and mailto logic |
| `students.json` | Student roster (`name`, `roll_number`, `email_id`, `course`) |
| `design-system.pdf` | Visual reference the styling was adapted from |

## Updating the student list

Edit `students.json` and add entries in the same shape:

```json
{
  "name": "Full Name",
  "roll_number": 2613066,
  "email_id": "fullname.course2026@iimu.ac.in",
  "course": "GSCM"
}
```

The dropdown, search, and chips pick up new entries automatically — no code changes needed.
