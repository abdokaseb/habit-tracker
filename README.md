# 📱 Habit Tracker PWA

A minimalist, offline-first habit tracking app built as a **Progressive Web App** — zero dependencies, fully offline after first load, installable on any mobile device.

## 🔗 Live Demo

**[https://abdokaseb.github.io/habit-tracker/](https://abdokaseb.github.io/habit-tracker/)**

## ✨ Features

- ✅ **Habits & Habit Groups** — track individual habits or group related habits together
- 📦 **Group master checkbox** — one tap to mark an entire group done, or toggle children individually
- 👻 **Auto-hide completed** — finished items disappear to focus on what's left; toggle "Show completed" to reveal
- 📋 **Detail view** — tap any habit, group, or group item to see current streak, best streak, total days, completion rate, and a 3-month streak heatmap (most recent month first)
- ↕️ **Reorder habits** — tap the ↕️ button in the header to enter reorder mode; use ▲/▼ arrows to rearrange
- ✏️ **Edit habits & groups** — tap the ✏️ button to rename a habit, or edit a group's name and children
- 🗓️ **Edit past days** — tap any cell in the heatmap calendar to toggle a past completion
- 🎉 **All-done celebration** — congratulatory message when everything is done for the day
- 🔥 **Streak tracking** — per-habit, per-group, and best-streak stats
- ⭐ **Perfect day streak** — tracks consecutive days where every single item was completed
- ⏰ **Custom reset hour** — configure when your "day" resets (e.g. 6 PM for evening-based routines)
- 📅 **Day-of-week scheduling** — assign habits to specific days (e.g. Mon/Wed/Fri); streaks skip inactive days
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

## ⏰ Custom Reset Hour

The reset hour defines when your **logical "day" starts and ends**. Instead of midnight, you can set it to any hour — useful if your routine starts in the evening.

### How it works

| Reset Hour | Logical "Monday" window |
|---|---|
| 0 (midnight, default) | Mon 12:00 AM → Mon 11:59 PM |
| 6 AM | Mon 6:00 AM → Tue 5:59 AM |
| 6 PM (18) | Mon 6:00 PM → Tue 5:59 PM |

With a **6 PM reset**, the logical "Saturday" runs from **Friday 6:00 PM to Saturday 5:59 PM**. This means:

- Completing a Saturday habit at **Saturday 3:00 PM** (before 6 PM) stores it as the **Friday calendar date**
- Completing it at **Friday 7:00 PM** (after 6 PM) also stores it as the **Friday calendar date**
- The heatmap calendar shows the completion in the **Saturday row** (correctly reflecting the logical day, not the stored calendar date)

### What this means for weekly habits

Habits set to specific weekdays work correctly with any reset hour:
- A **"Saturday" habit** with a 6 PM reset appears on Saturday until 5:59 PM, then disappears
- The streak counts all consecutive logical Saturdays — regardless of whether the completion was stored as a Friday or Saturday calendar date internally
- The heatmap calendar displays completions on the **logical weekday row**, not the stored date row

### Setting the reset hour

Tap the ⚙️ gear icon in the header and choose "Day resets at" from the dropdown. Choose **6 PM** if your habits follow an evening schedule.

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
├── sw.js            # Service Worker — cache-first, version: habit-tracker-v1.13
├── manifest.json    # PWA manifest — name, icons, theme, display mode
├── icon-192.png     # App icon 192×192
├── icon-512.png     # App icon 512×512
└── README.md
```

## 📦 Data Format

```json
{
  "settings": { "resetHour": 18 },
  "items": [
    {
      "id": "abc123",
      "type": "habit",
      "name": "Evening walk",
      "completed": ["2026-02-27", "2026-03-06"],
      "activeDays": [6]
    },
    {
      "id": "def456",
      "type": "group",
      "name": "Morning Routine",
      "completed": ["2026-02-18"],
      "activeDays": [1, 3, 5],
      "children": [
        { "id": "g1", "name": "Brush teeth", "completed": ["2026-02-18"] },
        { "id": "g2", "name": "Stretch", "completed": ["2026-02-17"] }
      ]
    }
  ]
}
```

> **Note**: With `resetHour = 18`, the Saturday habit above has completions stored as **Friday dates** (`2026-02-27`, `2026-03-06`). This is correct — the app converts these back to logical Saturday when displaying and calculating streaks.

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
- Service Worker cache version: `habit-tracker-v1.13` (bump in `sw.js` to force update)
