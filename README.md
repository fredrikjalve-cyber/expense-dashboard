# Expense Dashboard

A one-page dashboard that answers a single question at a glance:
**where is our money going, and is anything moving in the wrong direction?**

## What it shows

From top to bottom, in order of importance:

1. **Verdict strip.** Total spend for the month, the change from the month
   before, and the fastest-growing category.
2. **Monthly spend trend.** Total spend per month as a line, with the
   fastest-growing category drawn against it.
3. **Where the money went.** Spend by category for the month, largest first,
   with each category's change from the month before.
4. **All expenses.** Every expense in the data, filterable by category and
   month and sortable by amount.

Use the **Month** picker at the top to look at an earlier month. Clicking a
category bar lists that category's expenses in the table.

### How to read the signals

- One accent color (rust) is reserved for things moving in the wrong
  direction. Everything else is neutral.
- A category is labelled **growing fast** when it is up by more than 25% *and*
  by more than $100 from the month before. Both conditions must hold, so small
  amounts do not trigger it.
- The **fastest-growing category** is the one with the largest dollar increase
  from the month before, not the largest percentage.
- Possible duplicate charges are counted in the totals. An expense with no
  amount is counted as $0, and a note under the verdict strip says so.

## How it was built

This dashboard was built by directing [Claude Code](https://claude.com/claude-code)
in plain language. The person who made it does not write code: they described
what the dashboard should answer, approved a plan, and reviewed the result.
Claude Code wrote and tested the page.

It is a single self-contained file, `index.html`. It uses no outside
libraries, loads nothing from other websites, and has no tracking.

## The data

The expense data is built into `index.html` itself. There is no database and
no server: the page is the data.

The source is a CSV file with five columns:
`Date, Vendor, Category, Amount, Notes`.

### How the data gets refreshed

1. Open the dashboard in a browser.
2. Click **Load new file** (or drag the file onto the page) and choose the
   new expense CSV. Keep earlier months in the file so the month-to-month
   comparisons keep working.
3. Check the numbers, then click **Save updated dashboard**. This downloads a
   new `index.html` with the new data built in.
4. Replace the `index.html` in this repository with the downloaded one and
   commit it. Vercel publishes the change automatically within a minute or so.

Loading a file only changes what you see in your own browser. Nothing is
uploaded anywhere, and the published dashboard does not change until step 4.

The same applies to visitors: anyone can load their own CSV to try the
dashboard with their own numbers, and that file never leaves their computer.

### Messy files

The dashboard reads real-world exports defensively. It understands mixed date
formats, amounts written with `$`, `USD` or commas, and common alternative
category names (for example "SaaS" is counted as Software). Rows it cannot use,
such as a spreadsheet total line or a date it cannot be sure about, are left
out, and the note under the verdict strip says how many.

## What is in this repository

| File | Purpose |
|---|---|
| `index.html` | The dashboard, including its data |
| `README.md` | This file |
| `.gitignore` | Keeps raw expense files and working files from being committed by accident |
