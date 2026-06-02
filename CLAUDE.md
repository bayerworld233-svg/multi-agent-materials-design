# CLAUDE.md — Multi-Agent AI Platform for Intelligent Materials Design

## Project Overview

Build a **competition-ready single-page demo** for a multi-agent AI system that helps researchers design porous alumina ceramics via freeze casting. The system simulates six AI agents collaborating to turn a design goal into concrete process recommendations.

This is a **prototype demo using simulated data**. Scientific logic must be credible but no real ML model is involved.

---

## Deliverables

Create exactly these four files. Do not create others unless asked.

| File | Purpose |
|---|---|
| `index.html` | Single-page interactive demo, all-in-one |
| `README.md` | GitHub-ready project README |
| `docs/project_brief.md` | Competition-style project brief |
| `data/mock_material_data.json` | Realistic mock data for agents and properties |

---

## 1. `index.html` — Full Specification

### Hard Technical Constraints

- Pure HTML + CSS + JavaScript only. **No React, No Vue, No build step.**
- No backend, no API calls, no API keys.
- Only allowed external resource: Google Fonts and Chart.js via CDN.
- Must run by double-clicking `index.html` in any modern browser.
- All CSS and JS embedded inside the single HTML file.

### Visual Design Direction

**Aesthetic: Scientific Instrument meets Research Terminal**

Think of the visual language of high-end scientific equipment software (electron microscopes, NIST databases, materials characterization tools) crossed with a modern SaaS dashboard. NOT the typical purple-gradient AI startup aesthetic.

Specific direction:
- **Background**: Near-black `#0a0e17` with a very subtle cool blue-tinted noise texture overlay
- **Accent color**: Teal-cyan `#00c9b1` as primary, amber `#f5a623` as secondary alert/highlight
- **Cards**: Dark `#111827` base, `1px` border in `rgba(0,201,177,0.15)`, very subtle `backdrop-filter: blur(8px)`, soft teal glow shadow on hover
- **Typography**: Use `DM Mono` (monospaced) for data values, agent outputs, and code-like content. Use `Syne` for headings. Both available on Google Fonts. This combination evokes scientific instrumentation.
- **No purple gradients. No generic sans-serif. No "glowing orb" hero sections.**

Layout rhythm:
- Full-width hero (minimal, just title + subtitle + a single CTA line)
- 2-column main layout: left = input + agent workflow, right = results panels
- Results panels are hidden until workflow completes, then fade in with `opacity` + `translateY` transition
- Mobile: single column stack

### Page Sections (in order)

#### Section 1: Hero
```
Title:    Multi-Agent AI Platform for Intelligent Materials Design
Subtitle: Collaborative AI agents guide researchers from design goals
          to validated process parameters — in seconds.
Badge:    [PROTOTYPE DEMO] [Freeze Casting] [Porous Alumina]
```
Small disclaimer at bottom of hero: *"This is a research prototype using simulated agent outputs. Not scientifically validated."*

#### Section 2: Input Panel (left column)

Fields:
- **Material System** (dropdown): Porous Alumina (Al₂O₃), Hydroxyapatite, Silicon Carbide, Titanium Dioxide
- **Target Porosity** (range slider 50–90%, default 72%, live value display)
- **Target Compressive Strength** (range slider 1–20 MPa, default 6 MPa, live value display)
- **Processing Method** (dropdown): Freeze Casting, Gel Casting, Slip Casting
- **Additional Design Notes** (textarea, placeholder: "e.g. biomedical scaffold, needs interconnected pores")

Example prompt chips (clicking fills all fields):
- Chip 1: "Biomedical scaffold — 75% porosity, 5 MPa"
- Chip 2: "Thermal insulation — 80% porosity, 3 MPa"
- Chip 3: "Filtration membrane — 65% porosity, 10 MPa"

Primary button: **"Run Multi-Agent Design Workflow"** — teal, full width, with a subtle pulse animation before first click

#### Section 3: Multi-Agent Workflow Panel (left column, below input)

Six agent cards in vertical sequence. Each card has:
- Agent icon (use inline SVG or Unicode symbol, see below)
- Agent name + role label
- Status badge: `PENDING` (gray) → `RUNNING` (amber, pulsing dot) → `COMPLETED` (teal)
- Output area: hidden while pending, appears when completed, styled as monospace terminal text

Agent definitions:

| # | Name | Icon | Role label | Timing |
|---|---|---|---|---|
| 1 | Planner Agent | ⬡ | Goal Decomposition | 0s delay, 1.5s duration |
| 2 | Literature Agent | ◈ | Mechanism Retrieval | 1.5s delay, 2s duration |
| 3 | Data Agent | ▦ | Process-Property Analysis | 3.5s delay, 1.8s duration |
| 4 | Prediction Agent | ◎ | Structure Prediction | 5.3s delay, 2s duration |
| 5 | Optimization Agent | ⟁ | Parameter Optimization | 7.3s delay, 1.5s duration |
| 6 | Report Agent | ☰ | Recommendation Synthesis | 8.8s delay, 1.2s duration |

