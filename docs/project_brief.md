# Multi-Agent AI Platform for Intelligent Materials Design

**Project Brief — Prototype Demo**

## 1. Problem Statement

Designing a new ceramic material — even within a well-characterized process like freeze casting — remains painfully empirical. A graduate researcher who wants a porous alumina scaffold with 75% porosity and at least 5 MPa compressive strength typically faces weeks or months of trial-and-error: browsing scattered literature, eyeballing trends in small in-house datasets, guessing starting parameters, running a batch, characterizing, and iterating. The freeze-casting parameter space (solid loading, cooling rate, cold-plate temperature, dispersant and binder loadings, sintering profile) is large enough to make exhaustive screening prohibitive, yet structured enough that an experienced expert navigates it intuitively. The cost of that expertise — and the time to develop it — is the bottleneck. No tool today turns a high-level design goal into a defensible recipe with the underlying process-structure-property reasoning made explicit.

## 2. Proposed Solution

A **multi-agent AI system** that decomposes a researcher's design goal into a coordinated workflow of specialized agents, each handling a distinct cognitive task — literature retrieval, data analysis, structure prediction, parameter optimization, and report synthesis. A Planner Agent orchestrates the sequence; a Report Agent produces a human-readable recommendation. The system does not replace researcher expertise — it surfaces and structures it. The researcher sees not just a recommended parameter set but the literature, correlations, and trade-offs that produced it.

This prototype implements the full UI and end-to-end workflow with simulated outputs so the interaction design and value proposition can be evaluated independently of model quality.

## 3. Target Users

- **Graduate researchers** in ceramics, biomaterials, or porous materials groups who need to scope an initial parameter set before committing wet-lab time.
- **Materials engineers** in industrial R&D evaluating process windows for new product lines (filters, scaffolds, catalyst supports).
- **PIs and program managers** who want a structured, reviewable artifact (the design report) to accompany experimental proposals.

## 4. System Architecture

The system is a directed pipeline of six agents, each with a narrow, well-scoped role:

| # | Agent | Role |
|---|---|---|
| 1 | **Planner** | Decomposes the design goal into sub-tasks and routes them to downstream agents |
| 2 | **Literature** | Retrieves mechanism descriptions and prior parameter ranges from a curated knowledge base |
| 3 | **Data** | Mines a process-property database for correlations and identifies promising regions |
| 4 | **Prediction** | Predicts microstructure and properties for candidate parameter sets |
| 5 | **Optimization** | Runs Bayesian search over the parameter space to satisfy the design constraints |
| 6 | **Report** | Synthesizes the trail of evidence into a human-readable recommendation |

A shared context object (design goal, intermediate findings, candidate solutions, confidence scores) flows through the pipeline and is exposed in the UI so the researcher can audit the reasoning at every step.

## 5. Technical Design

In a production realization:

- **Planner / Literature / Report agents** would be LLM-driven with structured-output guardrails; literature retrieval would use embedding search over a curated corpus.
- **Data agent** would query a SQL or vector-indexed materials database (e.g. Citrine, NOMAD, or in-house) and compute correlations on demand.
- **Prediction agent** would call a trained surrogate — Gaussian Process regression or a graph neural network — over the process-structure-property mapping.
- **Optimization agent** would wrap a Bayesian optimization library (BoTorch, Ax) with the design constraints as acquisition objectives.

For this prototype, every agent output is hardcoded but presented in the exact format the production system would emit. The UI is vanilla HTML/CSS/JS so it embeds into any environment — Jupyter dashboard, lab LIMS, or standalone web app — with no framework lock-in.

## 6. Expected Impact

Empirically, freeze-casting parameter screening for a new application typically requires **30–50 wet-lab batches** before a research team converges on a usable recipe. By front-loading literature, data correlation, and Bayesian search into a software layer, we expect the multi-agent system to compress this to **~5 targeted batches** for validation — a 6–10× reduction in time-to-result and a comparable reduction in materials and characterization cost. Beyond raw throughput, the structured report at the end of every run produces a reviewable artifact that improves transparency for advisors, reviewers, and downstream collaborators.

## 7. Limitations

- This is a **prototype**. All agent outputs are hardcoded; no model runs in the browser.
- Coverage is limited to **porous alumina via freeze casting**. Other material systems shown in the UI are placeholders.
- The recommended parameter set is plausible but **has not been wet-lab validated**.
- The radar chart and Pareto-front data are illustrative, drawn from a small mock dataset rather than a real database.

## 8. Future Development

- **Real data integration.** Connect the Data Agent to a published freeze-casting dataset (e.g. Studart et al. compilations) and train a surrogate model for the Prediction Agent.
- **Wet-lab validation loop.** Add a feedback path so experimental results from each recommended batch update the surrogate, turning the system into a closed-loop active-learning platform.
- **Expanded material systems.** Extend the corpus and surrogate to cover hydroxyapatite, SiC, and TiO₂; same architecture, retrained models.
- **Live LLM agents.** Replace the simulated Planner / Literature / Report outputs with hosted LLM calls, with retrieval-augmented generation over an indexed literature corpus.
- **Multi-objective Pareto exploration.** Let users sweep porosity-strength trade-offs interactively and view the full recommended set along the Pareto front, not just a single point.
