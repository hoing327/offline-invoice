# Offline Invoice Generator

**→ [Use it](https://hoing327.github.io/offline-invoice/)**

One HTML file. No account, no server, no build step, no dependencies. Open it and make an invoice.

Your data is stored in your own browser's `localStorage`. Nothing is uploaded — there is no backend to upload it to. Save the page to your disk and it keeps working with the network off, forever.

---

## What it does

- Line items with sub-notes, drag to reorder
- 22 currencies, tax, discounts, deposits already paid
- Saved clients and saved invoices, auto-incrementing numbers
- Overdue invoices flag themselves — that's your collections queue
- Print straight to PDF (A4, margins already set)
- Export/import your whole dataset as one JSON file

## Details it gets right

Small things, but they are the ones that cause arguments with a client:

- **Dates never shift by a timezone.** Due dates are computed as calendar dates and never converted to an instant. An invoice printed in Seoul and one printed in Lisbon show the same due date. (This was a real bug during development — `new Date(iso).toISOString()` moved the due date back a day for everyone east of UTC.)
- **Dates are never numeric.** `6 Aug 2026`, `Aug 6, 2026`, or `2026-08-06` — never `06/08/2026`, which means August 6th to an American client and June 8th to a German one.
- **Money is rounded per line, then summed** — the same order an accounting system uses — so the total always equals the sum of the printed rows.
- **Zero-decimal currencies** print as ¥3,000, not ¥3,000.00.
- **The currency code is on the amount-due line**, because `$` alone is ambiguous between at least six currencies.
- **Invoice numbers increment, and deleting an issued one warns you.** Most tax authorities want a gap-free sequence.

## Check the arithmetic yourself

Open it with `#selftest` on the end of the address:

```
https://hoing327.github.io/offline-invoice/#selftest
```

It runs 26 assertions on the money and date maths — discounts, tax bases, deposits, per-line rounding, zero-decimal currencies, month/year/leap-day boundaries — and prints the results. It should say **ALL 26 CHECKS PASSED**.

## What it deliberately doesn't do

No emailing, no payment links, no cloud sync, no accounting, no automatic tax rules. It makes correct invoices and remembers them. That's the whole scope, and it's why it can keep working untouched.

---

## The rest of the paperwork

An invoice is the easy half. The hard half is the contract that makes it collectable, and knowing what to send when it goes unpaid.

The **[Freelance Contract & Invoice Pack](https://wisealpha.gumroad.com/l/freelance-pack)** ($29, one payment) adds three plain-language contracts, a 25-clause library including what to strike from the client's own contract, and an eight-email collections sequence with the day to send each one.

There is also a **[free extract](https://wisealpha.gumroad.com/l/13-clauses)** — 13 clauses to strike from a client's contract, with the replacement wording.

*Not legal advice.*

## Licence

The generator in this repository is free to use, modify, and redistribute.
