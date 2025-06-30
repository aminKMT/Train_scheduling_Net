# 🚂  Railway-Scheduler-Animation

A lightweight Python/Colab demo that **builds a multi-track railway network, schedules opposing trains under station-capacity constraints, and produces an interactive animation of every train in motion**.

<p align="center">
  <img alt="demo gif" src="docs/demo.gif" width="640">
</p>

---
![image](https://github.com/user-attachments/assets/58a088e1-4b9a-44f3-8a06-6a6f6a910d29)

## ✨  Features

| What | How it works |
|------|--------------|
| **Branching network** | `networkx.MultiDiGraph` with loops, parallel tracks, and terminals |
| **Random or fixed station capacities** | 5 – 10 by default; easily overridden |
| **Greedy capacity-aware scheduler** | Trains reserve capacity ahead; if full they wait at the current station |
| **Shortest-path routing** | Each train uses `nx.shortest_path()` from origin to destination |
| **Edge-level movement** | Traversal time per edge (`T_TRAVEL`) is configurable; animation interpolates positions |
| **Live telemetry** | Real-time counters above every node show current occupancy |
| **Inline HTML animation** | `matplotlib.animation.FuncAnimation → to_jshtml()` for instant playback in Colab or Jupyter |

---

## 📦  Quick start (Colab)

| Step | Command |
|------|---------|
| 1. Clone / open notebook | <https://github.com/aminKMT/Train_scheduling_Net/blob/main/Train_Scheduling.ipynb> |
| 2. Run **one** cell | The notebook installs deps, builds the graph, runs the simulation, and pops up the animation |
| 3. Tweak parameters | Change anything in the **“USER-TUNEABLE PARAMETERS”** block → rerun |

> **Tip:** The whole project is a single self-contained cell; no extra files or data needed.

---

## 🔧  Key parameters

| Variable | Meaning | Default |
|----------|---------|---------|
| `CAP_RANGE` | Min–max trains a station can hold | `(5, 10)` |
| `T_STOP`   | Minutes each train dwells at a station | `2` |
| `T_TRAVEL` | Minutes to traverse an edge | `3` |
| `RIGHT_TRAINS / LEFT_TRAINS` | How many trains start on each side | `4 / 3` |
| `ARRIVAL_RIGHT / ARRIVAL_LEFT` | Entry times (mins) for each train | `[0,3,5,9] / [1,4,6]` |
| `SIM_HORIZON` | Safety stop for the simulation | `250` |
| `FPS` | Animation frame rate | `5` |

Change them at the top of the script and rerun—everything else adapts automatically.

---

## 🛠️  Extending

* **Bigger graphs:** swap in any `networkx` graph (or an `osmnx` import) and update the `pos` layout dict.
* **Exact optimisation:** replace the greedy loop with a MILP / CP-SAT model if you need optimal global delays.
* **Better visuals:** add background images, color scales for delays, or export to mp4/GIF for sharing.

---

## 📑  Requirements

```bash
python 3.9+
networkx
matplotlib
tqdm           # optional progress bar
