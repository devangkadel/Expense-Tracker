# Monthly Expense Ledger

A personal expense tracker that runs as a Claude artifact. You log expenses by date, category and amount, and the page shows each month's total, a category breakdown, a six-month trend and every line item. Entries are saved to the artifact's own database, so they're still there when you come back on any device. Everything can be downloaded as a PDF report or an Excel workbook.

**Live page:** https://claude.ai/artifact/7HFukCnBJdagkyExVfGnXh

---

## Contents

- [Features](#features)
- [Getting started](#getting-started)
- [Using the ledger](#using-the-ledger)
- [Categories](#categories)
- [Currency](#currency)
- [Exports](#exports)
- [How data is stored](#how-data-is-stored)
- [Sharing and access](#sharing-and-access)
- [Technical overview](#technical-overview)
- [Known limitations](#known-limitations)
- [Troubleshooting](#troubleshooting)
- [Changelog](#changelog)

---

## Features

| Area | What it does |
|---|---|
| Add expenses | Date, description, category and amount, saved instantly |
| Edit expenses | Pencil icon on each line item loads it back into the form |
| Remove expenses | Two-click remove (click **Remove**, then **Confirm** within 3 seconds) |
| Month navigation | Step backwards and forwards through months with ‹ › |
| Summary tiles | Total spent, change vs. previous month, daily average, largest category, entry count, biggest single expense |
| Category breakdown | Donut chart plus a ranked legend with amounts, shares and bars |
| Six-month trend | Bar chart of monthly totals ending at the month shown |
| Line items | Every expense in the month, newest first, with weekday (e.g. *Mon, Nov 2*) |
| Export | Download all data as **PDF** or **Excel (.xlsx)** |
| Currency display | € EUR, $ USD, £ GBP, ₹ INR |
| Themes | Follows light / dark mode automatically |
| Responsive | Works on desktop, tablet and phone widths |

---

## Getting started

1. Open the live page while signed in to claude.ai.
2. Pick your currency in the top-right **Currency** selector.
3. Add your first expense in **Add an expense**.
4. Use ‹ › next to the month name to move between months.

No installation, account setup or configuration is needed.

---

## Using the ledger

### Adding an expense

| Field | Rules |
|---|---|
| Date | Required. Defaults to today. Decides which month the expense belongs to. |
| Description | Required, up to 80 characters. |
| Category | Pick one from the list (see [Categories](#categories)). |
| Amount | Required, greater than zero, rounded to 2 decimals. |

Click **Add expense**. If the date falls in a different month from the one on screen, the page jumps to that month.

### Editing an expense

1. In **Line items**, click the pencil icon on the row.
2. The form at the top switches to **Edit expense**, is highlighted, and the row is shaded.
3. Change any field and click **Save changes**.
4. To back out, click **Cancel** or press **Esc**.

Changing the date to another month moves the expense to that month.

### Removing an expense

Click **Remove**, then click **Confirm** within 3 seconds. Removal is permanent.

### Example entries

When first created, the ledger came with sample entries tagged **example**. If any are still present, a **Remove example entries** link appears in the Line items header (click it twice to confirm).

### Reading the summary

- **Total spent** is the sum for the month shown. The line underneath compares it with the previous month (red = higher spending, green = lower).
- **Daily average** divides the total by the days elapsed so far (current month) or by all days (past months). Future months show "—".
- **Largest category** is the category with the highest total and its share of the month.
- **Entries** is the number of expenses, plus the biggest single one.

---

## Categories

| # | Category |
|---|---|
| 1 | Housing |
| 2 | Groceries |
| 3 | Dining out |
| 4 | Transport |
| 5 | Utilities |
| 6 | Health |
| 7 | Entertainment |
| 8 | Shopping |
| 9 | Subscriptions |
| 10 | Miscellaneous |
| 11 | Other |

Each category has a fixed color, used in both the chart and the line-item chips, in light and dark themes.

---

## Currency

The **Currency** selector changes the symbol shown, not the stored numbers. No exchange rates are applied. It's a display preference saved in your browser, so other people viewing the page, or you on another device, may see a different symbol.

| Option | Symbol in page and Excel | Code in PDF |
|---|---|---|
| Euro | € | EUR |
| US dollar | $ | USD |
| British pound | £ | GBP |
| Indian rupee | ₹ | INR |

---

## Exports

The **Download PDF** and **Download Excel** buttons sit in the **Line items** header. Both export **every month**, not only the one on screen. Your browser asks you to confirm each download.

Files are named `expense-ledger-YYYY-MM-DD.pdf` / `.xlsx`, using today's date.

### PDF report (A4)

1. Title, date range covered, currency and export date
2. Headline tiles: total spent, number of expenses, number of months, largest category
3. **Spending by month**: entries and total per month, with a grand total
4. **Spending by category**: entries, total and share
5. **All expenses**: grouped by month (newest first), with date, day, description, category and amount
6. Footer with page numbers on every page

### Excel workbook

| Sheet | Contents |
|---|---|
| Expenses | Date, Day, Month, Description, Category, Amount. Real Excel dates, currency formatting, column filters, and a `SUM` total row. |
| By month | Entries and total per month, with `SUM` totals |
| By category | Entries, total and share (%) per category |
| Month x category | Grid of months × categories with row totals |

---

## How data is stored

Expenses live in the artifact's built-in database, in a collection called `expenses`. Each expense is one document:

```json
{
  "date": "2026-11-02",
  "month": "2026-11",
  "desc": "Weekly groceries",
  "category": "Groceries",
  "amount": 86.4,
  "createdAt": 1793620403436,
  "updatedAt": 1793948764000,
  "example": true
}
```

| Field | Type | Notes |
|---|---|---|
| `date` | string `YYYY-MM-DD` | Date of the expense |
| `month` | string `YYYY-MM` | Derived from `date`. Used to group by month. |
| `desc` | string | Description, up to 80 characters |
| `category` | string | One of the categories above |
| `amount` | number | Two-decimal value, no currency attached |
| `createdAt` | number (ms since epoch) | Set when added |
| `updatedAt` | number (ms since epoch) | Set when edited (optional) |
| `example` | boolean | Only on sample entries (optional) |

- Data survives page reloads, republishes of the artifact, and switching devices.
- Changes show up live in every open copy of the page.
- The database holds up to 25,000 documents, which is many years of daily entries.
- The only thing kept in browser storage is the currency choice.

---

## Sharing and access

- The ledger is **private** by default: only the owner can open it.
- To share it, use the **Share** menu on the artifact page.
- People given **Contributor** (or higher) access can add, edit and remove entries in the same shared ledger.
- **Viewers** and **Commenters** can see the data but can't change it.
- Everyone with access sees the same expenses. There are no per-person ledgers.

---

## Technical overview

| Piece | Details |
|---|---|
| Format | Single self-contained HTML page (markup, CSS and JS in one file) |
| Storage | Artifact `db` capability (realtime document store) |
| Downloads | Artifact `downloads` capability (viewer-confirmed file saves) |
| Charts | Hand-drawn inline SVG. No chart library. |
| Excel export | [SheetJS](https://sheetjs.com/) `xlsx` 0.18.5, loaded only when exporting |
| PDF export | [jsPDF](https://github.com/parallax/jsPDF) 2.5.1 + [jspdf-autotable](https://github.com/simonbengtsson/jsPDF-AutoTable) 3.8.2, loaded only when exporting |
| Library hosting | cdnjs, with jsDelivr as fallback |
| Fonts | Instrument Sans (text) and Spline Sans Mono (numbers) from Google Fonts, with system fallbacks |
| Theming | CSS custom properties with light/dark variants, following the viewer's theme |

Declared capabilities:

```json
{ "db": {}, "downloads": true }
```

---

## Known limitations

- **No currency conversion.** Switching currency only changes the symbol.
- **PDF uses currency codes.** The PDF's built-in font can't display symbols like ₹, so amounts read e.g. `INR 26,000.00`.
- **Fixed category list.** New categories have to be added to the page's code. Ask Claude to add one.
- **No recurring expenses, budgets or income tracking** yet.
- **No import.** Expenses can't be uploaded from a CSV or Excel file yet.
- **Exports need internet access** to load the PDF/Excel libraries on first use.
- **Signed-out viewers** can't load or save data.

---

## Troubleshooting

| Problem | What to do |
|---|---|
| "Saving isn't available in this view" banner | Open the page while signed in to claude.ai, directly rather than in a preview. |
| "Lost the connection to your saved expenses" | Reload the page. |
| Download buttons don't appear | Downloads aren't available in this view. Open the artifact page directly. |
| "Couldn't load the export tools" | Check your internet connection or ad/script blocker, then try again. |
| "A download prompt is already open" | Accept or dismiss the open prompt first. |
| Download cancelled | You declined the browser's save prompt. Click the button again. |
| Wrong currency symbol on another device | The currency setting is per browser. Pick it again there. |
| "That expense no longer exists" while editing | Someone removed it in another tab or device. |

---

## Changelog

| Version | Date | Changes |
|---|---|---|
| 3 | 2026-11-06 | PDF and Excel export of all data. Pencil-icon editing. Redesigned currency selector. Weekday shown in line-item dates. |
| 2 | 2026-11-02 | Added **Miscellaneous** category. |
| 1 | 2026-10-29 | First release: add/remove expenses, monthly summary, category donut, six-month trend, line items, currency selector, example entries. |
