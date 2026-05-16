# BACKEND_EVALUATION
## The task — "Product Provenance API" 

### Scenario

```htm
Build a small system to track the lifecycle of a physical product. A product gets an ID at manufacture, then accumulates "events" as it moves through the supply chain (manufactured → shipped → received → sold → recycled). The API serves both internal dashboards and external partners (with different permissions). Build a minimal React UI to add/view events.
```

## Required deliverables
### Backend (Node.js + MongoDB) — the focus:

*REST API with these endpoints:*

1. POST `/products` — register a new product
2. POST `/products/:id/events` — append a lifecycle event
3. GET `/products/:id` — fetch product with full event history
4. GET `/products` — list products with filters: status, date range, partner ID, pagination
5. GET `/products/:id/verify` — verify the event chain is intact.


*Constraints:*

1. Events are append-only — once written, never modified or deleted. Enforce this at the schema/route level.
2. Each event must reference the previous event's ID, forming a chain (like a mini blockchain). The verify endpoint walks the chain and confirms integrity.
3. Two user roles: internal (full access) and partner (read-only, scoped to their own products). Implement auth via JWT.
4. Rate-limit the partner endpoints.
5. The GET `/products` list endpoint must handle 100k+ products performantly.


*Frontend (React):*

1. A page to view a product's event timeline
2. A form to add a new event


## Submission Rules ( You don't need to use this repo )

1. Working code in a Git repo with meaningful commit history — not one giant `"initial commit."`
2. A `README` with setup instructions, assumptions, and what you'd do with more time.
3. **Time budget:** Shouldn't be more than 4-6 hrs. Don't spend more than 8 hours. Submit what you have.