**Agent output text** (hardcoded, shown after each agent completes):

**Planner Agent:**
```
Goal decomposed into 4 sub-tasks:
[1] Retrieve freeze casting literature for Al₂O₃ systems
[2] Identify process-structure correlations (porosity 70–75%)
[3] Predict pore morphology from candidate parameters
[4] Optimize solid loading + cooling rate for strength ≥ 6 MPa
```

**Literature Agent:**
```
Retrieved 3 relevant mechanisms:
• Lamellar ice templating creates aligned pores (10–80 µm) 
  parallel to freezing direction. [Deville et al., 2006]
• Solid loading (30–45 vol%) inversely correlates with porosity;
  lower loading → higher porosity but reduced wall density.
• Cooling rate controls lamellae spacing: faster cooling → 
  finer pores (<20 µm), higher alignment score.
Confidence: 0.87
```

**Data Agent:**
```
Analyzed 847 data points from freeze casting database.
Key correlations identified:
  Porosity       ↑  with  ↓ solid loading    (r = -0.81)
  Pore size      ↑  with  ↓ cooling rate     (r = -0.74)
  Strength       ↑  with  ↑ solid loading    (r = +0.79)
  Alignment      ↑  with  ↑ cooling rate     (r = +0.68)
Optimal region: solid loading 32–36 vol%, cooling −1.5 to −2.0 °C/min
```

**Prediction Agent:**
```
Running structure-property prediction model...
Input: solid loading 34 vol%, cooling rate −1.8 °C/min

Predicted outputs:
  Porosity            73.2%    [target: >70%  ✓]
  Average pore size   38 µm
  Wall thickness      18 µm
  Pore alignment      0.84 / 1.0
  Compressive strength 6.4 MPa  [target: >5 MPa  ✓]
```

**Optimization Agent:**
```
Bayesian optimization complete (128 iterations).
Recommended process parameters:
  Solid loading       34 vol%
  Cooling rate        −1.8 °C/min
  Cold plate temp     −30 °C
  Dispersant (Darvan) 0.8 wt%
  Binder (PVA)        2.0 wt%

Pareto front: porosity-strength trade-off resolved at this point.
Estimated confidence: 0.82
```

**Report Agent:**
```
DESIGN RECOMMENDATION GENERATED
Material: Porous Al₂O₃ via Freeze Casting
Objective: Porosity >70%, Strength >5 MPa — ACHIEVED

All targets met. Proceed to experimental validation.
See recommendation panel for full parameter set.
```

#### Section 4: Results — Right Column (hidden until workflow complete, fade in)

**Panel A: Recommended Process Parameters**

Display as a styled data table or card grid:
| Parameter | Value | Unit |
|---|---|---|
| Solid Loading | 34 | vol% |
| Cooling Rate | −1.8 | °C/min |
| Cold Plate Temperature | −30 | °C |
| Dispersant (Darvan 811) | 0.8 | wt% |
| Binder (PVA) | 2.0 | wt% |
| Sintering Temperature | 1550 | °C |

**Panel B: Predicted Properties**

Display each as a horizontal progress bar with value label:
- Porosity: 73.2% (target ≥70%, bar color teal, show ✓)
- Average Pore Size: 38 µm
- Wall Thickness: 18 µm  
- Pore Alignment Score: 0.84 / 1.0
- Compressive Strength: 6.4 MPa (target ≥5 MPa, bar color teal, show ✓)

**Panel C: Radar Chart — Target vs Predicted**

Use Chart.js radar chart with 5 axes (normalized 0–1 scale):
- Axes: Porosity, Pore Size, Alignment, Strength, Wall Uniformity
- Dataset 1: "Target" — dashed line, amber color `#f5a623`
- Dataset 2: "Predicted" — solid line, teal color `#00c9b1`
- Dark background theme matching the page

**Panel D: Generated Report**

Styled as a document card with subtle left border accent:

```
MATERIAL DESIGN REPORT
━━━━━━━━━━━━━━━━━━━━━━

DESIGN RATIONALE
Freeze casting at −1.8 °C/min with 34 vol% solid loading produces
lamellar pore channels aligned along the freezing direction. The
selected cooling rate balances pore refinement (smaller lamellae
spacing) against wall density, achieving the target porosity-strength
combination.

POROSITY–STRENGTH TRADE-OFF
Increasing porosity beyond 76% would require reducing solid loading
below 30 vol%, which compromises wall integrity and drops compressive
strength below the 5 MPa threshold. The recommended parameters sit
at the Pareto-optimal point for this constraint set.

RECOMMENDED NEXT EXPERIMENT
Prepare Al₂O₃ slurry at 34 vol% with Darvan 811 (0.8 wt%) and PVA
(2.0 wt%). Freeze at −1.8 °C/min on copper cold plate at −30 °C.
Sinter at 1550 °C / 2h. Characterize via mercury porosimetry and
uniaxial compression testing.

NOTE: This recommendation is generated by a prototype AI system
using simulated predictions. Experimental validation is required.
```

