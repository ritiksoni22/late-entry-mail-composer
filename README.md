# Quik mailer

A single-page tool for drafting campus security permission emails — pick a request type, fill in the details, and it opens a pre-filled email in your default mail client.

## Request types

**Late Entry**
1. **Students going out** — search and multi-select from the student list; selections appear as removable chips below the dropdown.
2. **Expected return time** — pick a time in 15-minute increments (11:00 PM – 5:00 AM range).
3. **Vehicle number** *(optional)* — added as a line in the email body if filled.

**Offboarding**
1. **Leave campus** / **Return campus** — date + time of departure and return.

**Guest Visit**
1. **Visit date**, **Arrival time**, **Departure time**.
2. **Guests** — add as many guest rows (name + phone number) as needed.

Each tab's **Send Email** button builds the request body, then opens it via a `mailto:` link addressed per `mail-templates.json` (currently `to: csa.security@iimu.ac.in`, `cc: security@iimu.ac.in` — plus each selected student's email for Late Entry).

Review the drafted email in your mail client before sending — this tool only prepares it.

## Usage

Open `index.html` in a browser. No build step or server required.

## Files

| File | Purpose |
|---|---|
| `index.html` | Page structure/markup (tabs + all three forms) |
| `index.css` | Styling (design system: warm yellow accent, Playfair Display + Poppins) |
| `index.js` | Tab switching, dropdown, guest-row, date/time logic, and mailto building |
| `students.json` | Student roster (`name`, `roll_number`, `email_id`, `course`) |
| `mail-templates.json` | Email templates per request type (`to`, `cc`, `subject`, `body` with `{{placeholders}}`) |
| `design-system.pdf` | Visual reference the styling was adapted from |
| `thumbnail.html` / `thumbnail.png` | Social-preview image source and rendered output |

`students.json` and `mail-templates.json` are the canonical, human-editable source of truth — their contents are mirrored as JS constants (`STUDENTS`, `MAIL_TEMPLATES`) at the top of `index.js`, since a page opened directly via `file://` can't `fetch()` a sibling JSON file (CORS). **When you edit either JSON file, copy the same change into the matching constant in `index.js`.**

## Updating the student list

Edit `students.json` (and the `STUDENTS` constant in `index.js`) and add entries in the same shape:

```json
{
  "name": "Full Name",
  "roll_number": 2613066,
  "email_id": "fullname.course2026@iimu.ac.in",
  "course": "GSCM"
}
```

The dropdown, search, and chips pick up new entries automatically — no other code changes needed.

## Updating email templates

Edit `mail-templates.json` (and the `MAIL_TEMPLATES` constant in `index.js`). Each entry supports `to`, `cc`, `subject`, and a `body` string with `{{placeholder}}` tokens filled in at send time:

- `lateEntry`: `{{time}}`, `{{studentLines}}`, `{{vehicleLine}}`
- `offboarding`: `{{leave}}`, `{{back}}`
- `guest-visit`: `{{visitDate}}`, `{{visitStart}}`, `{{visitEnd}}`, `{{guestLines}}`
