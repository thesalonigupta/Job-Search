# Job-Search

A personal job-hunt dashboard for a post-grad search and spring 2027 internships: one page that tracks applications, networking outreach, target organizations, deadlines, to-dos, a calendar of interviews and chats, and skills/certifications.

This repo holds the dashboard **code only**. No personal data (contacts, notes, calendar entries) is committed.

## Using it

Open `dashboard/index.html` in a browser (double-click it, or serve the folder with `python3 -m http.server` and visit `http://localhost:8000/dashboard/`).

- **On claude.ai** the page uses the artifact's shared database, so records sync wherever it's opened.
- **Anywhere else** it runs in standalone mode: records are saved in that browser's local storage. Use **Export data** (top right) to download a JSON backup and **Import data** to restore it or move it to another browser.

Exports are named `jobhunt-export-YYYY-MM-DD.json` and are git-ignored so they don't end up in this public repo by accident.

## Tabs

| Tab | What it tracks |
| --- | --- |
| Overview | Reply-check reminder, pinned jobs, this week's calendar, open to-dos, job status counts, outreach funnel, next deadlines, contacts to nudge |
| To-Do | Tasks with due date, priority and status; quick-add box |
| Calendar | Interviews, coffee chats, meetings, recruiting events, assignments, club and personal items for the next 30 days |
| Jobs | Applications by status (Saved → Applied → Interviewing → Offer, or Rejected/Closed) and type (Full-time, Internship, Fellowship) with one-tap status moves |
| Outreach | Contacts grouped by stage (Request sent, Accepted, Replied); flags accepted contacts with no reply after 7 days |
| Target Orgs | Organizations by tier, why they fit, current status, careers links, new-posting flag |
| Resources & Events | Job boards, newsletters, programs and events |
| Deadlines | Upcoming and past application, scholarship and event deadlines |
| Skills & Certs | Courses and certifications with progress and target dates |

## Data format

`data/template.json` is an empty dataset you can import to start fresh. An export has the same shape: one object per collection, keyed by record id.

| Collection | Fields |
| --- | --- |
| `applications` | `org`, `role`, `job_type`, `location`, `source`, `status`, `date_applied`, `last_update`, `deadline`, `pinned`, `link`, `notes` |
| `outreach` | `name`, `org`, `role_title`, `channel`, `stage`, `date_contacted`, `last_contact`, `next_step`, `notes`, `archived` |
| `orgs` | `org`, `tier` (`1`, `2`, `pipeline`), `why_it_fits`, `current_status`, `check_back`, `careers_url`, `new_posting_flag`, `notes`, `archived` |
| `resources` | `name`, `type` (`job board`, `newsletter`, `event`, `program`), `date`, `url`, `notes`, `archived` |
| `deadlines` | `item`, `date`, `type` (`application`, `scholarship`, `event`), `notes`, `archived` |
| `certs` | `name`, `provider`, `status`, `progress`, `target_date`, `url`, `notes`, `archived` |
| `todos` | `task`, `due`, `priority`, `status`, `related`, `notes`, `archived` |
| `events` | `title`, `date`, `kind`, `start`, `end`, `where`, `calendar`, `notes`, `archived` |
| `settings/main` | `last_reply_check` |

Dates are `YYYY-MM-DD`, times are `HH:MM`, and "today" is computed in New York time.
