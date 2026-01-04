# DIT Result Viewer ✅

A lightweight front-end for viewing internal assessment results for Manmohan Memorial Polytechnic — Department of Information Technology.

---

## Overview
over
This project provides a small web UI that queries a remote Google Apps Script / sheet-based API to fetch and display student assessment results. It supports roll number, semester and DOB verification and renders a printable result card.

## Features

- Simple form-based UI (`index.html`) to request results
- Client-side DOB parsing and validation with flexible formats (YYYY-MM-DD, DD/MM/YYYY, etc.)
- Pretty, responsive result display with print support (`styles.css`)
- Inlined JavaScript logic in `index.html` that calls the Google Apps Script endpoint (external `app.js` has been moved to `app.js.bak` as a backup)
- Marks labeled `abs`/`absent` in the sheet as **Absent** in the result and treats any Absent subject as a failing subject (overall status becomes Fail)
- Subject names remain **black** for both Fail and Absent rows to keep the result sheet readable; status pills indicate Pass/Fail/Absent colors
- Printing hides the page header and form controls so only the result card is printed
- Helpful error messages and debug logging for easier troubleshooting

---

## Quick start 🚀

1. Clone or copy the project files to a local folder.
2. Recommended: run a simple local HTTP server (some browsers block fetch on `file://`):
   - Python 3: `python -m http.server 8000`
   - Or use the VS Code Live Server extension
3. Open `http://localhost:8000/` (or the server URL) and use the form to view results.

Note: Network requests go to the configured `API_URL` in the JS. Ensure that endpoint is reachable and allows CORS from your origin.

---

## Usage

- Enter **Roll No**, select **Semester**, and enter **DOB** (supported formats: `YYYY-MM-DD`, `YYYY/MM/DD`, `DD/MM/YYYY`, `MM/DD/YYYY`).
- Click **View Result**. If the record matches (Roll, Semester, DOB), a result card is displayed and can be printed.

---

## Styling & Behavior 🎨

- **College name** (`Manmohan Memorial Polytechnic`) is styled **red** for visibility.
- **Subject names** are rendered in **black** even when a subject fails or is marked Absent (the status pill shows red for Absent/fail).
- **Absent** subjects show a red "Absent" status pill and are treated as Fail for the overall status calculation.
- **Overall status** in the summary row: green for Pass, red for Fail.
- **Logo** is present in both the page header and the result card; logo sizes are controlled in `styles.css`.
- **Printing** hides the page header and form to print only the result card.

---

## Development & Notes 🔧

- Main files:
  - `index.html` — UI and inlined JS (preferred / active)
  - `styles.css` — styling for the result card and form
  - `app.js.bak` — previously `app.js`, moved to backup after JS was inlined in `index.html`
- Adjust the API endpoint by editing `API_URL` in the inline script at the top of `index.html` (or restore `app.js` from `app.js.bak` if you prefer an external file).
- If you see CORS or `file://` errors, serve the site over HTTP and check the remote API CORS policy.

---

## Troubleshooting

- "Page opened via file://" — open via HTTP server (see Quick start).
- "Server returned ..." — the API returned an error; check network console and the API URL.
- DOB validation errors — ensure DOB is in `YYYY-MM-DD` format and not a future date.
- If a subject is marked `abs`/`absent` in the sheet, it will show as **Absent** on the result and the overall status will be **Fail** (intended behavior).

---

## File structure

```
DIT_result/
  ├─ index.html
  ├─ styles.css
  ├─ app.js.bak  # backup of previous external JS
  ├─ README.md
```

---

## License

MIT — feel free to adapt for educational and internal use.

---

If you'd like, I can also add a short CONTRIBUTING guide or tidy up `app.js` to remove duplicated/trailing code. 💡