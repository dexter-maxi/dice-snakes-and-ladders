# TracSnake Skill — Intercom Agent Instructions

## Overview

TracSnake is a P2P Snake & Ladders game app built on the Intercom protocol. This skill file describes how Intercom agents should interact with TracSnake sessions.

## App Identity

- **App Name:** TracSnake
- **App Type:** P2P Turn-Based Game
- **Protocol:** Intercom Sidechannel + Replicated State
- **Interface:** Browser-based (`index.html`)

---

## Agent Capabilities

Intercom agents interfacing with TracSnake can perform the following actions:

### 1. `start_game`
Initiate a new game session between two peers.

**Payload:**
```json
{
  "action": "start_game",
  "player1": "<peer_id_or_trac_address>",
  "player2": "<peer_id_or_trac_address>",
  "mode": "pvp" | "pve"
}
```

**Response:**
```json
{
  "session_id": "<uuid>",
  "board": "standard_10x10",
  "turn": "player1",
  "state": { "player1": 1, "player2": 1 }
}
```

---

### 2. `roll_dice`
A player rolls the dice and requests a move.

**Payload:**
```json
{
  "action": "roll_dice",
  "session_id": "<uuid>",
  "player": "<peer_id>"
}
```

**Response:**
```json
{
  "rolled": 4,
  "from": 14,
  "to": 18,
  "event": null | "snake" | "ladder",
  "final_position": 18,
  "next_turn": "<peer_id>"
}
```

---

### 3. `sync_state`
Broadcast current game state to all peers in session.

**Payload:**
```json
{
  "action": "sync_state",
  "session_id": "<uuid>",
  "state": {
    "player1": 42,
    "player2": 17,
    "turn": "player2",
    "move_count": 12
  }
}
```

---

### 4. `game_over`
Emit when a player wins (reaches square 100).

**Payload:**
```json
{
  "action": "game_over",
  "session_id": "<uuid>",
  "winner": "<peer_id>",
  "moves_taken": 24,
  "trac_address": "<winner_trac_address>"
}
```

---

## Board Constants

Agents must be aware of the following fixed board configuration:

### Snakes (head → tail)
| From | To |
|------|----|
| 97 | 78 |
| 95 | 56 |
| 88 | 24 |
| 62 | 18 |
| 48 | 26 |
| 36 | 6  |
| 32 | 10 |
| 16 | 6  |

### Ladders (bottom → top)
| From | To |
|------|----|
| 1  | 38 |
| 4  | 14 |
| 9  | 31 |
| 20 | 42 |
| 28 | 84 |
| 40 | 59 |
| 51 | 67 |
| 63 | 81 |
| 71 | 91 |

---

## Sidechannel Usage (Real-time)

TracSnake uses Intercom's **fast P2P sidechain** for:
- Dice roll results (low-latency delivery to opponent)
- Move validation confirmations
- Game event notifications (snake/ladder hits)
- Turn change notifications

Message format follows the Intercom sidechain envelope:
```json
{
  "protocol": "tracsnake/v1",
  "type": "<action>",
  "payload": { ... },
  "timestamp": "<unix_ms>"
}
```

---

## Replicated State Usage (Durable)

TracSnake uses Intercom's **replicated state layer** for:
- Committing game results permanently
- Storing player win/loss records
- Publishing to global leaderboard
- Verifiable game history

---

## Error Codes

| Code | Meaning |
|------|---------|
| `ERR_NOT_YOUR_TURN` | Player tried to roll out of turn |
| `ERR_INVALID_SESSION` | Session ID not found |
| `ERR_OVERSHOOT` | Roll would exceed 100 (no move) |
| `ERR_GAME_ENDED` | Session already completed |

---

## Notes for Agents

- Agents should **not** trust client-reported dice rolls; in competitive mode, dice should be provably random (e.g., commit-reveal or VRF).
- The board layout is static and hardcoded — no dynamic board configurations in v1.
- CPU (AI) opponent moves are triggered automatically server-side with a 1-second delay for UX purposes.
- All positions are 1-indexed (1 to 100).

---

*TracSnake is a fork of [Intercom](https://github.com/Trac-Systems/intercom) by Trac Systems.*
