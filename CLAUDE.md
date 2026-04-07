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

React + Vite app with no routing and no state management library. No persistence — data resets on page reload.

### Component tree

```
App
├── Summary
├── TransactionForm
└── TransactionList
```

**`App.jsx`** — holds the single source of truth: the `transactions` array in `useState`. Passes `transactions` down to all three children and provides `handleAdd` as `onAdd` to `TransactionForm`.

**`Summary.jsx`** — receives `transactions` and derives `totalIncome`, `totalExpenses`, and `balance` internally via `filter`/`reduce`.

**`TransactionForm.jsx`** — owns all form field state (description, amount, type, category). On submit, calls `onAdd` with a fully constructed transaction object (amount as `parseFloat`). Resets fields after adding.

**`TransactionList.jsx`** — receives `transactions` and owns its own `filterType`/`filterCategory` state internally, since filters don't need to be shared.

### Shared constants

`categories` array is currently duplicated in `TransactionForm.jsx` and `TransactionList.jsx`.

### Styling

Plain CSS in `src/App.css` (component styles) and `src/index.css` (global reset). Classes `income-amount`, `expense-amount`, and `balance-amount` are shared between `Summary` and the transaction table rows in `TransactionList`.
