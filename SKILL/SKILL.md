---
name: genefeed
description: >
  Master reference skill for building, designing, and iterating on GeneFeed — a biohacking
  meal plan app. Use this skill whenever working on any aspect of this product — features, UI,
  copy, architecture, content logic, or roadmap decisions. Trigger on any request involving
  GeneFeed, the meal plan app, Gary Brecka nutrition principles, supplement recommendations,
  recipe generation, dietary restriction handling, or product strategy for this project.
  Always read this skill before writing any code, copy, or design for this product.
---

# GeneFeed — product skill

## Product name
**GeneFeed** — confirmed.

---

## Vision statement

> "You're out of ideas of what to eat? Not sure you're getting the right nutrients at the right time? Want to get the most out of your food? GeneFeed gives you a personalised weekly meal plan, supplement guide, and recipe book — built on biohacking science, tailored to how you actually eat."

The product removes decision fatigue around food. It doesn't lecture. It just hands you a plan.

---

## Target user

Health-conscious adults (25–45) who:
- Are aware of or follow Gary Brecka, Andrew Huberman, or similar biohacking voices
- Feel overwhelmed by nutrition information and want it distilled into an actionable weekly plan
- Have specific dietary needs (vegan, GF, keto, etc.) and struggle to find plans that honour them
- Want to feel better, have more energy, and eat intentionally — without becoming a full-time nutritionist

**They are not:** hardcore bodybuilders or clinical patients. Tone should feel like a knowledgeable friend, not a medical professional.

---

## Core nutrition principles (Gary Brecka-inspired)

All meal plans must align with these foundations:

1. **High protein, animal-based baseline** — prioritise whole animal proteins (eggs, meat, fish, organs) unless user is vegan/vegetarian, in which case use complete plant proteins (tempeh, quinoa, legume combos)
2. **Eliminate ultra-processed foods** — no refined seed oils, artificial sweeteners, additives, or packaged "health" foods with long ingredient lists
3. **Methylation support** — include methylation-friendly foods weekly: leafy greens (spinach, kale), eggs (choline + B12), liver (folate), legumes, sunflower seeds
4. **Circadian / time-restricted eating** — default meal timing should respect a 8–10 hour eating window; breakfast should not be ultra-early; dinner should not be ultra-late
5. **Whole food sourcing** — every ingredient should be recognisable as a real food; prioritise organic, seasonal, and minimally processed

When dietary restrictions conflict with these principles (e.g. vegan + high animal protein), the dietary restriction always wins. Adapt the principle, don't override the user's choice.

---

## Dietary restriction matrix

The app must support any combination of these restrictions simultaneously:

| Restriction | Key avoidances | Key substitutions |
|---|---|---|
| Vegan | All animal products | Tofu, tempeh, legumes, seeds, nutritional yeast |
| Vegetarian | Meat & fish | Eggs, dairy allowed; same plant proteins as vegan |
| Gluten-free | Wheat, barley, rye, spelt | Rice, oats (certified GF), quinoa, buckwheat |
| Dairy-free | Milk, cheese, butter, whey | Coconut oil, nut milks, olive oil, cashew cheese |
| Carnivore | All plants | Meat, fish, eggs, animal fats only |
| Keto / low-carb | Grains, sugar, starchy veg | Cauliflower rice, zucchini noodles, full-fat dairy |

**Combination rules:**
- Vegan + GF: emphasise rice, quinoa, lentils, chickpeas, nuts, seeds
- Vegan + Keto: very hard to do well — include a user-facing note that this is nutritionally challenging; still generate the plan but flag high-fat plant sources (avocado, coconut, nuts)
- Carnivore + anything plant-based: mutually exclusive — surface a conflict warning to the user

---

## Product output spec

Every generated plan must include all five of these components:

### 1. 7-day meal plan
- Three meals per day: breakfast, lunch, dinner
- Optional: one snack slot per day (user toggle)
- Format: day → meal → dish name + 2-line description
- Each meal tagged with: prep time, key nutrients, dietary labels

