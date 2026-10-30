# EMR Issue Ticketing and Management System for LAMISPlus

An AI-driven, web-based system for reporting, classifying and tracking issues raised by users of LAMISPlus, a Nigerian HIV/ART management platform. It is the practical component of a Master's thesis in Software Engineering at MIVA Open University.

## The problem

Facilities that use LAMISPlus report problems such as NDR XML errors, HTS record issues, biometrics failures and sync problems. These reports often arrive through informal channels, get categorised inconsistently and are hard to track. This project gives support teams one place to submit, classify, assign, resolve and analyse those issues.

## What it does

- Ticket submitters describe a problem and attach files. The AI service picks the category and priority automatically, so there is no category dropdown on the form.
- Technical leads and IT technicians assign, update and resolve tickets.
- Admins manage users and roles.
- Users receive in-app and email notifications.
- A dashboard shows KPIs and charts, and tickets can be exported as PDF or CSV.

The four user roles are Admin, Technical Lead, IT Technician and Ticket Submitter.

## Architecture

The system has three tiers plus a separate AI service.

```
React frontend (3000)  -->  Node/Express API (5000)  -->  PostgreSQL (5432)
                                   |
                                   +-->  FastAPI AI service (8000)
```

| Part | Technology |
|---|---|
| Frontend | React, Tailwind CSS, Recharts, React Router, Axios |
| Backend | Node.js, Express, JWT authentication, Nodemailer, pdfkit, json2csv |
| Database | PostgreSQL |
| AI service | Python, FastAPI, scikit-learn (TF-IDF with Logistic Regression) |

## Repository layout

```
emr-ticketing-system/
  backend/      Express API, routes, controllers, middleware
  frontend/     React application
  ai-service/   FastAPI service and training data
  database/     Schema, seed data and migrations
  docs/         Thesis notes, diagrams and screenshots
```

Each folder has its own short README explaining what belongs there.

## Getting started

These steps assume the application code has been added to each folder.

1. Install Node.js, Python 3.10 or newer, and PostgreSQL.
2. Create a database named `emr_ticketing` in PostgreSQL.
3. Run the SQL files in `database/` to create the tables and load the seed data.
4. Copy `backend/.env.example` to `backend/.env` and fill in your own values.
5. Start the backend: `cd backend`, `npm install`, `npm run dev`. It runs on port 5000.
6. Start the AI service: `cd ai-service`, `pip install -r requirements.txt`, `uvicorn main:app --reload --port 8000`.
7. Start the frontend: `cd frontend`, `npm install`, `npm start`. It opens on port 3000.

## Database

The schema has 11 tables: users, roles, tickets, issue_categories, ticket_updates, ticket_assignments, ai_predictions, feedback, audit_logs, notifications and export_records. The issue_categories table is seeded with 27 LAMISPlus-specific categories covering areas such as NDR XML, HTS, PMTCT, PrEP/PEP, biometrics and the EAC, ICT and OVC cascades.

## AI classification

The current model is trained on synthetic samples, so accuracy for category and priority is moderate. A real LAMISPlus dataset is being built to retrain it. DistilBERT is planned as an upgrade once there is enough data.

## Status

The project is in active development. This repository currently holds the initial structure, and the application code is being moved in from local development.

Planned work:

- Fix the tablet login issue caused by local network access
- Finish the Tickets page export dropdown and date range filter
- Expand the training dataset and retrain the classifier

## Security note

Never commit `.env` files, database passwords or JWT secrets. The `.gitignore` in this repository already excludes them.

## Author

Frank Imoh, MSc Software Engineering, MIVA Open University.
