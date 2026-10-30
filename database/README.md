# Database

PostgreSQL schema and seed data. Database name: `emr_ticketing`.

Planned files:

```
database/
  schema.sql      Table definitions
  seed.sql        Roles and the 27 LAMISPlus issue categories
  migrations/     Numbered changes made after the first version
```

Tables: users, roles, tickets, issue_categories, ticket_updates, ticket_assignments, ai_predictions, feedback, audit_logs, notifications, export_records.

The users table has a generated column that joins first_name and last_name into full_name, so do not insert into full_name directly.

Load order: run schema.sql first, then seed.sql, against the emr_ticketing database (for example with pgAdmin or psql).