### 2. Shopping list
- Organised by category: Proteins, Produce, Pantry, Dairy/Alternatives, Supplements
- Quantities scaled to household size (1–6 people)
- Highlight items that serve methylation support with a ✦ marker

### 3. Recipes with instructions
- Each recipe: ingredient list (scaled) + step-by-step method (max 6 steps)
- Include one "why this food" note per recipe linking to a Brecka principle
- Reading level: clear, conversational, no jargon

### 4. Macros & nutritional info
- Per meal: calories, protein (g), carbs (g), fat (g)
- Per day: totals + % of estimated daily needs (based on user-provided weight/goal if available)
- Call out key micronutrients where relevant (B12, folate, Omega-3, Zinc)

### 5. Supplement recommendations
- Weekly supplement stack tailored to dietary restrictions and goals
- Format: supplement name → why it's recommended → suggested timing
- Flag any supplements that are especially critical for the user's restriction (e.g. B12 for vegans is always mandatory)
- Do not recommend specific brands — keep it generic

---

## User inputs (required to generate a plan)

| Input | Type | Required |
|---|---|---|
| Household size | Number (1–6) | Yes |
| Dietary restrictions | Multi-select | Yes (can be "none") |
| Health goal | Single select: Energy / Weight loss / Muscle / Longevity / General health | Yes |
| Eating window preference | Toggle: Standard (8–10hr) / Flexible | Optional |
| Allergies or foods to avoid | Free text | Optional |
| Current weight (for macro scaling) | Number | Optional |

---

## UX principles

The app must feel immediately familiar. Use established, well-understood UX patterns — no clever reinventions.

### Core UX rules
- **Progressive disclosure:** show the minimum needed at each step; reveal complexity only when the user asks for it. Onboarding = 3 steps max.
- **Defaults do the work:** pre-select sensible defaults for every input so the user can generate a plan in under 60 seconds without filling in everything
- **Forgiving inputs:** never block progress with validation errors; warn softly, allow override
- **Clear primary action:** every screen has one obvious next step (one CTA, visually dominant)
- **Instant feedback:** every tap/click should produce a visible response within 100ms (loading states, button press states)
- **Familiar navigation patterns:** bottom nav or top nav — nothing custom or hidden; no hamburger menus for primary actions
- **Empty states earn their keep:** if no plan exists yet, the empty state explains what the user will get and has a prominent CTA — never a blank screen

### Onboarding flow (3 steps)
1. **Who are you eating for?** — household size + dietary restrictions (multi-select chips)
2. **What's your goal?** — single select: Energy / Weight loss / Muscle / Longevity / General health
3. **Generate** — one big button; plan appears immediately with a loading skeleton

No sign-up required to generate a first plan. Paywall appears only when the user tries to access the full output.

### Mobile-first
All layouts designed for 375px width first. Desktop is a bonus, not a requirement for v1.

---

## Personalisation & learning

The app should get smarter with each interaction, building a preference profile that improves future plans.

