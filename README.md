# GeneFeed

> Your personalised weekly meal plan, supplement guide, and recipe book — built on biohacking science, tailored to how you actually eat.

GeneFeed removes food decision fatigue. Tell it your household size, dietary needs, and health goal. It hands you a complete week: 21 meals, full recipes, a scaled shopping list, macros, and a supplement stack — all built on Gary Brecka's biohacking principles.

---

## What it does

- **7-day meal plan** — breakfast, lunch, and dinner every day, with prep times and descriptions
- **Full recipes** — ingredients, step-by-step method, and a "why this food" note linked to a biohacking principle
- **Scaled shopping list** — organised by category (Proteins, Produce, Pantry, etc.), scaled to household size, with methylation support foods marked ✦
- **Macros & nutrients** — calories, protein, carbs, fat per meal; key micronutrients called out
- **Supplement stack** — personalised to your dietary restrictions and goal, with timing and reasoning

---

## How it learns

GeneFeed builds a preference profile from your behaviour:

| Signal | How captured |
|---|---|
| 👍 / 👎 per meal | Inline rating on each meal card |
| Explicit notes | Free text in your Profile tab |
| Weekly micro-survey | Optional prompt after each new plan |

Every new plan you generate includes your preference profile — liked meals, disliked meals, and hard constraints — so suggestions improve over time. Profile is stored in `localStorage` (no account needed).

---

## Dietary support

Supports any combination of: **Vegan · Vegetarian · Gluten-free · Dairy-free · Carnivore · Keto / low-carb**

Conflict detection built in (e.g. Carnivore + Vegan surfaces a warning).

---

## Tech stack

| Layer | Choice |
|---|---|
| Frontend | Vanilla HTML/CSS/JS — single file, zero dependencies |
| AI generation | Claude API (`claude-sonnet-4-20250514`) |
| Storage | Browser `localStorage` |
| Fonts | Fraunces (serif display) + DM Sans (body) via Google Fonts |
| Hosting | Any static host — Netlify, GitHub Pages, direct file share |

No backend. No database. No build step. Open `index.html` and it works.

---

## Running locally

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/genefeed.git
cd genefeed

# Open in browser
open index.html
```

The Claude API call is handled client-side. No API key setup needed when running via Claude.ai artifacts.

---

## Project structure

```
genefeed/
├── index.html        # The full application (single file)
├── README.md         # This file
├── CHANGELOG.md      # Version history and decision log
└── SKILL/
    └── SKILL.md      # Product definition, UX principles, design system
```

---

## Nutrition principles (Gary Brecka-inspired)

1. High protein, whole animal foods (or complete plant proteins for plant-based diets)
2. Zero ultra-processed ingredients
3. Methylation support — eggs, leafy greens, liver, legumes
4. Circadian eating — 8–10 hour eating window
5. Whole food sourcing — every ingredient recognisable as real food

Dietary restrictions always override these principles.

---

## Roadmap

### v1 (current)
- [x] 3-step onboarding
- [x] AI-generated 7-day plan
- [x] Recipes, shopping list, supplements
- [x] Per-meal feedback (👍/👎)
- [x] Preference profile with localStorage
- [x] Weekly micro-survey

### v2 (planned)
- [ ] User accounts + cross-device sync
- [ ] Regenerate individual meals
- [ ] Calendar / meal scheduling view
- [ ] Grocery delivery integration

---

## PM notes

This project is built as both a real product and a product management portfolio piece. The `SKILL/SKILL.md` file contains the full product definition — vision, user persona, feature spec, UX principles, and design language — written before a single line of code.

Decision log is maintained in `CHANGELOG.md`.

---

*Built with Claude · Inspired by Gary Brecka*
