# T-Minus

A web app with a live countdown to a trip departure and a packing checklist. Single user, single device, no accounts.

Full requirements live in `PRD.md`. That file is the source of truth for scope. This file is the source of truth for how to build it.

---

## Stack (locked — do not substitute)

- Vite + React + TypeScript
- Tailwind CSS
- `localStorage` for all persistence
- No other dependencies without asking first

If you think this project needs a library that isn't listed here, stop and ask before installing it.

---

## Explicitly out of scope

Do not build, scaffold, or suggest any of these:

- User accounts, login, signup, auth of any kind
- A backend, an API, a server, or a database (no Supabase, no Firebase, no Postgres)
- Multiple trips at once — the MVP is exactly one trip
- Custom categories beyond the three defaults
- Reusable templates, sharing, or push notifications

Everything above is in the PRD's "+" column. That means later, not now.

---

## Data model

Two types, both stored in `localStorage` under the single key `t-minus:v1`.

```ts
type Trip = {
  name: string;
  departsAt: string; // ISO 8601 datetime
};

type Item = {
  id: string;
  label: string;
  category: 'Essentials' | 'Clothes' | 'Electronics';
  packed: boolean;
};

type AppState = {
  trip: Trip | null;
  items: Item[];
};
```

`trip: null` means no trip has been set up yet — show the setup form.

Read state from `localStorage` once on mount. Write on every change. Wrap reads in try/catch, since stored data can be corrupt or absent, and fall back to a clean empty state rather than crashing.

---

## Build order

Build one slice at a time. Each slice must run in the browser and be visibly working before starting the next. Do not scaffold ahead.

1. **Scaffold.** Vite + React + TS + Tailwind. Renders a page saying "T-Minus". Confirm `npm run dev` works.
2. **Trip setup.** Form for trip name and departure date/time. Saves to `localStorage`. Survives a page refresh.
3. **Countdown.** Live days/hours/minutes remaining, ticking on its own. Uses the saved departure date.
4. **Starter checklist.** Seeded items in the three categories. Check and uncheck. Checked state persists.
5. **Add and delete.** Custom item into any category. Delete any item, seeded or custom.
6. **Unpacked count and zero state.** Count of remaining items. A clear "you're off" state when the countdown hits zero.
7. **Edit trip.** Change the trip name or departure date after setup without losing the checklist.
8. **Deploy.** Push to GitHub, deploy the static build.

Slices 1 through 7 cover every MVP requirement in the PRD. Nothing else is MVP.

---

## Working rules

- After each slice works, stop. Tell me what changed and what to click to verify it.
- Commit after each working slice, with a message naming the slice.
- Small files. One component per file, in `src/components/`.
- When something is ambiguous in the PRD, ask rather than assuming. Guessing wrong costs more than asking.
- Do not refactor working code unless asked.

---

## Decisions already made

These came up while planning. Don't re-litigate them.

- **Countdown granularity:** display days/hours/minutes, but re-render every second so the minutes roll over on time.
- **Seeded list:** keep it short, roughly six to eight items per category. Obvious things people forget — passport, charger, medication, adapter. A wall of forty items is worse than none.
- **Deleting seeded items:** allowed, same as custom ones. There's no distinction between them after setup.
- **Past dates:** if the entered departure is already in the past, show the "you're off" state rather than a negative countdown.
- **Re-seeding:** seed the starter list exactly once, at trip creation. Never re-seed after that. If the user deletes every item, the list stays empty across refreshes.
- **Zero state:** a full-screen takeover replacing the whole UI, with a "Show my list" button that reveals the checklist.
- **Editing after setup:** both the trip name and the departure date are editable. Slice 7 covers both, not just the date.
- **Adding items:** a small "+" input under each of the three category headings. Not one form with a category dropdown.
- **Unpacked count:** one global count in the header, not per-category. At zero it reads "All packed", not "0 items left".
- **Timezone:** device local time, with the offset baked in at save.
- **Deleting:** no confirmation, no undo. Reject empty or whitespace-only labels. Duplicate labels are allowed.
- **Starting over:** "clear the list and start a new trip" is not MVP. Do not add a reset button.
- **Deploy target:** Vercel. No Vite `base` config needed.
- **Past dates at setup:** the setup form rejects a departure datetime that is already in the past and shows an inline error. This narrows the "Past dates" rule above: the "you're off" state is reachable when a date passes while the app is in use, or after an edit — never straight out of first-run setup.