### What the app learns
| Signal | How it's captured | How it's used |
|---|---|---|
| Meal ratings (👍/👎) | Inline on each meal card | Avoid disliked meals; surface liked ones in future plans |
| Skipped meals | "Skip this meal" action | Treat as implicit dislike; log the pattern |
| Regenerated meals | "Regenerate this meal" action | Treat as dislike; ask optional "why?" (too complex / don't like ingredients / other) |
| Saved recipes | Bookmark action | Prioritise these ingredients/styles in future plans |
| Explicit preferences | Free text in profile | Ingest as hard constraints ("I hate cilantro", "I love spicy food") |
| Plan completion | Did the user come back next week? | Proxy signal for overall satisfaction |

### Preference profile (stored per user)
```
{
  liked_ingredients: [],
  disliked_ingredients: [],
  liked_cuisines: [],
  disliked_meals: [],        // meal IDs or dish names
  complexity_preference: "simple" | "moderate" | "adventurous",
  explicit_notes: ""         // free text passed into generation prompt
}
```

### How learning feeds into generation
Every plan generation call includes the user's preference profile in the system prompt. The model is instructed to:
- Never repeat a disliked meal within a 4-week window
- Weight liked cuisines and ingredients positively
- Match complexity preference
- Treat explicit notes as hard constraints

For v1, the preference profile is stored in browser `localStorage`. No account required. In v2, sync to a user account for cross-device persistence.

---

## Feedback feature

Feedback is built into the product at three levels — passive (ratings), active (text), and aggregate (NPS-style).

### Level 1 — per-meal rating (passive, always visible)
- Every meal card has a 👍 / 👎 toggle
- One tap — no modal, no friction
- Stored in preference profile immediately
- Visual confirmation: icon fills on tap

### Level 2 — plan-level feedback (active, shown after 3 days)
- A soft prompt appears after the user has had the plan for 3 days: *"How's your plan going?"*
- Three quick options: Great / It's OK / Not for me
- Selecting "Not for me" opens a short optional text field: *"What wasn't working?"*
- Dismiss is always available — never block the user

### Level 3 — post-generation micro-survey (optional, shown once per week)
- After generating a new plan: *"Anything we should know for next time?"*
- Free text, max 280 chars
- Stored in preference profile as `explicit_notes`
- Shown maximum once per week — never spammy

### Feedback data use
- Levels 1 & 2 feed directly into the personalisation profile (see above)
- Level 3 text is passed verbatim into the next generation prompt
- Aggregate feedback (thumbs up/down ratios, plan ratings) surfaces in a simple "Your taste profile" screen showing what the app has learned about you

### Feedback UI principles
- Never interrupt a task to ask for feedback
- Always dismissible with one tap
- Confirmatory — acknowledge when feedback is received ("Got it, we'll keep that in mind")
- Never guilt-trip about skipping feedback

---

## Design language

### Tone
- Warm, confident, and practical — like a nutritionist friend
- Never preachy, never guilt-inducing
- Use second person ("your plan", "you'll get", "your body")
- Short sentences. Active voice. No filler phrases.

### Visual style: warm & natural
- **Colour palette:** warm off-whites, deep forest greens, terracotta/clay accents, warm amber
- **Typography:** humanist sans-serif (e.g. Inter or DM Sans); generous line height
- **Imagery direction:** real food photography aesthetic — not studio-perfect, natural light, wooden surfaces, herbs
- **UI feel:** clean cards, soft borders, earthy tones — not clinical white, not neon biohacker aesthetic
- **Icons:** simple line icons; leaf, sun, clock, protein motifs

### Key UI components
- Meal card: dish name, meal type badge, prep time, macro pills, dietary tags
- Day row: collapsible, shows all three meals
- Shopping list: grouped accordion with checkboxes
- Supplement card: name, timing badge, reason
- Conflict warning: amber banner for impossible dietary combos

---

## Monetisation (v1 approach)
- **Free:** generate one plan (limited — no recipes, no macros)
- **Paid (one-time or subscription):** full plan with all 5 components, unlimited regeneration, household scaling
- Pricing TBD — suggested range €4.99 one-time / €7.99/month
- No ads. Product should feel premium even at free tier.

---

## Technical approach (no-code first)

Since the builder is non-technical, v1 should be built using:
- **Plan generation:** Claude API (via Claude-in-artifact or direct API calls)
- **Frontend:** React artifact or simple HTML/CSS — no backend required for v1
- **Distribution:** Gumroad, Lemon Squeezy, or direct link share
- **Payments:** handled by distribution platform
- **No database required for v1** — stateless generation per session

Avoid: Next.js, databases, auth systems, or anything requiring a server for v1.

---

## PM documentation checklist

When working on this product, always maintain:
- [ ] Feature decisions log (what was cut from v1 and why)
- [ ] User feedback notes (post-launch)
- [ ] Iteration changelog (v1 → v2 changes with rationale)
- [ ] Metrics to track: plans generated, conversion free→paid, repeat visits

This is a live portfolio artefact — document decisions as they happen.

---

## Out of scope for v1
- User accounts / saved plans
- Calendar integration
- AI chat / plan adjustment after generation
- Grocery delivery integration
- Social sharing
- Mobile app (web-first)

These are v2+ features. Do not build them until v1 is validated.
