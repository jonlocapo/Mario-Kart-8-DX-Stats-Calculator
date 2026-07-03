# Mario Kart 8 Deluxe — Stats Calculator

A single-file, dependency-free web app for exploring **Mario Kart 8 Deluxe** build
statistics. Pick a **Driver + Body + Tires + Glider**, see all 12 (+ hidden Invincibility)
stats as canvas meter bars, search for better builds live, and study the Pareto frontier for
any two stats. Modeled on the classic dasding MK8DX calculator.

Everything is in `index.html` — no build step, no frameworks, no external requests. Just open
the file.

## The model

A build has four components. The game stores each stat as **points**; for a given stat the
four parts' points are summed into a *Level* (0–20), and the value shown on the menu bars is:

```
displayed = (sum of the four parts' points + 3) / 4
```

so bars range from **0.75 to 5.75**. Stats: Ground/Water/Anti-Gravity/Air **Speed**,
**Acceleration**, **Weight**, Ground/Water/Anti-Gravity/Air **Handling**, **Traction/Grip**,
**Mini-Turbo**, and the hidden **Invincibility**.

Data (points, groupings) comes from the Super Mario Wiki page
[*Mario Kart 8 Deluxe in-game statistics*](https://www.mariowiki.com/Mario_Kart_8_Deluxe_in-game_statistics).
Parts that share an identical stat vector are grouped together, exactly like the reference
tool.

## Features

- **Builder** — four list-box pickers → 13 canvas meters (core stats + terrain variants).
- **Group / Individual toggle** for the pickers.
- **Find Better Builds** (merged into the builder) — the live build is the base; per-stat
  `< ≤ = ≥ > n/a` conditions, a *true-upgrades-only* checkbox, and a results table whose cells
  are coloured green/red vs. the base. Recomputes live on any change.
- **Pareto Frontier** — pick any two stats; SVG scatter with the frontier highlighted plus a
  table of frontier builds.
- **Reference tables** for every driver / body / tire / glider stat group.

Heavy enumeration runs over **unique combined stat-group vectors** (~21k), never over the
hundreds of thousands of individual part combinations, so it stays instant.

## Host it on GitHub Pages (free)

1. Push this repo to GitHub.
2. Repo **Settings → Pages**.
3. Under **Build and deployment**, set **Source: Deploy from a branch**.
4. Choose your branch and the **`/ (root)`** folder, then **Save**.
5. After a minute your calculator is live at
   `https://<username>.github.io/<repo>/`.

No configuration needed — `index.html` is fully self-contained.
