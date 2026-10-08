Here is a complete `README.md` for **PasarKlik**, written in English. You can copy-paste it directly into your project.

```markdown
# PasarKlik

> Daily food price catalog by region. Offline-first, no ads, no tracking.

PasarKlik is a lightweight, offline-first web app that displays daily food prices based on the user's region. It features a dark, terminal-inspired UI and stores all data locally on the device. An optional `data.json` file can be used to sync prices remotely.

---

## ✨ Features

- **Region-based onboarding** — Prices are tailored to the user's city/region.
- **Offline-first** — Data is saved in `localStorage` and remains accessible without internet.
- **Built-in seed data** — Comes with 45+ common food items (chili, rice, eggs, meat, snacks, etc.).
- **Search & category filters** — Quickly find products by name or filter by category.
- **Price change indicators** — Shows price direction (▲ up / ▼ down / ─ flat) with percentage change.
- **Google search shortcut** — One-tap search for a product's current market price.
- **WhatsApp complaints** — Send complaints directly to the admin via WhatsApp.
- **Settings modal** — Change region, view cache size, check last sync time, or clear all data.
- **PWA-ready** — Installable on mobile devices via an embedded manifest.
- **Responsive & dark mode** — Terminal-style UI with neon cyan accents, optimized for OLED screens.

---

## 🛠 Tech Stack

- **Vanilla HTML, CSS, JavaScript** — No frameworks, no build tools.
- **localStorage** — Persists region, cache, and sync timestamp.
- **Fetch API** — Optional sync from `./data.json`.
- **PWA** — Manifest embedded as a data URI; optional `sw.js` for service worker caching.
- **Deep links** — Google Search and WhatsApp (`wa.me`).

---

## 🚀 Getting Started

### Prerequisites

- Any modern browser (Chrome, Firefox, Safari, Edge).
- Optional: A local web server for full PWA and fetch functionality.

### Run Locally

1. Download or clone this repository.
2. Open `index.html` directly in your browser.

> **Note:** Opening via `file://` works, but `fetch('./data.json')` will fail and fall back to cached/seed data. Service worker will not register.

For full PWA and sync support, serve over HTTP:

```bash
# Using npx
npx serve .

# Or using Python
python3 -m http.server 8080
```

Then open `http://localhost:8080`.

---

## 📁 File Structure

```
PasarKlik/
├── index.html      # Main app (HTML + CSS + JS all-in-one)
├── data.json       # Optional remote sync data
├── sw.js           # Optional service worker for offline caching
└── README.md
```

---

## ⚙️ Configuration

Open `index.html` and modify the `APP` object inside the `<script>` tag:

```js
var APP = {
  version: '1.0.0',
  waTarget: '6282229753236', // WhatsApp number for complaints
  keys: {
    origin:  'pasarklik:origin',
    originTs:'pasarklik:originTs',
    sync:    'pasarklik:sync',
    cache:   'pasarklik:cache'
  },
  presets: ['Genteng, Banyuwangi','Banyuwangi','Jember', ...]
};
```

- **`waTarget`** — Change to your own WhatsApp number (international format, no `+`).
- **`presets`** — Add or remove region suggestions shown during onboarding.
- **`SEED`** — Add or edit the built-in product list.
- **`CATS`** — Add or remove product categories.

---

## 📦 Data Format (`data.json`)

If `data.json` exists, the app will attempt to fetch it when the user taps **Sync**. On success, it replaces the local cache. On failure, it keeps the existing data.

```json
{
  "products": [
    {
      "id": "cabai-merah",
      "name": "Cabai Merah Keriting",
      "icon": "🌶",
      "unit": "kg",
      "cat": "Cabai",
      "price": 45000,
      "prev": 42000
    }
  ]
}
```

| Field   | Type   | Description                          |
|---------|--------|--------------------------------------|
| `id`    | string | Unique product identifier            |
| `name`  | string | Display name                         |
| `icon`  | string | Emoji or symbol                      |
| `unit`  | string | Unit of measurement (kg, liter, etc.)|
| `cat`   | string | Category (must match `CATS`)         |
| `price` | number | Current price in IDR                 |
| `prev`  | number | Previous price (for delta calculation)|

---

## 🌐 PWA & Service Worker

- The web app manifest is embedded as a `data:` URI, so no separate `manifest.json` is required.
- `sw.js` is **optional**. If present, the app registers it for offline caching.
- If `sw.js` is missing, the app still works offline via `localStorage`.

To enable full PWA installability, create a `sw.js` in the root directory.

---

## 🧠 How It Works

1. **Onboarding** — User enters their region. It is saved to `localStorage`.
2. **Load Products** — App checks `localStorage` cache. If empty, uses `SEED` data.
3. **Render** — Products are filtered by search query and category, then displayed as cards.
4. **Sync** — User taps **Sync**. App fetches `./data.json`. On success, updates cache and re-renders.
5. **Complaints** — User writes a message. App formats it and opens WhatsApp with a pre-filled text.
6. **Settings** — User can change region, view cache size, see last sync time, or clear all data.

---

## 🎨 Customization

All visual styles are defined as CSS variables in `:root`:

```css
:root {
  --bg: #0a0a0a;
  --cy: #00e5ff;
  --mg: #ff006e;
  --gn: #22e07a;
  --rd: #ff3860;
  --f: 'SF Mono', ui-monospace, ...;
}
```

- **Colors** — Change `--cy` for the accent color.
- **Font** — Change `--f` for the monospace font stack.
- **Grid background** — Adjust `--grid` and `background-size` in `body`.

---

## 🔒 Privacy

- All data (region, cache, sync timestamp) is stored **locally** on the user's device.
- No analytics, no tracking, no third-party servers.
- Complaints are sent only when the user explicitly taps the WhatsApp button.

---

## 📄 License

MIT License. See `LICENSE` for details.

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

---

## 📞 Contact

- **WhatsApp (complaints):** https://wa.me/6282229753236
- **GitHub:** https://github.com/Ezrohell

---

*Built with Love for market-goers, home cooks, and small business owners.*
