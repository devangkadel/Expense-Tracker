# Monthly Expense Ledger

A personal expense tracker for logging expenses by date, category, payment mode and amount, with an optional photo or PDF of the bill. For each month it shows the total, a category breakdown, a six-month trend and every line item. Everything can be downloaded as a PDF report or an Excel workbook.

It comes in two editions built from the same code:

| Edition | Where it runs | Where data is saved | Best for |
|---|---|---|---|
| **Claude edition** | As a Claude artifact on claude.ai | The artifact's own database and file storage. Shared across your devices and with anyone you give access. | Day-to-day use |
| **Standalone edition** (`index.html`) | Any browser or static host, e.g. GitHub Pages | Each visitor's own browser | Sharing for feedback, offline use |

**Live page (Claude edition):** https://claude.ai/artifact/7HFukCnBJdagkyExVfGnXh

---

## Contents

- [Features](#features)
- [Getting started](#getting-started)
- [Using the ledger](#using-the-ledger)
- [Categories](#categories)
- [Payment modes](#payment-modes)
- [Bills and receipts](#bills-and-receipts)
- [Currency](#currency)
- [Exports](#exports)
- [How data is stored](#how-data-is-stored)
- [Standalone edition and GitHub Pages](#standalone-edition-and-github-pages)
- [Sharing and access](#sharing-and-access)
- [Technical overview](#technical-overview)
- [Known limitations](#known-limitations)
- [Troubleshooting](#troubleshooting)
- [Changelog](#changelog)

---

## Features

| Area | What it does |
|---|---|
| Add expenses | Date, description, category, payment mode and amount, saved instantly |
| Payment mode | Grouped dropdown: cash, cards, online, bank and other methods |
| Bill / receipt upload | Attach a JPG, JPEG, PNG, WEBP or PDF of up to 2 MB to any expense |
| View bills | Paperclip icon on the line item opens the bill in a viewer, with a Download button |
| Edit expenses | Pencil icon loads an expense back into the form, including its bill |
| Remove expenses | Two-click remove (click **Remove**, then **Confirm** within 3 seconds). Also deletes the bill. |
| Month navigation | Step backwards and forwards through months with ‹ › |
| Summary tiles | Total spent, change vs. previous month, daily average, largest category, entry count, biggest single expense |
| Category breakdown | Donut chart plus a ranked legend with amounts, shares and bars |
| Six-month trend | Bar chart of monthly totals ending at the month shown |
| Line items | Date with weekday (e.g. *Mon, Nov 2*), description, category, payment mode and amount |
| Export | Download all data as **PDF** or **Excel (.xlsx)** |
| Currency display | € EUR, $ USD, £ GBP, ₹ INR |
| Themes | Follows light / dark mode automatically |
| Responsive | Works on desktop, tablet and phone widths |

---

## Getting started

**Claude edition**
1. Open the live page while signed in to claude.ai.
2. Pick your currency in the top-right **Currency** selector.
3. Add your first expense in **Add an expense**.

**Standalone edition**
1. Open `index.html` in any modern browser (double-click it), or host it as shown in [Standalone edition and GitHub Pages](#standalone-edition-and-github-pages).
2. It starts empty. Add your first expense.

No installation, account or configuration is needed for either edition.

---

## Using the ledger

### Adding an expense

| Field | Required | Rules |
|---|---|---|
| Date | Yes | Defaults to today. Decides which month the expense belongs to. |
| Description | Yes | Up to 80 characters |
| Category | Yes | See [Categories](#categories) |
| Payment mode | No | See [Payment modes](#payment-modes). Defaults to *Not specified*. |
| Amount | Yes | Greater than zero, rounded to 2 decimals |
| Bill / receipt | No | One file, JPG / JPEG / PNG / WEBP / PDF, 2 MB max. See [Bills and receipts](#bills-and-receipts). |

Click **Add expense**. If a bill is attached, the button shows **Uploading…** until the file is saved. If the date falls in a different month from the one on screen, the page jumps to that month. Category and payment mode stay selected after adding, which speeds up entering several similar expenses.

### Editing an expense

1. In **Line items**, click the pencil icon on the row.
2. The form switches to **Edit expense**, is highlighted, and the row is shaded.
3. Change any field. For the bill you can:
   - keep it (shown as *filename (attached)*),
   - replace it with **Replace**,
   - remove it with **×**.
4. Click **Save changes**, or **Cancel** / **Esc** to leave it unchanged.

### Removing an expense

Click **Remove**, then **Confirm** within 3 seconds. The expense and its attached bill are both permanently deleted.

### Example entries

If sample entries tagged **example** are present, a **Remove example entries** link appears in the Line items header (click it twice to confirm).

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

## Payment modes

| Group | Option in the dropdown | Saved as |
|---|---|---|
| — | Not specified | *(empty)* |
| — | Cash | `Cash` |
| Cards | Debit card | `Debit card` |
| Cards | Credit card | `Credit card` |
| Cards | Prepaid / forex card | `Prepaid card` |
| Online | UPI | `UPI` |
| Online | Net banking | `Net banking` |
| Online | Mobile wallet | `Mobile wallet` |
| Bank | Bank transfer (NEFT / RTGS / IMPS) | `Bank transfer` |
| Bank | Auto-debit (EMI / standing instruction) | `Auto-debit` |
| Bank | Cheque | `Cheque` |
| Bank | Demand draft | `Demand draft` |
| Other | Pay later / BNPL | `Pay later` |
| Other | Gift card / voucher | `Gift card / voucher` |
| Other | Other | `Other` |

The payment mode shows in the **Paid via** column, and both exports summarize spending by payment mode. Expenses saved before payment mode existed show "—" until edited.

---

## Bills and receipts

| Rule | Value |
|---|---|
| Accepted formats | `.jpg`, `.jpeg`, `.png`, `.webp`, `.pdf` |
| Maximum size | 2 MB per file |
| Files per expense | 1 |

- Files that are too large, empty or in another format are refused before upload, with a message saying why.
- Click the **paperclip** icon on a line item to open the bill:
  - **Images** show inside the viewer.
  - **PDFs** show inside the viewer in the standalone edition. In the Claude edition they open in a new tab or download.
- **Download** in the viewer saves the original file.
- Close the viewer with **×**, **Esc**, or a click outside it.
- Phone camera photos (HEIC) aren't accepted. Most phones can share or save a photo as JPG.

---

## Currency

The **Currency** selector changes the symbol shown, not the stored numbers. No exchange rates are applied. It's a display preference saved in your browser.

| Option | Symbol in page and Excel | Code in PDF |
|---|---|---|
| Euro | € | EUR |
| US dollar | $ | USD |
| British pound | £ | GBP |
| Indian rupee | ₹ | INR |

---

## Exports

The **Download PDF** and **Download Excel** buttons sit in the **Line items** header. Both export **every month**, not only the one on screen. Files are named `expense-ledger-YYYY-MM-DD.pdf` / `.xlsx`.

The exports list bill file names but don't include the bill files themselves. Download those from the viewer.

### PDF report (A4)

1. Title, date range covered, currency and export date
2. Headline tiles: total spent, number of expenses, number of months, largest category
3. **Spending by month**: entries and total per month, with a grand total
4. **Spending by category**: entries, total and share
5. **Spending by payment mode**: entries, total and share
6. **All expenses**: grouped by month (newest first) with date, day, description, category, paid via and amount. Expenses with an attached bill are marked **[bill]**.
7. Page numbers on every page

### Excel workbook

| Sheet | Contents |
|---|---|
| Expenses | Date, Day, Month, Description, Category, Payment mode, Amount, Bill / receipt (file name). Real Excel dates, currency formatting, column filters, and a `SUM` total row. |
| By month | Entries and total per month, with `SUM` totals |
| By category | Entries, total and share (%) per category |
| By payment mode | Entries, total and share (%) per payment mode |
| Month x category | Grid of months × categories with row totals |

---

## How data is stored

Each expense is one document:

```json
{
  "date": "2026-11-02",
  "month": "2026-11",
  "desc": "Weekly groceries",
  "category": "Groceries",
  "payment": "UPI",
  "amount": 86.4,
  "receipt": {
    "id": "a1b2c3d4e5f6a7b8c9d0e1f2a3b4c5d6",
    "name": "dmart-bill.jpg",
    "type": "image/jpeg",
    "size": 482113
  },
  "createdAt": 1793620403436,
  "updatedAt": 1793948764000
}
```

| Field | Type | Notes |
|---|---|---|
| `date` | string `YYYY-MM-DD` | Date of the expense |
| `month` | string `YYYY-MM` | Derived from `date`. Used to group by month. |
| `desc` | string | Up to 80 characters |
| `category` | string | One of the categories above |
| `payment` | string or `null` | One of the saved values above. Missing on older entries. |
| `amount` | number | Two-decimal value, no currency attached |
| `receipt` | object or `null` | Pointer to the stored bill: `id`, original `name`, MIME `type`, `size` in bytes |
| `createdAt` | number (ms since epoch) | Set when added |
| `updatedAt` | number (ms since epoch) | Set when edited (optional) |
| `example` | boolean | Only on sample entries (optional) |

### Where each edition keeps it

| | Claude edition | Standalone edition |
|---|---|---|
| Expenses | Artifact database, collection `expenses` | Browser `localStorage`, key `expense-ledger:v1:expenses` |
| Bill files | Artifact file storage, served at `/_blob/<id>` | Browser IndexedDB, database `expense-ledger`, store `receipts` |
| Currency choice | Browser `localStorage` | Browser `localStorage` |
| Shared across devices | Yes | No |
| Live updates between open tabs | Yes | Yes (same browser) |

Bills are uploaded before the expense is saved, so an expense never points at a missing file. If saving fails, the just-uploaded file is cleaned up.

---

## Standalone edition and GitHub Pages

`index.html` is a single file with no server, build step or account needed. It starts empty, and each visitor gets their own private ledger in their browser.

### Publish on GitHub Pages (free)

1. On github.com, create a new **public** repository, e.g. `expense-ledger`. Pages on private repositories needs a paid plan.
2. **Add file → Upload files**, upload `index.html` (keep that name) and this `README.md`, then commit.
3. Go to **Settings → Pages**, choose **Deploy from a branch**, branch **main**, folder **/(root)**, and click **Save**.
4. After a minute or two the page is live at `https://<your-username>.github.io/expense-ledger/`.

### Collecting feedback

- Testers with a GitHub account can leave comments in the repository's **Issues** tab.
- A tester can send an Excel or PDF export to show exactly what they entered.

### What testers should know

- Data stays in their browser only. Nothing is sent to you or anyone else.
- Clearing browser data, or using a private window, deletes their expenses and bills. A banner warns them when the browser is blocking storage.
- Data doesn't move between browsers or devices.

---

## Sharing and access (Claude edition)

- The ledger is **private** by default: only the owner can open it.
- To share it, use the **Share** menu on the artifact page. Because it stores bill files, it can be shared within your organization but not through a public link.
- **Contributors** and above can add, edit and remove entries.
- **Editors** and the owner can upload bills. Others can view existing bills but won't see the upload field.
- **Viewers** and **Commenters** can see the data but can't change it.
- Everyone with access sees the same expenses. There are no per-person ledgers.

---

## Technical overview

| Piece | Details |
|---|---|
| Format | Single self-contained HTML page (markup, CSS and JS in one file) |
| Charts | Hand-drawn inline SVG. No chart library. |
| Excel export | [SheetJS](https://sheetjs.com/) `xlsx` 0.18.5 |
| PDF export | [jsPDF](https://github.com/parallax/jsPDF) 2.5.1 + [jspdf-autotable](https://github.com/simonbengtsson/jsPDF-AutoTable) 3.8.2 |
| Library loading | Only when exporting, from cdnjs with jsDelivr as fallback |
| Fonts | Instrument Sans (text) and Spline Sans Mono (numbers) from Google Fonts, with system fallbacks |
| Theming | CSS custom properties with light/dark variants |

**Claude edition capabilities:**

```json
{ "db": {}, "downloads": true, "assets": {} }
```

- `db`: expense records
- `assets`: bill files
- `downloads`: PDF / Excel / bill downloads

**Standalone edition:** the same code with small adapters that use `localStorage` for expenses, IndexedDB for bills, and the browser's native file download.

---

## Known limitations

- **No currency conversion.** Switching currency only changes the symbol.
- **PDF uses currency codes.** The PDF's built-in font can't display symbols like ₹, so amounts read e.g. `INR 26,000.00`.
- **One bill per expense**, 2 MB max. HEIC photos aren't accepted.
- **Exports don't bundle bill files.** Download bills individually from the viewer.
- **Fixed category and payment mode lists.** Changes need a code update.
- **No recurring expenses, budgets, income or split payments** yet.
- **No import** from CSV or Excel yet.
- **Exports need internet access** to load the PDF/Excel libraries on first use.
- **Standalone edition** data is per browser and can be lost if browser data is cleared. Export regularly as a backup.

---

## Troubleshooting

| Problem | What to do |
|---|---|
| "Bills must be 2 MB or smaller" | Compress the image, crop it, or take the photo at a lower resolution |
| "isn't a supported file" | Save or convert the bill to JPG, PNG, WEBP or PDF |
| Bill / receipt field missing (Claude edition) | Only people who can edit the artifact can upload. Ask the owner for Editor access. |
| "Couldn't upload the file" | Check your connection and try again |
| "Attachment storage is full" | Remove old expenses with bills you no longer need |
| PDF bill doesn't open inside the page (Claude edition) | Expected. Use **Open in new tab** or **Download** in the viewer. |
| "This file couldn't be found" | The bill was deleted, or browser data was cleared (standalone edition) |
| "Saving isn't available in this view" | Open the Claude edition directly while signed in to claude.ai |
| Storage warning banner (standalone edition) | You're in a private window or storage is blocked. Use a normal window. |
| Download buttons don't appear | Open the artifact page directly rather than in a preview |
| "Couldn't load the export tools" | Check your internet connection or ad/script blocker, then try again |
| "A download prompt is already open" | Accept or dismiss the open prompt first |
| "That expense no longer exists" while editing | It was removed in another tab or device |

---

## Changelog

| Version | Date | Changes |
|---|---|---|
| 4 | 2026-11-07 | **Payment mode** dropdown (15 options in 5 groups) and **Paid via** column. **Bill / receipt upload** (JPG, JPEG, PNG, WEBP, PDF, 2 MB max) with viewer and download. Payment-mode summaries in PDF and Excel. Bill file names in Excel. Dropdown arrows kept inside their fields. Standalone `index.html` edition for GitHub Pages. |
| 3 | 2026-11-06 | PDF and Excel export of all data. Pencil-icon editing. Redesigned currency selector. Weekday shown in line-item dates. |
| 2 | 2026-11-02 | Added **Miscellaneous** category |
| 1 | 2026-10-29 | First release: add/remove expenses, monthly summary, category donut, six-month trend, line items, currency selector, example entries |
