# Multi-Agent AI Platform for Intelligent Materials Design

> Collaborative AI agents guide researchers from design goals to validated process parameters — in seconds.

![demo](https://img.shields.io/badge/status-prototype-orange)
![license](https://img.shields.io/badge/license-MIT-blue)
![stack](https://img.shields.io/badge/stack-vanilla%20HTML%2FCSS%2FJS-teal)

A single-page interactive demo of a multi-agent AI system that helps materials researchers design **porous alumina ceramics via freeze casting**. Six specialized AI agents collaborate to turn a high-level design goal (e.g. "75% porosity, 5 MPa") into concrete, recipe-level process parameters and a written design report.

This is a **prototype using simulated outputs** — no real ML model runs in the browser. The scientific logic is plausible but not experimentally validated.

![Demo Screenshot](docs/screenshot.png)

## Features

- **Six-agent workflow** — Planner → Literature → Data → Prediction → Optimization → Report, animated sequentially with live status indicators
- **Live design controls** — material system, processing method, target porosity, target strength, and free-text notes
- **One-click example goals** — biomedical scaffold, thermal insulation, and filtration membrane presets
- **Quantitative results** — recommended process parameters, predicted properties with target validation, radar chart comparing target vs. predicted across five axes
- **Generated design report** — human-readable rationale, trade-off analysis, and next-experiment suggestion
- **Zero build step** — pure HTML/CSS/JS in a single file; opens by double-click

## Multi-Agent Workflow

```
┌─────────┐    ┌───────────┐    ┌──────────┐    ┌────────────┐    ┌──────────────┐    ┌──────────┐
│  Input  │───▶│ ⬡ Planner │───▶│◈ Literat │───▶│ ▦ Data     │───▶│ ◎ Prediction │───▶│ ⟁ Optim. │
│  Goals  │    │ decompose │    │  retrieve│    │  correlate │    │  structure   │    │  Bayesian│
└─────────┘    └───────────┘    └──────────┘    └────────────┘    └──────────────┘    └────┬─────┘
                                                                                            │
                                                                              ┌─────────────▼─────────────┐
                                                                              │ ☰ Report  ─▶  Parameters  │
                                                                              │            ─▶  Properties │
                                                                              │            ─▶  Radar      │
                                                                              │            ─▶  Document   │
                                                                              └───────────────────────────┘
```

## Tech Stack

| Layer | Technology |
|---|---|
| Markup | HTML5 (semantic, single file) |
| Styling | CSS3 with custom properties, Google Fonts (Syne, DM Mono) |
| Logic | Vanilla JavaScript (IIFE, no globals, no build step) |
| Charts | [Chart.js 4.x](https://www.chartjs.org/) via CDN (radar chart, dark theme) |
| Data | Static JSON (`data/mock_material_data.json`) |

No bundler, no framework, no backend, no API keys.

## Run Locally

```bash
git clone <repo-url>
cd 材料agent
open index.html       # macOS
# or simply double-click index.html in your file browser
```

Any modern browser (Chrome, Safari, Firefox, Edge) works. An internet connection is required on first load so the browser can fetch Google Fonts and Chart.js from their CDNs.

## Deploy with GitHub Pages

1. Push this repository to GitHub.
2. In the repo go to **Settings → Pages**, set **Source** to `Deploy from a branch` and pick `main` / `(root)`.
3. Wait ~30 seconds, then visit `https://<your-username>.github.io/<repo-name>/`.

That's it — no build step, no workflow file needed.

## Project Structure

```
.
├── index.html                       # Single-page demo (HTML + CSS + JS, all inline)
├── README.md                        # This file
├── docs/
│   └── project_brief.md             # Competition-style project brief
└── data/
    └── mock_material_data.json      # Mock material systems, freeze-casting database, agent outputs, presets, Pareto front
```

## Scientific Background

**Freeze casting** is a near-net-shape ceramic processing route in which a ceramic slurry is poured into a mold, frozen directionally, and freeze-dried so that ice crystals act as a sacrificial template. After sintering, the result is an anisotropic porous body with **lamellar pore channels aligned along the freezing direction**. The two dominant process knobs are **solid loading** (controls porosity and wall density) and **cooling rate** (controls lamellae spacing and pore alignment). Together they trace out a Pareto front between porosity and compressive strength — the multi-agent system in this demo helps researchers locate the optimal point on that front for a given application.

## Limitations & Disclaimer

- **Simulated outputs.** Agent responses, predicted properties, and the recommended parameter set are hardcoded for demonstration. No ML model or LLM runs at runtime.
- **Single material system.** The fully wired-up workflow targets porous Al₂O₃ via freeze casting; other dropdown options are placeholders.
- **Not scientifically validated.** Treat all numbers as illustrative. Experimental validation in a wet lab would be required before applying any parameter set.

## Future Roadmap

- [ ] **Real ML model** — replace the Prediction Agent's hardcoded output with a trained surrogate (e.g. Gaussian Process or graph neural network) over a real freeze-casting dataset.
- [ ] **Lab data integration** — closed-loop feedback where actual experimental results refine the surrogate after each run.
- [ ] **Multi-material support** — extend the data layer and agent prompts to cover hydroxyapatite, SiC, and TiO₂ alongside Al₂O₃.
- [ ] **LLM-powered agents** — wire the Planner / Literature / Report agents to a hosted LLM with retrieval over a curated literature corpus.

## License

MIT — see `LICENSE` if provided.

## Acknowledgments

- Freeze-casting mechanism descriptions inspired by S. Deville et al., *Science* (2006).
- UI typography: [Syne](https://fonts.google.com/specimen/Syne) and [DM Mono](https://fonts.google.com/specimen/DM+Mono) via Google Fonts.
- Charting: [Chart.js](https://www.chartjs.org/).