#### Section 5: "Why This Matters" (full width, bottom)

Three cards in a row:
1. **Accelerates Discovery** — Reduces iteration cycles from months to minutes by connecting literature, data, and prediction in one workflow.
2. **Process-Property Intelligence** — Makes implicit expert knowledge about freeze casting explicit and queryable by any researcher.
3. **Extensible Architecture** — Same multi-agent framework applies to battery materials, mesoporous catalysts, and biomedical scaffolds.

### Interaction Behavior

- On page load: all agent cards show `PENDING`, results panels hidden, chart not rendered
- On "Run" click: button disabled, agents activate sequentially per timing table above
- Progress bar at top of workflow panel shows 0→100% as agents complete
- After final agent: results panels fade in with 400ms staggered delay between panels
- "Reset Demo" button (secondary style, top right of workflow panel): resets all states to initial, clears results, re-enables Run button
- Example chips: clicking fills all input fields and briefly highlights them with a flash animation

---

## 2. `README.md` — Full Specification

Structure:
1. Title + subtitle + badges (demo / prototype / MIT license)
2. One-paragraph project summary
3. Screenshot placeholder: `![Demo Screenshot](docs/screenshot.png)`
4. Features list (6 bullet points)
5. Multi-agent workflow (ASCII diagram showing the 6-agent chain)
6. Tech stack table (HTML5, CSS3, Vanilla JS, Chart.js)
7. "Run Locally" (literally: clone repo, open index.html)
8. "Deploy with GitHub Pages" (3-step instructions)
9. Project structure tree
10. Scientific background (3–4 sentences on freeze casting + process-structure-property)
11. Limitations & disclaimer (prototype, simulated data, not validated)
12. Future roadmap (4 items: real ML model, lab data integration, multi-material support, LLM-powered agents)
13. License + acknowledgments

Tone: professional, clear, suitable for both recruiters and researchers.

---

## 3. `docs/project_brief.md` — Full Specification

Competition-style document (~600–800 words). Sections:

1. **Problem Statement** — Trial-and-error in materials design is slow; freeze casting has a large, underexplored parameter space
2. **Proposed Solution** — Multi-agent AI system that decomposes design goals and uses process-structure-property knowledge
3. **Target Users** — Graduate researchers, materials engineers, R&D labs
4. **System Architecture** — Describe the 6-agent pipeline with roles
5. **Technical Design** — How agents would work in a real system (LLM for Planner/Literature/Report, ML model for Prediction, Bayesian optimizer for Optimization)
6. **Expected Impact** — Quantify: "reduces parameter screening from ~50 experiments to ~5"
7. **Limitations** — Prototype only, simulated outputs, no real model
8. **Future Development** — Real data integration, wet-lab validation loop, expanded material systems

---

## 4. `data/mock_material_data.json` — Full Specification

Include these top-level keys:

```json
{
  "material_systems": [...],       // 3 materials with properties
  "freeze_casting_database": [...], // 12 data points: params → properties
  "agent_outputs": {...},          // pre-written outputs for each agent
  "example_design_goals": [...],   // 3 complete goal presets
  "pareto_front": [...]            // 8 points on porosity-strength trade-off
}
```

`freeze_casting_database` entries must include:
`solid_loading`, `cooling_rate`, `cold_plate_temp`, `dispersant_wt`, `binder_wt`,
`porosity`, `pore_size_um`, `wall_thickness_um`, `alignment_score`, `compressive_strength_mpa`

Values must be internally consistent (higher porosity should correspond to lower solid loading, etc.).

---

## Code Quality Requirements

- Comment every major JS function with a one-line description
- Use CSS custom properties (`--color-accent`, `--color-bg`, etc.) for all theme values
- JS: no global variable pollution; wrap in an IIFE or use module pattern
- Validate that the Chart.js radar chart renders correctly with the dark theme
- Test that Reset truly resets all UI state (no stale values)

---

## Completion Checklist

Before finishing, verify:
- [ ] `index.html` opens in browser with no console errors
- [ ] All 6 agents animate correctly in sequence
- [ ] Results panels are hidden on load and appear after workflow
- [ ] Radar chart renders with correct data and dark theme
- [ ] Reset button works completely
- [ ] All 4 files created at correct paths
- [ ] README has working GitHub Pages deploy instructions
- [ ] `mock_material_data.json` is valid JSON
