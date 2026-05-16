# Senior Full Stack Engineer — Take-Home Task

## Welcome

Thanks for taking the time to work on this. We've designed this task to be representative of the kind of problems you'd actually work on at LW3 — building reliable, performant backend services with a small frontend layer.

We respect your time. **Spend 4–6 hours on this. Please don't exceed 8.** We'd rather see honest tradeoffs in a time-boxed submission than a polished overbuild. Tell us in your README what you'd do with more time.

---

## The Scenario

Build a small system to track the lifecycle of a physical product through a supply chain.

A product is registered at manufacture and accumulates **events** as it moves through stages — `manufactured`, `shipped`, `received`, `sold`, `recycled`, and so on. Each event is permanent; the history is the source of truth.

There are two types of API consumers:
- **Internal users** — LW3 staff, full access
- **Partner users** — external companies, read-only access scoped to their own products

---

## What to Build

### Backend (Node.js + MongoDB) — the main focus

A REST API with the following endpoints:

| Method | Endpoint | Purpose |
|---|---|---|
| `POST` | `/products` | Register a new product |
| `POST` | `/products/:id/events` | Append a lifecycle event |
| `GET` | `/products/:id` | Fetch product with full event history |
| `GET` | `/products` | List products with filters and pagination |
| `GET` | `/products/:id/verify` | Verify the event chain is intact |

**Requirements and constraints:**

1. **Append-only events.** Once written, an event must never be modified or deleted. Enforce this at the data layer, not just the route.

2. **Event chain.** Each event references the previous event's ID (or hash), forming a chain. The `verify` endpoint walks the chain and confirms its integrity end-to-end.

3. **Auth via JWT.** Two roles: `internal` (full access) and `partner` (read-only, scoped to products they own).

4. **Rate limiting.** Partner endpoints should be rate-limited; internal endpoints can have a looser limit.

5. **Performance.** Assume the `GET /products` list endpoint will eventually serve 100,000+ products.

6. **Filters on the list endpoint:** by status, date range, partner ID, with pagination.

### Frontend (React) — kept intentionally small

A minimal UI with just two screens:
- A product view showing the event timeline
- A form to add a new event

**Please don't spend time on UI polish.** We're not evaluating design here.

---

## What to Submit

1. **A Git repository** (public GitHub/GitLab repo, or a zip with the `.git` folder intact). We want to see your commit history — incremental commits with meaningful messages, not one giant "initial commit."

2. **A `README.md`** with:
   - Setup instructions (we should be able to run it locally in under 5 minutes)
   - Any assumptions you made
   - What you'd do differently or add with more time


---


## What We're Evaluating

In rough order of importance:

- **Decision-making and tradeoffs.** Can you defend your choices with reasoning grounded in the constraints?
- **Code quality.** Clean structure, sensible error handling, readable naming.
- **Correctness on the hard parts.** Append-only enforcement and chain verification actually work.
- **Performance awareness.** Your indexing and query design show you've thought about scale.
- **Honesty about scope and tradeoffs.** What you didn't do is often as informative as what you did.

We are **not** evaluating:

- UI design
- Test coverage percentage (some meaningful tests are good; obsessive coverage isn't)
- Whether you used AI assistance

---

## A Few Notes

- The task brief is deliberately a little ambiguous in places (e.g. what exactly an "event" contains beyond type and timestamp). Make reasonable assumptions and document them.
- Use whichever libraries you'd reach for in a real project. Don't reinvent wheels.
- If something in this brief is unclear, email us at marungsha@logisticsw3.com — we'd rather clarify than have you guess wrong.

## Next Steps

After you submit, we'll review and schedule a **30–45 minute walkthrough call** where you'll demo the code, answer a few follow-up questions, and we'll ask you to make a small live change. That call is where most of our evaluation happens — your submission is the starting point for the conversation.

Good luck - we're looking forward to seeing what you build.

- The LW3 Team
