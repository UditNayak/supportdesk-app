# Scaler Support Desk

A small Flask-based internal support-desk web application. Users can log in, view and search
their tickets, post comments, upload and download attachments, run network diagnostics, and
escalate tickets.

> **Note:** This application is intended for educational and security-training purposes. It
> should not be deployed in a production environment.

## Requirements

- Python 3.8+

## Setup

Create and activate a virtual environment, then install dependencies:

```bash
python3 -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

## Running the app

```bash
python app.py
```

The app starts on `http://127.0.0.1:5050`.

Seed accounts created on first run:

| Username | Password  | Role  |
|----------|-----------|-------|
| alice    | alice123  | user  |
| bob      | bob123    | user  |
| carol    | carol123  | admin |

## Static analysis

This project is scanned with [Semgrep](https://semgrep.dev/), which is included in
`requirements.txt` and therefore installed by the setup step above. Scan results are kept in
the `semgrep-results/` folder.

To reproduce the scan (with the virtual environment activated):

```bash
# Make sure the results folder exists
mkdir -p semgrep-results

# Human-readable output
semgrep scan --config auto --exclude venv . > semgrep-results/semgrep_results.txt 2>&1

# Machine-readable output (JSON)
semgrep scan --config auto --exclude venv --json . > semgrep-results/semgrep_results.json
```

`--config auto` downloads and applies Semgrep's recommended rule sets (an internet
connection is required on the first run). `--exclude venv` keeps the scan focused on the
application code rather than installed dependencies.

## Project structure

```
supportdesk-app/
├── app.py            # Flask routes and application entry point
├── models.py         # SQLite data access layer
├── utils.py          # Helper functions (hashing, validation, path resolution)
├── templates/        # Jinja2 HTML templates
│   ├── base.html
│   ├── index.html
│   └── … (other .html files)
├── static/           # CSS
│   └── styles.css
└── attachments/      # Uploaded ticket attachments
```