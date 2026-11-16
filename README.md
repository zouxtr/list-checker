# List Checker

A small offline web app for competitive-programming practice lists.
Everything lives in one file — no server, no network, no dependencies.

## Opening

Open `index.html` with a double click (or `xdg-open index.html`). Works offline.

## Importing a list

Hit **+ Paste a list** and paste your text. The format is free-form:

```
CDQ:
    https://zerojudge.tw/ShowProblem?problemid=c571 -- count dominated points in 3D
    https://www.luogu.com.cn/problem/P3810 -- Three-Dimensional Partial Order

divide and conquer over time:
    https://arena.olimpiici.com/#/catalog/603/problem/101494 -- LTI 2022 A2 renovation
    RSOP J
```

Rules:

- A line ending in `:` → a group title.
- A line with a link → a checkbox. Text after `--` becomes a note on that link.
- A line with no link (e.g. `RSOP J`) → a plain note, no checkbox.
- Lines before the first group title land in “Uncategorized”.

The dialog shows the number of groups, links and notes it recognised before you import.
If the same list was already imported, you can open the old sheet or import it again.

## Working with a sheet

- **Checkbox** — click the box or the item text. Checked items get struck through.
- **open ↗** — opens the link in a new tab without changing the checkbox.
- **⌕ search** — filters by note, URL or domain.
- **hide completed** — hides checked items.
- The `2/4` labels next to each group title and the bar at the top show progress.

## Editing a sheet

### Title and date

- Click the **sheet title** at the top, or the pencil button on a card in the left rail.
- Change the title and/or the date-time, then **Save** (or press Enter). `Esc` cancels.
- The date drives the rail ordering and the calendar, so back-dating a sheet moves it to its new day.

### Contents (groups, links and notes)

Click **✎ edit contents** in the toolbar (or press `e`) to edit the sheet in place:

- Every group title becomes an editable field; **delete group** removes the group and everything in it.
- Every line gets a text field and a URL field. Changing the URL between a link and empty turns
  that line into a plain note and back again — so you can fix a typo, swap a link, or add a note.
- **×** deletes a single line, **+ link or note** appends one to that group, **+ group** adds a new group.
- Pressing **Enter** in a field adds a new line below; **↑/↓** move between fields.
- An invalid URL (e.g. `javascript:...`) is marked and not saved — other edits are kept immediately anyway.
- Everything is saved as you type. Press **✓ done editing**, `e`, or `Esc` to go back to the checklist.

## Sheets and calendar

- Imported sheets sit on the left, ordered by date (newest first; the `newest ↓` button flips it).
- **Calendar** marks the days you imported a sheet — the day gets a hand-drawn pencil circle. Click a day to list its sheets.
- The `×` on a card deletes that sheet (after confirmation).

## Dark mode

Click the moon button in the header (or press `d`) to switch between the paper look and a dark
“charcoal” look. The choice is remembered, and on first visit it follows your system preference.

## Saving and backups

Everything is saved automatically in the browser (`localStorage`) — checkmarks, sheets, ordering, theme.
Closing the tab or restarting the browser loses nothing.

- **Export** — downloads the whole archive as `list-checker-YYYY-MM-DD.json`.
- **Import** — restores sheets from such a file. Duplicate sheets (same content) are skipped.

If the browser blocks `localStorage` for `file://` pages the app tells you. In that case serve the
folder locally, e.g. `python3 -m http.server`, and open `http://localhost:8000`.

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| `n` | new import |
| `e` | toggle content editing for the current sheet |
| `d` | toggle dark mode |
| `/` | search |
| `1` / `2` | sheets / calendar |
| `Space` | check the focused checkbox |
| `Esc` | close the dialog, the title/date panel, or leave content editing |

## Printing

`Ctrl+P` prints the active sheet only — with its title and date, and without the rail, buttons,
calendar or edit controls. Works from dark mode too (always prints on white).

## Technical notes

- One file, ~330 KB, fonts embedded as base64 (offline-safe).
- Fonts: [Neucha](https://fonts.google.com/specimen/Neucha) for body text and
  [Caveat](https://fonts.google.com/specimen/Caveat) for headings — both with Cyrillic, OFL licensed.
- Parser self-tests: open `index.html#test` and check the console (12 checks).
- Data never leaves your machine — there are no outbound requests.
