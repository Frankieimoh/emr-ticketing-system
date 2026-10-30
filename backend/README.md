# Backend

Node.js and Express API for the ticketing system.

Planned layout:

```
backend/
  server.js        Entry point
  config/          Database and app configuration
  routes/          Route definitions
  controllers/     Request handling logic
  middleware/      Authentication (JWT) and role checks
  utils/           Email, PDF and CSV export helpers
  uploads/         Uploaded ticket attachments (not committed)
```

Setup:

1. Copy `.env.example` to `.env` and fill in your own values.
2. Run `npm install`.
3. Run `npm run dev`. The API listens on port 5000.

Route order matters in `routes/ticketRoutes.js`: `/api/tickets/categories` must be declared before `/:id`, or Express treats the word "categories" as a ticket id.
