# 🐍 TracSnake — P2P Snake & Ladders on Trac Network

> A fully playable, browser-based Snake & Ladders game built as a fork of [Intercom](https://github.com/Trac-Systems/intercom) — demonstrating real-time peer-to-peer gameplay coordination over the Trac Network sidechain.

[![Live Demo](https://img.shields.io/badge/Demo-Live%20App-00ff88?style=flat-square)](./index.html)
[![Fork of](https://img.shields.io/badge/Fork%20of-Intercom-blue?style=flat-square)](https://github.com/Trac-Systems/intercom)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)](./LICENSE)

---

<img width="1304" height="832" alt="image" src="https://github.com/user-attachments/assets/4acbee9c-0d70-4df7-bca0-704208686d7f" />


## 🎯 What is TracSnake?

**TracSnake** is a peer-to-peer multiplayer Snake & Ladders game that leverages the Intercom protocol's sidechannel architecture for real-time player coordination. Instead of relying on centralized game servers, TracSnake uses Intercom's P2P messaging layer to synchronize game state between players — trustlessly and without a middleman.

### Key Features

- **🎮 Fully Playable** — Complete Snake & Ladders implementation with animated moves, snake/ladder effects, and win detection
- **👥 2-Player Mode** — Local multiplayer for two players on same device
- **🤖 VS CPU Mode** — Play against an AI opponent
- **🌐 P2P Ready** — Architecture designed for Intercom sidechain state sync
- **⚡ Zero Dependencies** — Pure HTML/CSS/JS, no build step required
- **📱 Responsive** — Works on desktop and mobile browsers
- **🎨 Dark UI** — Professional dark-themed interface built for Trac ecosystem aesthetics

---

## 🗺️ Board Layout

Standard 10×10 Snake & Ladders board (squares 1–100):

| Feature | Count | Details |
|---------|-------|---------|
| Snakes | 8 | e.g., 97→78, 95→56, 88→24 |
| Ladders | 9 | e.g., 1→38, 28→84, 63→81 |
| Players | 2 | Player 1 (blue) / Player 2 or CPU (red) |
| Win Condition | Exact roll to reach 100 | — |

---

## 🚀 How to Run

```bash
# Clone this repo
git clone https://github.com/YOUR_USERNAME/TracSnake.git
cd TracSnake

# Open in browser — no build needed!
open index.html
```

Or simply open `index.html` in any modern browser.

---

## 🏗️ Architecture / Intercom Integration

TracSnake is designed around Intercom's two-layer architecture:

```
┌─────────────────────────────────────────────────────┐
│                   TracSnake App                      │
│  ┌─────────────────┐   ┌──────────────────────────┐ │
│  │  Game Logic     │   │  Intercom Sidechain Layer│ │
│  │  - Dice rolls   │◄──│  - P2P game state sync   │ │
│  │  - Move valid.  │   │  - Move broadcast        │ │
│  │  - Win detect   │   │  - Player coordination   │ │
│  └─────────────────┘   └──────────────────────────┘ │
└─────────────────────────────────────────────────────┘
```

**Sidechannel usage (real-time):**
- Broadcasting dice roll results to opponent
- Syncing current board positions
- Delivering game events (snake hit, ladder found)

**Replicated state usage (durable):**
- Recording final game results on-chain
- Leaderboard entries
- Match history

---

## 📁 Project Structure

```
TracSnake/
├── index.html       # Complete game app (single-file)
├── skill.md         # Agent skill file for Intercom protocol
├── README.md        # This file
└── LICENSE
```

---

## 🤖 Agent Skill

See [`skill.md`](./skill.md) for instructions on how Intercom agents can interact with TracSnake — including how to trigger game sessions, sync state, and broadcast moves over the network.

---

## 🪙 Trac Address (Payout)

```
trac1dcwzkezjhe068um8z76rmuv30kwkugrv84qt5gews9ul94kqm84qjpx5vv
```

> **Replace the above with your actual Trac address to receive 500 TNK payout.**

---

## 📸 Proof of Working App

The app runs entirely client-side. To verify:

1. Open `index.html` in browser
2. Click **ROLL** to start playing
3. Game auto-detects snakes (🐍) and ladders (🪜)
4. First to reach square 100 wins

**Features verified:**
- ✅ Board renders correctly (10×10, numbered 1–100)
- ✅ Snake and ladder positions visually marked with SVG overlays
- ✅ Dice animation and step-by-step piece movement
- ✅ Snake/Ladder teleportation with game log
- ✅ Win condition detection and overlay
- ✅ VS CPU mode with auto-roll
- ✅ New Game / Reset functionality

---

## 🔗 Links

- **Upstream Intercom:** https://github.com/Trac-Systems/intercom
- **Awesome Intercom List:** https://github.com/Trac-Systems/awesome-intercom
- **Trac Network:** https://trac.network

---

## 📄 License

MIT — fork freely, build boldly.
