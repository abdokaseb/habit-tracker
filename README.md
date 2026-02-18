# 📱 Habit Tracker PWA

A minimalist, offline-first habit tracking app built as a **Progressive Web App** — zero dependencies, fully offline after first load, installable on any mobile device.

## 🔗 Live Demo

**[https://abdokaseb.github.io/habit-tracker/](https://abdokaseb.github.io/habit-tracker/)**

## ✨ Features

- ✅ **Add & complete habits** — single tap to toggle daily completion
- 🔥 **Streak tracking** — consecutive-day streak counter per habit (up to 365 days)
- 📊 **Weekly dots** — 7-day visual history for each habit at a glance
- 📈 **Stats dashboard** — done today / total habits / best streak cards
- 💾 **Local storage** — all data persisted in `localStorage`, never leaves your device
- 📴 **Fully offline** — Service Worker with cache-first strategy
- 📲 **Installable** — PWA manifest enables "Add to Home Screen" on mobile
- 🌙 **Dark glassmorphism theme** — modern design with gradient accents, glow effects, and micro-animations
- 🎯 **Empty state guidance** — friendly prompt when no habits are added yet
- 🗑️ **Delete with confirmation** — prevent accidental habit removal
- ⌨️ **Keyboard support** — press Enter to submit in the add-habit modal

## 📲 Install on Your Phone

1. Open the [live URL](https://abdokaseb.github.io/habit-tracker/) in **Chrome** (Android) or **Safari** (iOS)
2. Tap **⋮ → Add to Home Screen** (Chrome) or **Share → Add to Home Screen** (Safari)
3. The app now works like a native app — **fully offline!**

## 🏗️ Tech Stack

| Component | Technology |
|---|---|
| App | Single `index.html` — all HTML, CSS, JS inline |
| Styling | Vanilla CSS with CSS custom properties, glassmorphism dark theme |
| Typography | [Inter](https://fonts.google.com/specimen/Inter) via Google Fonts |
| Persistence | `localStorage` API |
| Offline | Service Worker (`sw.js`) with cache-first strategy |
| Installability | PWA Manifest (`manifest.json`) |
| Icons | Python-generated PNG icons (192×192, 512×512) with gradient + checkmark |
| Hosting | GitHub Pages (auto-deploys from `main` branch) |

## 📁 Project Structure

```
habit_tracking/
├── index.html       # Full app (HTML + CSS + JS inline, ~526 lines)
├── sw.js            # Service Worker — caches all assets on install
├── manifest.json    # PWA manifest — name, icons, theme, display mode
├── icon-192.png     # App icon 192×192 (purple gradient with checkmark)
├── icon-512.png     # App icon 512×512
└── README.md
```

## 🛠️ Development

```bash
# Serve locally (access from phone on same Wi-Fi at http://<your-ip>:8080)
python -m http.server 8080

# No build step — edit index.html directly
# PWA install requires HTTPS (GitHub Pages provides this automatically)
```

## 📦 Data Format

Habits are stored in `localStorage` under the key `habit_tracker_data`:

```json
{
  "habits": [
    {
      "name": "Exercise 30 min",
      "completed": ["2026-02-17", "2026-02-18"]
    }
  ]
}
```

## 🚀 Deployment

- Hosted via **GitHub Pages** — push to `main` branch to update
- Service Worker cache version: `habit-tracker-v1` (bump in `sw.js` to force update)
- To deploy fresh: Settings → Pages → Source: `main` / `/ (root)`
