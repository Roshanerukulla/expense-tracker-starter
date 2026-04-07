# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install       # Install dependencies
npm run dev       # Start dev server at http://localhost:5173
npm run build     # Production build
npm run lint      # Run ESLint
npm run preview   # Preview production build
```

## Architecture

This is a single-file React app (no routing, no state management library). All logic lives in `src/App.jsx`:

- **State**: `transactions` array (id, description, amount, type, category, date) held in `useState`. No persistence — data resets on page reload.
- **Derived values**: `totalIncome`, `totalExpenses`, and `balance` are computed inline from `transactions` on every render. `amount` is stored as a string but used in arithmetic — this is an intentional bug in the starter.
- **Filtering**: `filterType` and `filterCategory` state produce `filteredTransactions` via inline filter chains; no separate filter component.
- **Form**: Controlled inputs; `handleSubmit` appends a new transaction and resets fields.
- **Styling**: Plain CSS in `src/App.css` (component styles) and `src/index.css` (global reset). CSS classes `income-amount`, `expense-amount`, and `balance-amount` are shared between the summary cards and the transaction table cells.

The app is intentionally a course starter — it has a known bug (string vs number arithmetic in totals), basic UI, and monolithic structure meant to be refactored during the course.
