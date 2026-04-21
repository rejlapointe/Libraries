# Libraries
# Last updated: 2026-04-21

This folder contains standalone demos and reference files for JavaScript libraries — not tied to any specific app. Use it to explore, test, and compare libraries before applying them to a project.

GitHub: https://github.com/rejlapointe/Libraries

---

## Files in This Folder

### format_toolbox_demo.html
Interactive demo of 4 popular font & cell formatting libraries (MS Office-style toolbars). Open in a browser — no server needed.

| Library | Type | What It Does |
|---|---|---|
| **Quill.js** | Rich text / Word-like | Full formatting toolbar: bold, italic, font size, color, alignment, lists |
| **Handsontable** | Excel-like grid | Spreadsheet with right-click menu, sorting, cell editing, 400+ formulas |
| **x-data-spreadsheet** | Lightweight spreadsheet | Canvas-based Excel clone with toolbar for font, color, borders |
| **Tabulator.js** | Data grid | Feature-rich table with per-cell color formatters and conditional styling |

---

## Library Replacement Opportunities (Portfolio & SnapTrade Apps)

Audit of `D:\MySoftwareProjects\PortfolioStatus` apps. Full file: `PortfolioStatus/libraries.md`.

### High Impact

| App | Area | Lines | Library | Why Better | Phrase to Use |
|---|---|---|---|---|---|
| Portfolio | `localStorage` state (70 lines, brittle) | `cash_injection.html:1018-1088` | `localforage` | Versioned, won't break when UI changes | "Replace the localStorage state management in the Portfolio Balancer with localforage" |
| Portfolio | Portfolio math (c_star, GT1/GT2, pass logic) | `cash_injection.html:650-720` | `decimal.js` | Floating-point precision — current code can drift | "Replace the portfolio math calculations in the Portfolio Balancer with decimal.js" |
| Portfolio | Table rendering (150 lines of `innerHTML` loops) | `cash_injection.html:787-953` | Tabulator formatters (already in use) | Eliminate repetitive `innerHTML` builds | "Replace the innerHTML table rendering loops in the Portfolio Balancer with Tabulator formatters" |

### Medium Impact

| App | Area | Lines | Library | Why Better | Phrase to Use |
|---|---|---|---|---|---|
| Portfolio | Currency formatting (scattered duplicates) | Both files | `numeral.js` | One call replaces hand-rolled parse/format | "Replace currency formatting in the Portfolio app with numeral.js" |
| Portfolio | Currency input masking | Both files | `cleave.js` | Auto-formats on keystroke, handles paste correctly | "Replace currency input masking in the Portfolio app with cleave.js" |
| SnapTrade | `buildCashTable()` HTML string building | `snaptrade_test.html:235-273` | `lit-html` | XSS-safe, composable, no string concatenation | "Replace the buildCashTable HTML string building in the SnapTrade app with lit-html" |
| SnapTrade | Pivot/merge array logic | `snaptrade_test.html:452-498` | `lodash` | `groupBy`/`mapValues` replace manual loops | "Replace the pivot and merge array logic in the SnapTrade app with lodash" |
| SnapTrade | Tabulator formatter sprawl (80+ lines) | `snaptrade_test.html:155-222` | Extract to module | Reusable, testable formatters | "Extract the Tabulator formatters in the SnapTrade app into a reusable module" |

### Low Impact

| App | Area | Lines | Library | Why Better | Phrase to Use |
|---|---|---|---|---|---|
| Portfolio | Accordion toggles | Both files | Native `<details>`/`<summary>` | No library needed — built into HTML | "Replace accordion toggles in the Portfolio app with native HTML details/summary elements" |
| Portfolio | Tab switching | Both files | CSS only | Already minimal, no change needed | "Simplify tab switching in the Portfolio app to CSS only" |
| SnapTrade | `fmtMoney()`/`fmtNum()` custom formatters | `snaptrade_test.html:145-150` | `numeral.js` | Single source of truth across both apps | "Replace fmtMoney and fmtNum in the SnapTrade app with numeral.js" |
| SnapTrade | Async loading state (repetitive try/catch) | `snaptrade_test.html:378-417` | `SWR` | Auto caching, retries, loading state | "Replace the async loading state try/catch patterns in the SnapTrade app with SWR" |
| SnapTrade | Password via `prompt()` | `snaptrade_test.html:362-365` | Native `<dialog>` | Better UX, no library needed | "Replace the password prompt() in the SnapTrade app with a native dialog element" |

**Top recommendation:** `numeral.js` — touches both apps across Medium and Low rows. One small CDN include, biggest reach.
