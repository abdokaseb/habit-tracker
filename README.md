# 📱 Habit Tracker PWA

A minimalist, offline-first habit tracking app built as a **Progressive Web App** — zero dependencies, fully offline after first load, installable on any mobile device.

## 🔗 Live Demo

**[https://abdokaseb.github.io/habit-tracker/](https://abdokaseb.github.io/habit-tracker/)**

## ✨ Features

- ✅ **Habits & Habit Groups** — track individual habits or group related habits together
- 📦 **Group master checkbox** — one tap to mark an entire group done, or toggle children individually
- 👻 **Auto-hide completed** — finished items disappear to focus on what's left; toggle "Show completed" to reveal
- 📋 **Detail view** — tap any habit, group, or group item to see current streak, best streak, total days, completion rate, and a 3-month streak heatmap (most recent month first)
- 🎉 **All-done celebration** — congratulatory message when everything is done for the day
- 🔥 **Streak tracking** — per-habit, per-group, and best-streak stats
- ⭐ **Perfect day streak** — tracks consecutive days where every single item was completed
- ⏰ **Custom reset hour** — configure when your "day" resets (e.g. 2 AM for night owls)
- 📊 **Stats dashboard** — done today / total / best streak / perfect days
- 💾 **Local storage** — all data persisted in `localStorage`, never leaves your device
- 📴 **Fully offline** — Service Worker with cache-first strategy
- 📲 **Installable** — PWA manifest enables "Add to Home Screen" on mobile
- 🌙 **Dark glassmorphism theme** — modern design with gradient accents, glow effects, micro-animations
- 🗑️ **Delete with confirmation** — prevent accidental removal of habits or groups
- ⌨️ **Keyboard support** — Enter to submit in modals

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
| Icons | Python-generated PNG icons (192×192, 512×512) |
| Hosting | GitHub Pages (auto-deploys from `main` branch) |

## 📁 Project Structure

```
habit_tracking/
├── index.html       # Full app (HTML + CSS + JS inline)
├── sw.js            # Service Worker — cache-first, version: habit-tracker-v2
├── manifest.json    # PWA manifest — name, icons, theme, display mode
├── icon-192.png     # App icon 192×192
├── icon-512.png     # App icon 512×512
└── README.md
```

## 📦 Data Format

```json
{
  "settings": { "resetHour": 2 },
  "items": [
    {
      "id": "abc123",
      "type": "habit",
      "name": "Meditate",
      "completed": ["2026-02-17", "2026-02-18"]
    },
    {
      "id": "def456",
      "type": "group",
      "name": "Morning Routine",
      "completed": ["2026-02-18"],
      "children": [
        { "id": "g1", "name": "Brush teeth", "completed": ["2026-02-18"] },
        { "id": "g2", "name": "Stretch", "completed": ["2026-02-17"] }
      ]
    }
  ]
}
```

## 🛠️ Development

```bash
# Serve locally (access from phone on same Wi-Fi at http://<your-ip>:8080)
python -m http.server 8080

# No build step — edit index.html directly
# PWA install requires HTTPS (GitHub Pages provides this)
# To force SW update: bump CACHE_NAME in sw.js
```

## 🚀 Deployment

- Hosted via **GitHub Pages** — push to `main` branch to update
- Service Worker cache version: `habit-tracker-v2` (bump in `sw.js` to force update)
