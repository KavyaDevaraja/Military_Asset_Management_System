# 3–5 minute video walkthrough

Before recording, run the database, backend and frontend and verify the demo workflows.

**0:00–0:30 — Context:** “Sentinel is a prototype for asset inventory across multiple bases. It records purchases, transfers and personnel assignments.”

**0:30–1:00 — Architecture:** “The frontend uses React and Vite. The Express API validates requests and checks JWT authentication and roles. PostgreSQL stores users, bases, assets and transaction history.”

**1:00–1:45 — Dashboard/assets:** Show dashboard counts, search the inventory, and add a demo asset as Admin.

**1:45–2:30 — Purchases/transfers:** Record a purchase and show the stock increase. Transfer a quantity between bases and show the movement record and updated stock.

**2:30–3:00 — Assignments:** Assign a small quantity to demo personnel and show the assignment history.

**3:00–3:40 — RBAC/audit:** Explain the three roles. Sign in as Logistics Officer and show that permissions differ. Return to Admin and open the audit log.

**3:40–4:15 — Limitations:** “This is a prototype using synthetic data. A production version needs stronger authentication, tests, monitoring, return workflows and more detailed asset traceability. It must not store real classified information.”

**Close:** “Thank you for reviewing Sentinel.”
