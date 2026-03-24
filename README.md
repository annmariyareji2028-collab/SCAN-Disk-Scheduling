# SCAN Disk Scheduling Simulator

A fully interactive, browser-based simulator for the **SCAN (Elevator) Disk Scheduling Algorithm** — built with pure HTML, CSS, and JavaScript. No frameworks, no backend, no dependencies.

---

## What is SCAN?

The **SCAN algorithm** (also called the Elevator Algorithm) works like an elevator in a building:

1. The disk head moves in one direction (left or right), servicing all requests it encounters.
2. When it reaches the **disk boundary**, it reverses direction.
3. It then services remaining requests on the way back.

This approach reduces the extreme wait times seen in simpler algorithms like FCFS or SSTF.

---

## Features

| Feature | Details |
|---|---|
| **Algorithm** | Full SCAN (Elevator) implementation |
| **Directions** | Left or Right initial head movement |
| **Visualization** | Animated Canvas graph with glow effects |
| **Animation** | Play / Pause / Reset with adjustable speed |
| **Step Table** | Per-step breakdown with cumulative seek time |
| **Stats Panel** | Total seek time, requests served, boundary hits |
| **Sequence Display** | Animated badge row showing service order |
| **Validation** | Full input validation with descriptive errors |
| **Responsive** | Works on desktop and mobile browsers |
| **Zero dependencies** | Single `.html` file, runs offline |

---

## How to Run

1. Open `index.html` in any modern browser (Chrome, Firefox, Edge, Safari)
2. That's it — no installation, no server needed

---

## How to Use

### Step 1 — Fill in the Inputs

| Field | Description | Example |
|---|---|---|
| Number of Requests | How many disk requests to simulate | `8` |
| Initial Head Position | Starting track of the disk head | `53` |
| Disk Size | Maximum track number (disk range: 0 to N) | `199` |
| Direction | Which way the head moves first | `Right` |
| Seek Sequence | Comma-separated list of track requests | `98, 183, 37, 122, 14, 124, 65, 67` |

> **Tip:** The number of values in the Seek Sequence must match the Number of Requests field.

### Step 2 — Click "Simulate SCAN"

The simulator will:
- Run the SCAN algorithm on your inputs
- Display the service order, total seek time, and boundary hit count
- Render the head movement graph on canvas
- Populate the step-by-step breakdown table

### Step 3 — Animate

Use the animation controls below the graph:

| Control | Action |
|---|---|
| ▶ Play | Start step-by-step animation |
| ⏸ Pause | Freeze animation at current step |
| ↺ Reset | Return to beginning |
| Speed slider | Drag to control animation pace (slow → fast) |

The active row in the table highlights in sync with the animation.

---

## Algorithm Walkthrough

Given:
- **Head:** 53
- **Direction:** Right
- **Disk Size:** 0–199
- **Requests:** 98, 183, 37, 122, 14, 124, 65, 67

**Step 1** — Split requests into two groups:
- Right of head (≥ 53): `65, 67, 98, 122, 124, 183` → sorted ascending
- Left of head (< 53): `37, 14` → sorted descending

**Step 2** — Move right, serve all right-side requests in order:
`53 → 65 → 67 → 98 → 122 → 124 → 183`

**Step 3** — Hit right boundary (track 199):
`183 → 199`

**Step 4** — Reverse, serve left-side requests:
`199 → 37 → 14`

**Final service order:** `53 → 65 → 67 → 98 → 122 → 124 → 183 → 199 → 37 → 14`

**Total seek time:** sum of all absolute differences between consecutive positions.

---

## Graph Guide

The canvas graph plots **disk track (Y-axis)** against **step number (X-axis)**.

| Element | Meaning |
|---|---|
| 🔴 Pink dot | Initial head position |
| 🔵 Cyan dot | Serviced request |
| 🟢 Green dot | Disk boundary hit (direction reversal) |
| ⚪ White dot | Current position during animation |
| Cyan line | Head movement path |
| Dashed vertical line | Boundary reversal point |

---

## Input Validation

The simulator validates all inputs before running:

- Number of requests must be ≥ 1
- Head position must be ≥ 0 and ≤ disk size
- Disk size must be ≥ 1
- All track numbers in the sequence must be within `0 – disk size`
- Count of values in the sequence must match the declared number of requests

Errors are displayed inline below the input form in red.

---

## Repository Files

```
yourusername.github.io/
├── index.html      ← The entire simulator (HTML + CSS + JS)
└── README.md       ← This file
```

```
index.html              ← renamed from scan_disk_scheduler.html
├── HTML  — Layout and structure
├── CSS   — Dark theme, animations, responsive grid
└── JS
    ├── runSCAN()       — Core algorithm
    ├── simulate()      — Input parsing, validation, orchestration
    ├── drawChart()     — Canvas rendering
    ├── animLoop()      — requestAnimationFrame animation loop
    ├── renderTable()   — Step-by-step breakdown table
    └── renderSequence() — Animated badge sequence display
```

---

## Browser Compatibility

| Browser | Supported |
|---|---|
| Chrome 90+ | ✅ |
| Firefox 88+ | ✅ |
| Edge 90+ | ✅ |
| Safari 14+ | ✅ |
| Mobile browsers | ✅ (responsive layout) |

---

## License

Free to use for educational purposes.
