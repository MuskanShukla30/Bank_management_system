<h1 align="center">🏦 Bank Management System</h1>

<p align="center">
  <strong>A simple Flask and MySQL web application for user registration, login, and viewing an account balance.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python 3" />
  <img src="https://img.shields.io/badge/Flask-web%20framework-000000?style=flat-square&logo=flask&logoColor=white" alt="Flask" />
  <img src="https://img.shields.io/badge/MySQL-database-4479A1?style=flat-square&logo=mysql&logoColor=white" alt="MySQL" />
</p>

---

## ✨ Overview

The **Bank Management System** is a small web app built with Flask and MySQL. Visitors can create an account, sign in, and view the balance associated with their account on a session-protected dashboard. The project is a basic learning/demo app; it does not currently provide deposits, withdrawals, or transaction history.

## 🚀 Features

- 📝 Register a username and password
- 🔐 Log in and keep the authenticated username in a Flask session
- 💰 View the account balance on the dashboard
- 🚪 Log out and clear the session
- 🗄️ Store users and balances in MySQL
- 🎨 Simple HTML pages with a shared CSS stylesheet

## 🏗️ Architecture

```text
┌─────────────────────────────┐
│ Browser                     │
│ Home · Register · Login     │
│ Account Dashboard           │
└──────────────┬──────────────┘
               │ HTTP
┌──────────────▼──────────────┐
│ Flask application (app.py)  │
│ Routes · Session · Queries  │
└──────────────┬──────────────┘
               │ mysql-connector
┌──────────────▼──────────────┐
│ MySQL (bank_db)             │
│ users: username, password,  │
│ balance                     │
└─────────────────────────────┘
```

### Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python 3 · Flask |
| Database | MySQL · `mysql-connector-python` |
| Frontend | HTML · CSS · Jinja templates |
| Authentication | Flask session |

## 📁 Project Structure

```text
Bank_management_system/
├── app.py                 # Flask routes and MySQL operations
├── requirements.txt       # Empty in the current repository
├── database/
│   ├── __init__.py
│   ├── config.py          # MySQL connection settings
│   └── bank.sql           # Empty in the current repository
├── templates/
│   ├── index.html         # Welcome page
│   ├── register.html      # Registration form
│   ├── login.html         # Login form
│   └── dashboard.html    # Account balance view
└── static/
    └── style.css          # Shared styles
```

## 🔧 Installation & Local Setup

### Prerequisites

- Python 3 and pip
- MySQL Server
- A MySQL account with permission to create a database and table

### 1. Clone the repository

```bash
git clone https://github.com/MuskanShukla30/Bank_management_system.git
cd Bank_management_system
```

### 2. Create and activate a virtual environment (recommended)

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

macOS/Linux:

```bash
source .venv/bin/activate
```

### 3. Install dependencies

`requirements.txt` is empty in the current repository. Install the app's imports directly:

```bash
python -m pip install Flask mysql-connector-python
```

### 4. Create the database and table

The repository's `database/bank.sql` file is empty, but the app expects a database named `bank_db` with a `users` table containing `username`, `password`, and `balance` columns. In a MySQL client, run:

```sql
CREATE DATABASE bank_db;
USE bank_db;

CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(100) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    balance DECIMAL(12, 2) NOT NULL DEFAULT 0.00
);
```

Update `database/config.py` with your local MySQL host, username, password, and database name. The current file contains a hard-coded database password; replace it with your own local settings and do not commit real credentials.

### 5. Start the web app

```bash
python app.py
```

Open [http://127.0.0.1:5000](http://127.0.0.1:5000) in a browser. Register an account, sign in, and the dashboard will show the account's starting balance (the schema above defaults it to `0.00`).

## 🧭 Application Flow

| Route | Behavior |
|---|---|
| `/` | Shows the welcome page with registration and login links. |
| `/register` | Displays the registration form and inserts the submitted username and password. |
| `/login` | Checks the submitted credentials and creates a session on success. |
| `/dashboard` | Requires a logged-in session and displays the user's current balance. |
| `/logout` | Clears the session and returns to the welcome page. |

## ⚠️ Security & Current Limitations

- Passwords are currently stored and compared as plain text. This is suitable only as a learning example; a real system must use secure password hashing.
- The Flask secret key and MySQL settings are hard-coded in `app.py` and `database/config.py`. Configure them outside source code before any deployment.
- The app enables Flask debug mode when run directly. Do not use the development server or debug mode in production.
- Registration does not currently handle duplicate usernames or display validation errors.
- The dashboard only displays a balance. Deposits, withdrawals, transfers, and transaction history are not implemented.
- `requirements.txt` and `database/bank.sql` are empty in the current repository; follow the setup instructions above to install dependencies and create the schema.

---

<p align="center"><strong>Bank Management System · Flask + MySQL</strong></p>
