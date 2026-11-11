# Monthly Expense Ledger

A personal expense tracker. You log expenses by date, category, payment mode and amount, with an optional photo or PDF of the bill. For each month it shows the total, an interactive category breakdown, a six-month trend and sortable line items. Everything can be downloaded as a PDF report or an Excel workbook.

People can use it in two ways:

- **Registered account (testing, max 10 users):** sign in with any email or mobile number and a demo code.
- **Continue without an account:** start tracking straight away, with expenses saved in that browser.

> **Testing version.** Sign-in codes are simulated and accounts aren't password-protected. Anyone who knows a registered email or number can open that account. Use dummy details and don't store anything sensitive.

It comes in two editions built from the same code:

| Edition | Where it runs | Registered accounts | Without an account |
|---|---|---|---|
| **Hosted edition** <!-- Claude edition: runs as a Claude artifact on claude.ai --> | As a hosted web page | Shared storage: works from **any browser or computer** | This browser only |
| **Standalone edition** (`index.html`) | Any browser or static host, e.g. GitHub Pages | **This browser only** (no shared database) | This browser only |

<!-- **Live page (Claude edition):** https://claude.ai/artifact/7HFukCnBJdagkyExVfGnXh -->

---

## Contents

- [Features](#features)
- [Getting started](#getting-started)
- [Accounts and sign-in](#accounts-and-sign-in)
- [Using the ledger](#using-the-ledger)
- [Categories](#categories)
- [Payment modes](#payment-modes)
- [Bills and receipts](#bills-and-receipts)
- [Currency](#currency)
- [Exports](#exports)
- [How data is stored](#how-data-is-stored)
- [Standalone edition and GitHub Pages](#standalone-edition-and-github-pages)
- [Sharing and access (hosted edition)](#sharing-and-access-hosted-edition)
- [Technical overview](#technical-overview)
- [Known limitations](#known-limitations)
- [Troubleshooting](#troubleshooting)
- [Changelog](#changelog)

---

## Features

| Area | What it does |
|---|---|
| Sign up / sign in | Email or mobile number plus a 6-digit demo code. Up to 10 registered users. |
| Continue without an account | Track expenses without signing in, saved in this browser |
| Account menu | Name, contact, user number, **Edit name**, **Sign out** |
| Add expenses | Date, description, category, payment mode and amount |
| Payment mode | Grouped dropdown: cash, cards, online, bank and other methods |
| Bill / receipt upload | Attach a JPG, JPEG, PNG, WEBP or PDF of up to 2 MB |
| View bills | Paperclip icon opens the bill in a viewer, with a Download button |
| Edit / remove | Pencil icon to edit (including the bill); two-click remove |
| Month navigation | ‹ › to step through months; **This month** jumps back |
| Summary tiles | Total spent, change vs. previous month, daily average, largest category, entry count, biggest expense |
| Category breakdown | Interactive donut: hover pops out a slice and shows its figures; click filters line items |
| Six-month trend | Bar chart of monthly totals; click a bar to open that month |
| Line items | Date with weekday (e.g. *Mon, Nov 2*), description, category, payment mode, amount |
| Sorting | Click any column heading to sort; click again to reverse. Remembered. |
| Search and filter | Search box, category filter chip, live count and total of what's shown |
| Export | Download all data as **PDF** or **Excel (.xlsx)** |
| Currency display | € EUR, $ USD, £ GBP, ₹ INR |
| Themes and layout | Light / dark mode; works on desktop, tablet and phone |

---

## Getting started

**Hosted edition** <!-- Claude edition -->
1. Open the live page while signed in<!-- to claude.ai -->. The owner must share it with you first.
2. Choose **Create account**, **Sign in**, or **Continue without an account**.

**Standalone edition**
1. Open `index.html` in a modern browser (double-click it), or host it as shown in [Standalone edition and GitHub Pages](#standalone-edition-and-github-pages).
2. Choose **Create account**, **Sign in**, or **Continue without an account**.

---

## Accounts and sign-in

### Creating an account

1. Choose **Create account**, enter your name and an email address or mobile number. Dummy details are fine.<!-- e.g. `user1@test.com` -->
2. A verification screen appears. In demo mode no message is sent; the code is shown on screen.
3. Enter the code. You're signed in, and you stay signed in on that browser for 30 days or until you sign out.

### Demo codes

Each registered user gets a code based on their user number:

| User | Code |
|---|---|
| 1 | `111111` |
| 2 | `222222` |
| 3 | `333333` |
| … | … |
| 9 | `999999` |
| 10 | `000000` |

After 5 wrong codes the attempt is cancelled and you start again.

### Signing in

Choose **Sign in**, enter the email or number you registered with, then the code. In the hosted edition<!-- Claude edition --> this works from any browser or computer, and you see the same expenses everywhere.

- Email addresses are not case-sensitive.
- For mobile numbers, the last 10 digits are matched, so `+91 98765 43210` and `9876543210` are the same account.

### The 10-user limit

Registration is capped at 10 accounts during testing (emails and mobile numbers count together). When all places are taken:

- the sign-in screen says so;
- anyone trying to sign up sees: *"Thanks for your interest! Registration is limited to 10 people during testing and every place is taken. You can still track expenses by choosing 'Continue without an account' below."*;
- registered users can still sign in.

### Continue without an account

- Expenses are saved in the current browser only, and never reach the shared storage.
- The account menu shows **Guest**, with **Sign in or create an account**. Your browser-only expenses stay there and come back the next time you choose *Continue without an account*.
- Clearing browser data, or using a private window, deletes them.

### Account menu

Click your name (top right) to see your name, email or number, and user number, plus:

- **Edit name:** changes the name shown on your account.
- **Sign out:** returns to the sign-in screen on this browser.

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
| Bill / receipt | No | One file, JPG / JPEG / PNG / WEBP / PDF, 2 MB max |

Click **Add expense**. The new row briefly lights up in Line items. If the date falls in another month, the page jumps there. Category and payment mode stay selected for the next entry.

### Editing and removing

- **Edit:** click the pencil icon, change any field (including replacing or removing the bill), then **Save changes**. **Cancel** or **Esc** backs out.
- **Remove:** click **Remove**, then **Confirm** within 3 seconds. The bill is deleted too.

### Sorting line items

| Column | First click | Second click |
|---|---|---|
| Date | Newest first | Oldest first |
| Description | A to Z | Z to A |
| Category | A to Z | Z to A |
| Paid via | A to Z | Z to A |
| Amount | Highest first | Lowest first |

Expenses without a payment mode always sit at the bottom of **Paid via**. Ties are broken by date, newest first. The sort is remembered in your browser.

### Searching and filtering

- **Search** matches description, category, payment mode, amount and date within the month shown.
- **Category filter:** click a donut slice or legend row to show only that category. Clear it with the chip's **×** or by clicking the category again.
- The toolbar shows the result, e.g. *6 of 30 shown · ₹1,131.00*.
- Search and filter only change what's on screen. Downloads always include everything.

### Exploring the charts

- **Hover** (or Tab to) a category: its slice pops out, others fade, and the centre shows its name, amount and share.
- **Click** a bar in **Last six months** (or press Enter on it) to open that month.
- **This month** appears whenever you're viewing another month.

### Reading the summary

- **Total spent:** the month's sum, with the change vs. last month (red = higher, green = lower).
- **Daily average:** total divided by days so far (current month) or all days (past months).
- **Largest category:** top category and its share.
- **Entries:** count, plus the biggest single expense.

---

## Categories

Housing · Groceries · Dining out · Transport · Utilities · Health · Entertainment · Shopping · Subscriptions · Miscellaneous · Other

Each category has a fixed color in the chart and line-item chips, in light and dark themes.

---

## Payment modes

| Group | Option | Saved as |
|---|---|---|
| — | Not specified | *(empty)* |
| — | Cash | `Cash` |
| Cards | Debit card / Credit card / Prepaid / forex card | `Debit card` / `Credit card` / `Prepaid card` |
| Online | UPI / Net banking / Mobile wallet | `UPI` / `Net banking` / `Mobile wallet` |
| Bank | Bank transfer (NEFT / RTGS / IMPS) | `Bank transfer` |
| Bank | Auto-debit (EMI / standing instruction) | `Auto-debit` |
| Bank | Cheque / Demand draft | `Cheque` / `Demand draft` |
| Other | Pay later / BNPL / Gift card / voucher / Other | `Pay later` / `Gift card / voucher` / `Other` |

---

## Bills and receipts

| Rule | Value |
|---|---|
| Accepted formats | `.jpg`, `.jpeg`, `.png`, `.webp`, `.pdf` |
| Maximum size | 2 MB per file |
| Files per expense | 1 |

- Files that are too large, empty or in another format are refused, with a message saying why.
- **Images** open inside the viewer.
- **PDFs** open inside the viewer in the standalone edition. In the hosted edition<!-- Claude edition --> they open in a new tab or download.
- HEIC phone photos aren't accepted; save or share them as JPG.
- **Hosted edition:**<!-- Claude edition --> only people with **Editor** access can upload bills. Others can view existing bills.
- **Standalone edition:** anyone can upload; bills are kept in that browser.

---

## Currency

The selector changes the symbol only. No conversion is applied, and the choice is saved per browser.

| Option | Symbol in page and Excel | Code in PDF |
|---|---|---|
| Euro | € | EUR |
| US dollar | $ | USD |
| British pound | £ | GBP |
| Indian rupee | ₹ | INR |

---

## Exports

**Download PDF** and **Download Excel** (Line items header) export **every month** of the ledger you're in: your account's, or your browser-only one. Files are named `expense-ledger-YYYY-MM-DD.pdf` / `.xlsx`. Bill file names are listed, but the files themselves aren't bundled.

### PDF report (A4)

1. Title, date range, currency and export date
2. Headline tiles: total spent, expenses, months, largest category
3. Spending by month, by category, and by payment mode
4. All expenses grouped by month (newest first): date, day, description, category, paid via, amount; **[bill]** marks attachments
5. Page numbers

### Excel workbook

| Sheet | Contents |
|---|---|
| Expenses | Date, Day, Month, Description, Category, Payment mode, Amount, Bill / receipt. Real dates, currency format, filters, `SUM` total. |
| By month | Entries and total per month |
| By category | Entries, total and share |
| By payment mode | Entries, total and share |
| Month x category | Months × categories grid with totals |

---

## How data is stored

### Records

| Record | Path | Contents |
|---|---|---|
| Account | `accounts/<accountId>` | `seq` (user number), `name`, `kind` (`email` / `mobile`), `hash` (SHA-256 fingerprint of the email or number, used to look it up), `masked` (a partly hidden copy of the email or number<!-- e.g. `us•••@test.com` -->), `createdAt` |
| Registered user's expense | `ledgers/<accountId>/expenses/<expenseId>` | See below |
| Guest expense | Browser `localStorage`, key `expense-ledger:guest:expenses` | See below |

The full email or number isn't stored in the shared records. Only the fingerprint and a masked version are, plus the full value in the signed-in browser's session.

### Expense document

```json
{
  "date": "2026-11-02",
  "month": "2026-11",
  "desc": "Weekly groceries",
  "category": "Groceries",
  "payment": "UPI",
  "amount": 86.4,
  "receipt": { "id": "a1b2c3…", "name": "dmart-bill.jpg", "type": "image/jpeg", "size": 482113 },
  "createdAt": 1793620403436,
  "updatedAt": 1793948764000
}
```

`payment`, `receipt` and `updatedAt` are optional.

### Where each edition keeps it

| | Hosted edition<!-- Claude edition --> | Standalone edition |
|---|---|---|
| Accounts and registered users' expenses | Hosted database<!-- artifact database --> (shared by everyone with access) | Browser `localStorage`, key `expense-ledger:standalone:db:v1` |
| Guest expenses | Browser `localStorage` | Browser `localStorage` |
| Bill files | Hosted file storage<!-- artifact file storage, served at /_blob/<id> --> | Browser IndexedDB `expense-ledger` → `receipts` |
| Sign-in session | Browser `localStorage`, key `ledger-session:v2` (30 days) | Same |
| Currency and sort | Browser `localStorage` (`cur`, `sort`) | Same |

---

## Standalone edition and GitHub Pages

`index.html` is a single file with no server or build step. It uses the same code as the hosted edition<!-- Claude edition -->, with a small built-in adapter that stores everything in the browser.

**What's different:** there's no shared database, so a registered account only exists in the browser where it was created. Signing in with the same email on another computer won't find it. The 10-user limit is also counted per browser. To make accounts work across browsers and computers on GitHub Pages, the adapter can be replaced with a hosted database (for example, the free tiers of Firebase or Supabase).

### Publish on GitHub Pages (free)

1. Create a **public** repository on github.com, e.g. `expense-ledger`. Pages on private repos needs a paid plan.
2. **Add file → Upload files**, upload `index.html` (keep that name) and `README.md`, then commit.
3. Go to **Settings → Pages**, choose **Deploy from a branch**, **main**, **/(root)**, then **Save**.
4. After a minute or two it's live at `https://<your-username>.github.io/expense-ledger/`.

### Collecting feedback

- Testers with a GitHub account can comment in the repo's **Issues** tab.
- A tester can send an Excel or PDF export to show what they entered.

---

<!-- Claude edition -->
## Sharing and access (hosted edition)

- The page is **private** to its owner until shared from the **Share** menu. It can be shared within the owner's organization, not by public link.
- Give testers **Contributor** access so they can register and save expenses. **Viewers** can only use *Continue without an account*.
- **Editors** can also upload bills.
- Because accounts aren't password-protected, anyone with access can open any registered account if they know its email or number.

---

## Technical overview

| Piece | Details |
|---|---|
| Format | Single self-contained HTML page |
| Sign-in | Mock OTP. Email/number matched by SHA-256 fingerprint (Web Crypto). |
| Charts | Hand-drawn inline SVG |
| Excel export | SheetJS `xlsx` 0.18.5 |
| PDF export | jsPDF 2.5.1 + jspdf-autotable 3.8.2 |
| Library loading | On first export, from cdnjs with jsDelivr as fallback |
| Fonts | Instrument Sans and Spline Sans Mono (Google Fonts), with system fallbacks |

<!--
**Claude edition (artifact) capabilities:**

```json
{
  "db": { "rules": [
    { "path": "", "read": "interact", "write": "interact" },
    { "path": "data/users/{self}", "read": "interact", "write": "interact" }
  ] },
  "user": {}, "downloads": true, "assets": {}
}
```
-->

**Standalone edition:** a built-in storage adapter<!-- window.claude --> backed by `localStorage` (records) and IndexedDB (bills), with native browser downloads.

---

## Known limitations

- **No real security (testing only).** Codes are simulated and shown on screen; anyone who knows a registered email or number can open that account.
- **Standalone accounts don't sync.** On GitHub Pages / local file, everything stays in that browser until a hosted database is connected.
- **Guest expenses can't be moved** into an account yet.
- **No account deletion or contact change** from the page yet.
- **No currency conversion**; the PDF uses currency codes (e.g. `INR 26,000.00`).
- One bill per expense, 2 MB max; HEIC not accepted; exports don't bundle bill files.
- Fixed category and payment mode lists.
- No recurring expenses, budgets, income or import yet.
- Exports need internet access on first use to load the PDF/Excel libraries.

---

## Troubleshooting

| Problem | What to do |
|---|---|
| "We couldn't find an account for that email or number" | Check for typos, or create an account. In the standalone edition, accounts only exist in the browser where they were made. |
| "That code isn't right" | Use the code shown on the verification screen (user 1 → 111111, and so on) |
| "Too many incorrect codes" | Start again from Sign in |
| "That email or number is already registered" | Sign in with it instead |
| Registration limit message | All 10 places are taken. Use *Continue without an account*. |
| Guest expenses missing | They're saved per browser. Use the same browser, not a private window, and don't clear site data. |
| "Registration isn't available in this view" (hosted edition) | Open the page directly while signed in<!-- to claude.ai -->, with at least Contributor access |
| Bill field missing (hosted edition) | Only Editors can upload bills |
| "Bills must be 2 MB or smaller" | Compress or crop the image |
| "isn't a supported file" | Convert to JPG, PNG, WEBP or PDF |
| "No expenses match" | Clear the search box or the category chip |
| "Couldn't load the export tools" | Check your connection or script blocker, then retry |
| "That expense no longer exists" while editing | It was removed in another tab or device |

---

## Changelog

| Version | Date | Changes |
|---|---|---|
| 7 | 2026-11-12 | **Test accounts**: sign up / sign in with any email or mobile plus demo code (10 users max, works across browsers in the hosted edition<!-- Claude edition -->). **Continue without an account** (browser-only). Edit name, sign out, guest menu. Friendly limit message. Standalone edition updated with a browser-storage adapter. |
| 6 | 2026-11-11 | First sign-in version (tied to the hosting platform's user accounts<!-- claude.ai accounts -->); superseded by version 7. |
| 5 | 2026-11-11 | Sortable columns; interactive donut with hover and click-to-filter; search, filter chip and live totals; clickable trend bars; **This month** button; row highlights; keyboard support. |
| 4 | 2026-11-07 | Payment mode dropdown and **Paid via** column; bill / receipt upload (2 MB) with viewer; payment-mode summaries in exports; dropdown arrow fix; standalone `index.html`. |
| 3 | 2026-11-06 | PDF and Excel export; pencil-icon editing; redesigned currency selector; weekday in dates. |
| 2 | 2026-11-02 | Added **Miscellaneous** category. |
| 1 | 2026-10-29 | First release: add/remove expenses, monthly summary, category donut, six-month trend, line items, currency selector, example entries. |
