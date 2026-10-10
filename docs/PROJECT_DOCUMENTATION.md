# Sentinel — Project Documentation

## 1. Project overview
Sentinel is a web-based prototype for tracking asset inventory and movements across multiple bases. It supports purchases, inter-base transfers, personnel assignments, role-based access control and audit history.

Assumptions: asset records represent quantities by asset code at a base; purchases add stock; transfers reduce source stock and increase destination stock; assignments reduce available stock. Demo data is synthetic.

Limitations: no return workflow, MFA, rate limiting, serial/lot tracking or production monitoring. Do not use real or classified military information.

## 2. Tech stack and architecture
React + Vite frontend → Express REST API → PostgreSQL relational database. JWT tokens authenticate requests; bcrypt hashes passwords; server middleware and route checks enforce permissions. PostgreSQL is suitable because the system relies on related records, foreign keys, constraints and transactions.

## 3. Data models
- users: name, email, password hash, role, assigned base.
- bases: base name and location.
- assets: code, name, equipment type, quantity, base, status, notes.
- purchases: asset, base, quantity, cost, supplier, date, recording user.
- transfers: asset, source/destination bases, quantity, timestamp, user.
- assignments: asset, personnel, base, quantity, status, timestamp, user.
- audit_logs: actor, action, entity, JSON details, timestamp.

## 4. RBAC
Admin can access all bases and audit logs. Base Commander can manage asset records and assignments at their own base. Logistics Officer can record purchases and transfers for their own base. Backend enforces these restrictions; hiding UI controls is not the only security layer.

## 5. API logging
Purchase, transfer, assignment and asset creation actions write audit entries. The Admin-only audit page displays recent entries. A production implementation should use immutable audit storage and alerting.

## 6. Setup instructions
See root README. Create PostgreSQL database, run `backend/db/schema.sql`, configure `backend/.env`, run backend on port 4000 and frontend on port 5173.

## 7. Main endpoints
- POST `/api/auth/login`
- GET `/api/auth/me`, `/api/bases`, `/api/dashboard`
- GET/POST `/api/assets`
- GET/POST `/api/purchases`
- GET/POST `/api/transfers`
- GET/POST `/api/assignments`
- GET `/api/audit-logs` (Admin only)

## 8. Production improvements
Add automated tests, request rate limiting, structured logs, backups, alerting, pagination, monitoring for API latency and failed authorization, and inventory reconciliation. Add item-level traceability where appropriate.
