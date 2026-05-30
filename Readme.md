# Padre's Pantry 🫒

Mediterranean meal plan site for a 67M, 190lb, lightly active, Type 2 diabetic.

**Macro targets:** ~1,900 kcal · ~130g protein · ~170g low-GI carbs · ~75g fat · 33g+ fiber

## Repo structure

```
padres-pantry/
├── index.html          ← Single-file React app (no build step needed)
├── nutrition.json      ← Nutrition database (edit once, applies everywhere)
└── weeks/
    ├── 2026-W23.json   ← Current week
    └── 2026-W24.json   ← Add new weeks here
```

## Running locally

```bash
# Any static file server works. Easiest:
npx serve .

# Or with Python:
python3 -m http.server 8080
```

Then open `http://localhost:8080` (or whatever port).

> ⚠️ Must be served — can't open index.html directly as a file:// URL because of the JSON fetch calls.

## Deploying

Works on any static host:
- **GitHub Pages** — push to `main`, enable Pages in repo settings, point at `/` (root). Done.
- **Netlify** — drag the folder into netlify.com/drop
- **Vercel** — `vercel` in the project folder

## Adding a new week

1. Duplicate `weeks/2026-W23.json` → rename to `weeks/2026-W24.json`
2. Update all meal content, macros, shopping list
3. Add the new week to `WEEK_REGISTRY` at the top of `index.html`:
   ```js
   const WEEK_REGISTRY = [
     { id: "2026-W23", label: "Week of June 1, 2026" },
     { id: "2026-W24", label: "Week of June 8, 2026" },  // ← add this
   ];
   ```
4. The new week auto-becomes "This Week"; old week moves to Past Weeks.

## Nutrition database

`nutrition.json` contains per-ingredient macros and micros. Add new ingredients as needed — format matches existing entries. The `_dri` section at the bottom sets Padre's daily reference intakes for the micronutrient panel.

## Week JSON structure

Each week file supports:
- `breakfasts` — array of breakfast options with `days`, `name`, `macros`, `ingredients`, `steps`
- `lunches` — same structure
- `dinners` — array indexed by day, same structure
- `snacks` — array of snack options with `name`, `macros`, `desc`
- `shopping` — object with category keys → string array
- `targets` — macro breakdown table for Nutrition tab
- `macros` — weekly average macro targets
- Ingredient `substitutions` — swap button support (see sardines in W23 for example)

## T2D dietary notes

- Carb sources are always **low-GI**: lentils, chickpeas, quinoa, farro, vegetables
- No refined grains (white rice, white pasta) — swap to farro or quinoa
- No added sugar
- Healthy fat emphasis: olive oil, salmon, sardines, walnuts, almonds
- No raw onion (preference)
- Fiber target: 30g+ per day for blood sugar stability
