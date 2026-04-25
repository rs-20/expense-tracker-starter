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

React 19 + Vite app with no routing or state management libraries. `src/App.jsx` is the root and owns the `transactions` array as the single source of truth, passing it down to three components:

- **`Summary`** — receives `transactions`, computes `totalIncome`, `totalExpenses`, and `balance` internally.
- **`TransactionForm`** — owns its own form field state (description, amount, type, category); calls `onAdd(transaction)` prop when submitted.
- **`TransactionList`** — receives `transactions`, owns filter state (filterType, filterCategory) internally, applies filters in render via chained `.filter()`.

`categories` is defined locally in both `TransactionForm` and `TransactionList`.

**State shape:** Each transaction is `{ id, description, amount (number), type ("income"|"expense"), category, date }`.

**Known intentional issues (part of a course):**
- **Data:** `"Freelance Work"` is seeded as `type: "expense"` but `category: "salary"` — likely intentional course material.
- **UI:** Minimal styling; a `.delete-btn` CSS class exists in `App.css` but no delete functionality is wired up yet.
