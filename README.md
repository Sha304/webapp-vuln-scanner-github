# WebApp Vuln Scanner (minimal)

A lightweight, educational web application vulnerability scanner with a small Flask UI. It performs simple automated checks for common issues (reflected XSS and basic SQL injection patterns) by crawling same-host pages and testing form inputs and query parameters.

---

## 🔍 What this project does

- Crawls a target site (same host) and collects pages and forms.
- Tests form inputs and query parameters using predefined payloads for:
  - Reflected XSS (payload reflected in the response) ✅
  - Basic SQL injection detection by looking for common SQL error text in responses ✅
- Provides a minimal web UI (`/`) to submit a URL and view findings.
- Includes small utility functions for saving scan output to `scan_results.json` (via `db.py`).

> Note: This is a minimal, educational scanner — it is not a full-featured security scanner and can produce false positives.

---

## ✅ Features

- Simple crawler limited to the same host
- Form discovery and automatic payload injection
- Tests for reflected XSS and common SQLi error messages
- Flask-based UI and an API endpoint (`POST /scan`) to run scans programmatically

---

## ⚠️ Limitations & Safety

- Only performs unauthenticated checks; does not handle login-protected pages
- May produce false positives and cannot be used as a replacement for professional tools
- **Do not** run this scanner against systems you do not own or have explicit permission to test. Unauthorized scanning may be illegal.

---

## 🧰 Prerequisites

- Python 3.8 or newer
- pip
- (Optional) A virtual environment tool like `venv` or `virtualenv`

Required Python packages (listed in `requirements.txt`):
- Flask
- requests
- beautifulsoup4
- lxml
- python-dotenv
- tqdm

---

## 🚀 Installation & Quick Start (Windows)

1. Clone the repo and change directory:

   git clone <repo-url>
   cd webapp-vuln-scanner-github

2. Create and activate a virtual environment:

   python -m venv venv
   .\venv\Scripts\activate

3. Install dependencies:

   pip install -r requirements.txt

4. Start the app:

   python app.py

   Or on Windows use `run_windows.bat`, on Unix use `run_unix.sh` (make sure scripts are executable).

5. Open the UI in your browser:

   http://127.0.0.1:5000

---

## 🔁 API Usage

Run a scan via curl (form POST):

curl -X POST -F "url=http://example.com" http://127.0.0.1:5000/scan

Or POST JSON:

curl -X POST -H "Content-Type: application/json" -d '{"url":"http://example.com"}' http://127.0.0.1:5000/scan

The endpoint returns JSON with `results.issues`, an array of issues found.

---

## 🧩 Project Structure

- `app.py` — Flask web app & API
- `analyzer.py` — wrapper to run scans and normalize URLs
- `scanner.py` — crawler + basic scanners for forms and query params
- `payloads.py` — XSS & SQLi payload lists
- `db.py` — small helper to persist scan results to `scan_results.json`
- `templates/` & `static/` — UI files

---

## ✍️ Contributing

Pull requests are welcome. Please keep changes focused and add tests or examples when adding functionality.

---

## 📜 License

This project is provided for educational purposes. Use responsibly and at your own risk.
