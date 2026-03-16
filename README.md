# Crease Pattern Explorer

A visual, interactive tool for studying the geometry of origami bases — fold it by hand, understand it mathematically, simulate it, then perturb it.

---

## Overview

Crease Pattern Explorer is a browser-based environment for investigating the mathematical structure of traditional origami bases. It bridges physical folding practice with the underlying geometry: given a crease pattern, the tool verifies flat-foldability conditions at every interior vertex, renders the mountain/valley assignment as an interactive planar graph, and animates the fold sequence in real time.

The project grew from a simple question: *why do these folds actually work?* The answer lives in two elegant theorems — and this tool makes both of them tangible.

---

## Features

- **Crease pattern visualization** — renders any crease pattern as a labeled planar graph, with edges colored by mountain/valley/border assignment
- **Kawasaki's theorem checker** — verifies at each interior vertex that alternating angle sums equal 180°, with per-vertex pass/fail annotation
- **Maekawa's theorem checker** — confirms that mountain and valley count at each vertex differ by exactly 2
- **Fold animation** — spring-mass simulation folds the crease pattern from flat sheet to finished model, with a continuous fold-angle slider
- **Perturbation mode** — nudge crease angles while preserving Kawasaki's condition and watch the resulting 3D geometry update in real time
- **Bundled bases** — bird base, frog base, waterbomb base, and preliminary base included out of the box
- **FOLD format import** — load any crease pattern in the community-standard FOLD JSON format

---

## The Mathematics

Two theorems govern whether a crease pattern is flat-foldable at a single vertex:

**Kawasaki's Theorem**
For a single interior vertex with 2n alternating angles θ₁, θ₂, ..., θ₂ₙ, the pattern is flat-foldable if and only if:

```
θ₁ + θ₃ + θ₅ + ... + θ₂ₙ₋₁ = 180°
```

That is, the alternating sums of angles around the vertex must each equal 180°.

**Maekawa's Theorem**
At any interior vertex, if M is the number of mountain folds and V the number of valley folds meeting at that vertex:

```
|M - V| = 2
```

Together, these are necessary (but not sufficient) conditions for global flat-foldability. The tool checks both at every interior vertex and surfaces violations immediately.

---

## Getting Started

### Prerequisites

- Node.js ≥ 18
- A modern browser (Chrome, Firefox, or Safari)

### Installation

```bash
git clone https://github.com/username/crease-pattern-explorer.git
cd crease-pattern-explorer
npm install
npm run dev
```

Then open `http://localhost:5173` in your browser.

### Loading a crease pattern

The app opens with the bird base loaded by default. To load a different base, use the selector in the top-left panel. To load your own crease pattern:

1. Export it as a `.fold` file from any compatible tool (Origami Simulator, Oriedita, or by hand)
2. Click **Import** and select the file
3. The graph, theorem checks, and simulation will populate automatically

---

## Project Structure

```
crease-pattern-explorer/
├── src/
│   ├── core/
│   │   ├── graph.js          # Planar graph representation of crease patterns
│   │   ├── kawasaki.js       # Kawasaki's theorem verification
│   │   ├── maekawa.js        # Maekawa's theorem verification
│   │   └── simulation.js     # Spring-mass fold simulation
│   ├── ui/
│   │   ├── GraphView.jsx     # Interactive crease pattern renderer
│   │   ├── SimView.jsx       # 3D fold animation (WebGL)
│   │   ├── TheoremPanel.jsx  # Per-vertex theorem checker UI
│   │   └── PerturbPanel.jsx  # Angle perturbation controls
│   ├── data/
│   │   ├── bird-base.fold
│   │   ├── frog-base.fold
│   │   ├── waterbomb-base.fold
│   │   └── preliminary-base.fold
│   └── main.jsx
├── public/
├── package.json
└── README.md
```

---

## Usage Guide

### Exploring a base

Select a base from the dropdown. The left panel shows the crease pattern as a planar graph — click any interior vertex to see its angle sequence and theorem check results. Green indicates both Kawasaki and Maekawa are satisfied; red flags a violation.

### Animating the fold

Use the **Fold** slider in the right panel to animate from flat (0°) to fully folded (1.0). The spring-mass simulation runs in real time; complex crease patterns may fold more slowly on lower-end hardware.

### Perturbation mode

Toggle **Perturb** to enable angle editing. Click a vertex, then drag the angle handles. The tool adjusts adjacent angles to maintain Kawasaki's condition automatically. Watch how small deviations from the canonical base geometry propagate into the 3D folded shape.

### Importing custom crease patterns

Any `.fold` file is accepted. The FOLD format specification is documented at [github.com/edemaine/fold](https://github.com/edemaine/fold). Crease patterns exported from Origami Simulator or designed in Oriedita will import without modification.

---

## Roadmap

- [ ] Global flat-foldability checking (currently per-vertex only)
- [ ] Layer ordering inference for flat-folded states
- [ ] Export crease pattern as SVG or PDF
- [ ] Straight skeleton visualization for fold-and-cut construction
- [ ] Support for rigid origami simulation (fixed-panel, hinge-only folding)
- [ ] TreeMaker output import

---

## References

- Demaine, E. D., & O'Rourke, J. (2007). *Geometric Folding Algorithms: Linkages, Origami, Polyhedra*. Cambridge University Press.
- Lang, R. J. (2011). *Origami Design Secrets: Mathematical Methods for an Ancient Art* (2nd ed.). A K Peters/CRC Press.
- Tachi, T. Origami Simulator. [origamisimulator.org](https://origamisimulator.org)
- Ghassaei, A. (2018). *Real-time Origami Simulation*. Proceedings of the 7th International Meeting on Origami in Science, Mathematics and Education (7OSME).
- Bern, M., & Hayes, B. (1996). The complexity of flat origami. *Proceedings of the 7th Annual ACM-SIAM Symposium on Discrete Algorithms*, 175–183.

---

## License

MIT License. See `LICENSE` for details.
