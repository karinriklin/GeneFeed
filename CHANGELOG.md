# Changelog

All notable changes and product decisions are documented here.

---

## v1.0.0 — Initial release

### What shipped
- 3-step onboarding (household size, dietary restrictions, health goal)
- AI-powered 7-day meal plan generation via Claude API
- Full recipe cards with ingredients, method, and biohacking rationale
- Scaled shopping list with methylation support markers
- Personalised supplement stack with timing and reasoning
- Per-meal 👍/👎 feedback wired to preference profile
- Plan-level feedback (3-day check-in prompt)
- Weekly micro-survey feeding into next plan generation
- Profile tab showing taste stats, liked/disliked meals, and explicit notes
- Conflict detection for impossible dietary combos (e.g. Carnivore + Vegan)
- Full localStorage persistence — no account required

### Decisions log

**Single-file architecture**
Chose a single `index.html` with no build step or dependencies. Rationale: the builder is non-technical, zero budget, and needs to ship and share quickly. A React app with a bundler would add friction with no user-facing benefit at v1 scale.

**No user accounts in v1**
Accounts add auth complexity, a backend, and a database — none of which are needed to validate whether users want the core product. localStorage is sufficient for v1. Moved to v2 backlog.

**Claude API called client-side**
For v1, the API call happens directly from the browser. No backend proxy needed. This keeps the architecture simple and free to host. Will need a backend proxy in v2 to protect API keys at scale.

**Fallback mock plan**
If the API call fails (network, quota, etc.), the app falls back to a realistic hardcoded plan rather than showing an error. This ensures the demo and portfolio presentation always work, and gives users something useful even in degraded state.

**Fraunces + DM Sans typography**
Chose Fraunces (optical-size serif) for display headings and DM Sans for body. Rationale: the warm & natural design direction needed a humanist, organic feel — not a clinical sans-serif stack. Fraunces has character without being precious.

**Dietary restrictions override all nutrition principles**
When a user's dietary choice conflicts with a Brecka principle (e.g. vegan + high animal protein), the restriction wins. Rationale: user autonomy and trust. The app should never feel preachy or like it's second-guessing the user's choices.

**Feedback is never blocking**
All three feedback levels (per-meal, plan-level, micro-survey) are always dismissible with one tap. Rationale: forcing feedback destroys trust and session completion rates. The preference signal from voluntary feedback is higher quality anyway.

### What was cut from v1
- Individual meal regeneration — adds complexity; users can regenerate the full plan instead
- Snack slot — adds UI complexity; not core to the value proposition
- Calendar integration — v2 feature; no user signal yet that it's needed
- Social sharing — not aligned with the private, personal nature of meal planning
- Mobile app — web-first for v1; validate before investing in native

---

## Upcoming — v1.1

- [ ] Regenerate individual meals inline
- [ ] Print / export plan as PDF
- [ ] Shareable plan link (read-only)
