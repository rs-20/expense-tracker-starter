# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev      # Start dev server at http://localhost:5173
npm run build    # Production build
npm run lint     # Run ESLint
npm run preview  # Preview production build
```

## Architecture

This is a single-component React app (Vite + React 19). All logic lives in `src/App.jsx` — there are no sub-components, routing, or state management libraries.

**Known intentional issues (part of a course):**
- **Bug:** `amount` is stored as a string, so `reduce` concatenates instead of summing — totals are wrong. Fix: parse to `Number(t.amount)` in the reduce calls.
- **Data:** `"Freelance Work"` is seeded as `type: "expense"` but `category: "salary"` — likely intentional course material.
- **UI:** Minimal styling; a `.delete-btn` CSS class exists in `App.css` but no delete functionality is wired up yet.

**State shape:** Each transaction is `{ id, description, amount (string), type ("income"|"expense"), category, date }`.

**Filtering:** Applied client-side in render via chained `.filter()` on the `transactions` array; no derived state is memoized.
