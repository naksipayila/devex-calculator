<p align="center">
  <br>
  <strong>DevEx Calculator</strong>
  <br>
  <sub>Robux to USD &middot; Live TRY Rates &middot; Tax Calculator</sub>
  <br><br>
  <img alt="Version" src="https://img.shields.io/badge/version-1.0-4aa3ff">
  <img alt="License" src="https://img.shields.io/badge/license-MIT-35d49a">
</p>

---

A sleek, dark-themed calculator for Roblox developers. Instantly convert Robux to USD and Turkish Lira using the official DevEx rate and live exchange data. Built with zero dependencies.

## Contents

- [Features](#features)
- [Usage](#usage)
- [Tax Calculator](#tax-calculator)
- [Quick Buttons & Gestures](#quick-buttons--gestures)
- [Tech Stack](#tech-stack)
- [Exchange Rate](#exchange-rate)
- [Project Structure](#project-structure)
- [Development](#development)
- [License](#license)

## Features

### Core

| | |
|---|---|
| **Robux to USD** | Converts using the fixed DevEx rate of `0.0038` |
| **USD to Robux** | Click the USD field and type a value to reverse-calculate |
| **TRY Display** | Shows the live or manual Turkish Lira equivalent |
| **Number Formatting** | Turkish locale formatting with thousand separators |

### Controls

| | |
|---|---|
| **Quick Add** | `+1K` `+10K` `+100K` `+200K` buttons below the input |
| **Swipe to Double** | Swipe up any quick button to add `2x` the amount |
| **Clear** | Trash icon resets all values |
| **Rate Refresh** | Pulls the latest USD/TRY rate from the API |

### Tax Calculator

| | |
|---|---|
| **Net / Gross** | Enter net Robux or gross sale price &mdash; the other calculates automatically |
| **30% Fee** | Displays the exact Roblox marketplace fee |
| **Copy** | One-tap copy for the gross Robux value |
| **Drawer UI** | Opens as an overlay, closes on Escape or backdrop click |

### UX

| | |
|---|---|
| **Persistent State** | Robux amount and exchange rate survive page reloads |
| **Dark Theme** | Custom properties, subtle gradients, accent colors |
| **Responsive** | Works on desktop and mobile; quick buttons stack in two columns on small screens |
| **Animations** | Staggered entrance, number counter, flash feedback on add, swipe indicators |
| **Toast** | Brief confirmation on copy actions |

## Usage

Open `index.html` in any browser. No server, no build step.

```
# Windows
start index.html

# macOS
open index.html

# Linux
xdg-open index.html
```

### Basic Flow

1. Type a Robux amount or tap a quick-add button.
2. USD and TRY values appear instantly.
3. Click the USD field to edit it directly &mdash; the Robux field recalculates.
4. Adjust the TRY rate by typing in the rate row, or press the refresh icon.

### Double Amount

- **Mobile** &mdash; swipe up on any quick button. The label changes to the doubled value (`+10K` &rarr; `+20K`), the button lifts and scales up, then flashes green on success.
- **Desktop** &mdash; hold `Ctrl` and click a quick button.

### Copy Values

- Click the **TRY** amount to copy it.
- In the Tax Calculator, use the **copy icon** next to the gross Robux field.

## Tax Calculator

Tap the calculator icon in the header to open the drawer.

Enter either:

- **Net Robux** &mdash; the amount you actually received after the 30% cut, or
- **Gross Robux** &mdash; the original sale or gamepass price.

The other field and the fee amount calculate automatically.

```
Gross = Net / (1 - 0.30)      rounded down
Net   = Gross * (1 - 0.30)    rounded down
Fee   = Gross - Net
```

## Quick Buttons & Gestures

| Button | Adds | Double (swipe up) |
|--------|------|-------------------|
| `+1K` | 1,000 | 2,000 |
| `+10K` | 10,000 | 20,000 |
| `+100K` | 100,000 | 200,000 |
| `+200K` | 200,000 | 400,000 |

The swipe gesture requires a 35&nbsp;px upward movement while staying within the button. A live preview triggers after 15&nbsp;px.

## Tech Stack

| Layer | Technology |
|-------|------------|
| Markup | HTML5, ARIA labels, SVG icons |
| Styling | CSS custom properties, Flexbox, Grid, keyframe animations |
| Logic | Vanilla JavaScript (ES2015+) |
| Storage | LocalStorage |
| API | [open.er-api.com](https://open.er-api.com) |
| Font | Inter (Google Fonts) |

## Exchange Rate

The USD/TRY rate comes from the free [Exchange Rate API](https://open.er-api.com).

```
GET https://open.er-api.com/v6/latest/USD
```

Behavior:

- On page load, fetches the latest rate.
- Caches the result in LocalStorage for **24 hours**.
- If the API is unreachable, falls back to the cached rate.
- If no cache exists, falls back to the default of `46.00`.
- You can always type a custom rate manually.

## Project Structure

```
devex-calculator/
├── index.html      App markup and drawer overlay
├── style.css       Theme, responsive breakpoints, animations, ~960 lines
├── app.js          All logic, tax calc, API, gestures, ~490 lines
├── favicon.png     Browser tab icon (16x16)
└── README.md
```

## Development

No bundler, no framework, no npm.

```bash
# Syntax check
node --check app.js

# Format with Prettier (optional)
npx prettier --write .
```

Edit `DEVEX_RATE` or `TAX_RATE` at the top of `app.js` if the values change.

```js
const DEVEX_RATE = 0.0038;
const TAX_RATE   = 0.30;
```

Quick button amounts live in `renderQuickButtons()`:

```js
[1000, 10000, 100000, 200000].forEach((amt) => { ... });
```

## License

MIT &mdash; use it, modify it, ship it.
