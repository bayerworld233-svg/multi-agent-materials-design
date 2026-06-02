# Multi-Agent AI Platform for Intelligent Materials Design

> Collaborative AI agents guide researchers from design goals to **data-informed candidate process windows** — in seconds, with human review.

🟢 **Live demo:** https://bayerworld233-svg.github.io/multi-agent-materials-design/

![demo](https://img.shields.io/badge/status-prototype-orange)
![license](https://img.shields.io/badge/license-MIT-blue)
![stack](https://img.shields.io/badge/stack-vanilla%20HTML%2FCSS%2FJS-teal)

A single-page interactive demo of a multi-agent AI system that helps materials researchers design **porous ceramics via freeze casting**. Six specialized AI agents collaborate to turn a high-level design goal (e.g. "75% porosity, 5 MPa") into a **candidate** parameter set, predicted properties, and a written design report — all derived in real time from the user's inputs by a rule-based recommendation engine.

This is a **prototype using simulated outputs** — no real ML model or LLM runs in the browser. The scientific logic is plausible but **not experimentally validated**. Every output is a candidate that requires human review and wet-lab verification.

## Features

- **System Architecture pipeline** — a 7-node overview at the top of the page makes the data flow explicit: User Goal → Agent Orchestrator → Literature RAG → Materials Dataset → Prediction Model → Optimization Engine → Design Report.
- **Six-agent animated workflow** — Planner → Literature → Data → Prediction → Optimization → Report, animated sequentially with `PENDING / RUNNING / COMPLETED` status indicators and per-agent terminal-style output.
- **Input-driven recommendations** — a `generateRecommendation(inputs)` rule engine maps the user's targets (material, method, porosity, strength, notes) to concrete process parameters and predicted properties. Every change to the inputs produces a different recommendation.
- **KPI panel** — for the two user-set targets (porosity, compressive strength), a side-by-side comparison of target vs. predicted with Δ and a pass/fail indicator.
- **Radar chart** with five normalized axes (Porosity, Pore Size, Alignment, Strength, Wall Uniformity) — the chart re-renders from the current recommendation so the target vs. predicted polygons reflect the user's actual goal.
- **Generated design report** that mentions the user's actual targets, the predicted deltas, the design rationale, and a **Human Review Required** banner.
- **Multi-material aware** — Al₂O₃, Hydroxyapatite, SiC, and TiO₂ each carry a material-specific strength scale and sintering temperature.
- **Multi-method aware** — Freeze Casting / Gel Casting / Slip Casting each carry a different pore-alignment ceiling.
- **Zero build step** — pure HTML/CSS/JS in a single file; opens by double-click.

## Multi-Agent Workflow

```
[Input] → ⬡ Planner → ◈ Literature → ▦ Data → ◎ Prediction → ⟁ Optimization → ☰ Report → [Results]
              ↓             ↓            ↓           ↓                ↓                ↓
         decompose     retrieve     correlate    predict        optimize         synthesize
                                                                                       ↓
                                              ┌──────── Parameters / Properties / KPIs / Radar / Report ─┐
                                              │                                                           │
                                              │       Each panel renders from the current recommendation │
                                              └───────────────────────────────────────────────────────────┘
```

## How Recommendations Are Generated

A small rule engine inside `index.html` (`generateRecommendation(inputs)`) maps the user's design goal to a candidate parameter set. The rules are deliberately simple and illustrative — they are **not** a calibrated surrogate model:

- **Higher target porosity** → lower solid loading → may reduce predicted strength.
- **Higher target strength** → higher solid loading → may reduce predicted porosity.
- **Higher target strength** also pushes the cooling rate faster (more negative), refining pore size and improving alignment.
- **Material** changes the achievable strength at a given solid loading (SiC > Al₂O₃ > TiO₂ > HAp) and sets the sintering temperature.
- **Processing method** caps how anisotropic the predicted pore alignment can be (freeze casting allows lamellar / aligned pores; gel- and slip-casting are largely isotropic).

A confidence score is reported alongside the prediction — **it is illustrative, not a calibrated probability**.

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
git clone https://github.com/bayerworld233-svg/multi-agent-materials-design.git
cd multi-agent-materials-design
open index.html       # macOS
# or simply double-click index.html in your file browser
```

Any modern browser (Chrome, Safari, Firefox, Edge) works. An internet connection is required on first load so the browser can fetch Google Fonts and Chart.js from their CDNs.

## Deploy with GitHub Pages

This repo is already deployed at https://bayerworld233-svg.github.io/multi-agent-materials-design/. To deploy your own fork:

1. Push your fork to GitHub.
2. In the repo, go to **Settings → Pages**, set **Source** to `Deploy from a branch` and pick `main` / `(root)`.
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

**Freeze casting** is a near-net-shape ceramic processing route in which a ceramic slurry is poured into a mold, frozen directionally, and freeze-dried so that ice crystals act as a sacrificial template. After sintering, the result is an anisotropic porous body with **lamellar pore channels aligned along the freezing direction**. The two dominant process knobs are **solid loading** (controls porosity and wall density) and **cooling rate** (controls lamellae spacing and pore alignment). Together they trace out a Pareto front between porosity and compressive strength — the multi-agent system in this demo helps researchers locate a candidate point on that front for a given application.

## Limitations & Disclaimer

This demo is a **research prototype**. Read this section before drawing any conclusions from the numbers it produces.

- **Simulated outputs.** Agent responses, predicted properties, and the recommended parameter set are produced by a small rule engine in the browser. No ML model, LLM, or external service runs at runtime.
- **Illustrative, not validated.** All numbers are candidate predictions. Treat them as starting points for discussion, not as design specifications.
- **Not scientifically validated.** The system has not been benchmarked against experimental data. The confidence score is illustrative, not a calibrated probability.
- **Material coverage is partial.** Al₂O₃ is the most thoroughly modeled; Hydroxyapatite, SiC, and TiO₂ adjust strength and sintering temperature but are not exhaustively calibrated.
- **Human review required.** Every recommendation requires review by a domain expert and wet-lab validation before any procurement, processing, or characterization decision is made. The in-page "Human Review Required" banner is a non-removable part of every report.

## Future Roadmap

- [ ] **Real ML model** — replace the rule engine with a trained surrogate (e.g. Gaussian Process or graph neural network) over a real freeze-casting dataset.
- [ ] **Lab data integration** — closed-loop feedback where actual experimental results refine the surrogate after each run.
- [ ] **Calibrated multi-material support** — extend the strength-scale + sintering-temperature parameters to a proper materials database with uncertainty estimates.
- [ ] **LLM-powered agents** — wire the Planner / Literature / Report agents to a hosted LLM with retrieval-augmented generation over a curated literature corpus.

## License

MIT — see `LICENSE` if provided.

## Acknowledgments

- Freeze-casting mechanism descriptions inspired by S. Deville et al., *Science* (2006).
- UI typography: [Syne](https://fonts.google.com/specimen/Syne) and [DM Mono](https://fonts.google.com/specimen/DM+Mono) via Google Fonts.
- Charting: [Chart.js](https://www.chartjs.org/).
