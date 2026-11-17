# BloodBridge

A small public website that connects volunteer blood donors with people who need blood.
Donors and requesters sign up through simple forms. Phone numbers are never shown publicly:
only the admin page (password protected) shows them, so you can connect people by phone.

## Folder structure
    BloodBridge/
    ├── README.md            this file
    ├── DEPLOY.md            put it online, buy a domain
    ├── Procfile             start command for hosts such as Render
    ├── backend/
    │   ├── app.py           Flask server: routes, validation, SQLite database, matching, admin
    │   └── requirements.txt Python packages
    └── frontend/
        ├── templates/       HTML pages (base, index, donate, request, thanks, privacy, login, admin)
        └── static/style.css Styling (light and dark mode)

## Run on your computer
    cd BloodBridge
    pip install -r backend/requirements.txt
    # macOS/Linux
    ADMIN_PASSWORD=choose-a-strong-one python backend/app.py
    # Windows PowerShell
    $env:ADMIN_PASSWORD="choose-a-strong-one"; python backend/app.py
Open http://127.0.0.1:5000. The admin page is at /admin/login.
The database file `backend/bloodbridge.db` is created automatically on first run.

## Pages
| Address | What it does |
|---|---|
| `/` | Home: totals by blood group and city (no personal data) |
| `/donate` | Donor sign-up with eligibility and consent checkboxes |
| `/request` | Blood request form, with an urgent option |
| `/privacy` | Privacy statement |
| `/admin/login`, `/admin` | Admin only: view donors and requests, see compatible donors for each request (same city first), mark fulfilled, delete records |

## Settings (environment variables)
| Name | Purpose |
|---|---|
| `ADMIN_PASSWORD` | Password for /admin. If unset, the admin page stays locked. |
| `SECRET_KEY` | Long random text that signs login cookies. Set it in production. |
| `CONTACT_EMAIL` | Shown in the footer and privacy page so people can ask to be deleted. |
| `PRODUCTION` | Set to `1` online: secure cookies, debug off. |
| `DB_PATH` | Where the database file lives. Point it at a folder that survives redeploys. |

## How matching works
A request for blood group X can be filled by donors whose group appears in the compatibility map in
`backend/app.py` (`CAN`). Only donors marked available are listed, with same-city donors first.
This is a simplified teaching map, not medical advice.

## Safety notes
- This site only connects people. Real donations must happen at a licensed blood bank or hospital.
- You are storing other people's phone numbers. Start with people you know, keep the privacy page
  accurate, and delete records when asked.
- Spam protection: hidden trap field, 20-second wait between submissions, form tokens (CSRF).
