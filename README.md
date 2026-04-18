# Anand Kesavaraju's AI-Accelerated Systems Portfolio

I'm a biotech strategy and operations leader who used AI pair programming to go from zero modern web development experience to shipping functional, deployed systems in roughly six weeks. This portfolio highlights the platforms, dashboards, automation layers, and AI tooling I designed, directed, and iterated into working products.

The implementation was AI-assisted. The product direction, architecture choices, evaluation loop, and final integration decisions were mine. That is the through-line here: strong judgment, high learning velocity, and a willingness to get hands-on until the system works.

## What this portfolio demonstrates

- Rapid technical learning, from no traditional web development background to live full-stack systems
- End-to-end product ownership, from concept and UX direction through architecture, deployment, and iteration
- Systems thinking across cloud infrastructure, local devices, APIs, real-time telemetry, and user-facing software
- Practical AI leverage, using models as force multipliers while retaining responsibility for quality and decisions
- A builder-operator mindset that translates ambiguous problems into usable tools quickly

---

## 🧬 AI Evolution Engine

**Stack:** Node.js · Bayesian Statistics · Knowledge Graphs · DEPSO (Differential Evolution + Particle Swarm Optimization) · CLI

A decision-support and self-improvement engine for AI-assisted workflows. The system scans workspace artifacts, extracts evidence, proposes improvements, scores them probabilistically, and uses a hybrid DEPSO optimizer to tune its own scoring parameters over time.

**Problem:** Once an AI workspace becomes complex, it becomes harder to maintain consistent behavior, spot drift, and know which process changes are actually worth making — and the engine's own configuration becomes a non-trivial optimization problem.

**System:** I built an auditable engine that combines Bayesian scoring, evidence extraction, contradiction-aware knowledge graphs, and a DEPSO (Differential Evolution + Particle Swarm Optimization) meta-optimizer into a transparent, self-tuning optimization layer.

**Outcome:** The result is a more disciplined way to improve AI-assisted operations that gets better at improving itself over time.

**Skills gained:** Bayesian inference, evolutionary optimization (DE + PSO hybrids), knowledge graph design, systems architecture under ambiguity, and the ability to combine statistical methods with practical product judgment.

### Architecture highlights
- 6,800+ lines of transparent, zero-dependency code across 28 files
- Bayesian scoring with explicit confidence intervals for every proposal
- Knowledge graph with contradiction detection and causal-chain analysis
- Evidence extraction from workspace files and session artifacts
- Low-risk auto-application with higher-risk changes escalated for review
- Full CLI supporting dry runs, graph views, tests, JSON output, reports, and diff previews

### DEPSO meta-optimizer
The engine uses a hybrid **Differential Evolution + Particle Swarm Optimization** algorithm to tune its own scoring policy. Each individual in the population is a 36-dimensional strategy vector encoding rule weights, Bayesian prior shape, decision thresholds, evidence-type multipliers, and per-category proposal budgets. The merged implementation draws from four independent model builds (GPT-5.4, GPT-5.4-pro, O3, Opus), each competing on the same spec, with the best components combined:

```js
// Bayesian scoring with policy-genome-supplied parameters
function scoreProposals(proposals, evidence, config, state, graph, policy = null) {
  const bayesianConfig = resolveBayesianConfig(config, policy);
  return proposals.map((proposal) => {
    const prior = clamp(proposal.confidence, 0.05, 0.95);
    const alpha = bayesianConfig.priorAlpha + (prior * bayesianConfig.priorStrength) + samples.support;
    const beta = bayesianConfig.priorBeta + ((1 - prior) * bayesianConfig.priorStrength) + samples.oppose;
    const posteriorMean = alpha / (alpha + beta);
    const interval = credibleInterval(alpha, beta);
    // ...
  });
}
```

DE operators explore diverse policy configurations via mutation (`V = X_r1 + F·(X_r2 − X_r3)`) and binomial crossover, while PSO particles exploit promising regions by converging toward personal and global bests. The hybrid ratio adapts per generation using both operator success rates and population diversity — when diversity drops, more individuals switch to DE for exploration; when a promising region is found, PSO exploitation increases.

Overfitting is prevented through 20% holdout evidence validation, L2 regularization toward defaults, cross-generation alignment checks, and a calibration penalty targeting ~35% eligible proposals. Shadow mode runs the optimizer without affecting live decisions until the tuned policy is validated.

For higher-complexity systems, I often use a competitive multi-model workflow: assign the same problem to multiple frontier models, compare the outputs critically, and merge the strongest architectural and reasoning patterns into a production version. This project is the clearest example of that evaluation-and-synthesis approach.

---

## 🌐 kesavaraju.com, Personal Web Platform

**Stack:** Node.js · Vanilla JS · CSS3 · Cloudflare CDN · OCI (Oracle Cloud)

![Home](screenshots/home-dark.png?v=5)

<details><summary>☀️ Light Mode</summary>

![Home Light](screenshots/home-light.png?v=5)
</details>

**Problem:** I wanted a single web platform that could support a public professional presence, authenticated private experiences, and live integrations with other systems, without relying on a heavy framework or a patchwork of disconnected tools.

**System:** I built a custom full-stack platform with a unified design system, role-based access, reverse proxying, and real-time integrations. The public-facing experience is polished and distinctive, but the more important point is that the site functions as an extensible operating layer rather than a static brochure.

**Outcome:** The result is a production website that supports public portfolio content, authenticated private pages, and live data-connected tools under one architecture.

**Skills gained:** Full-stack architecture, product taste, access control, deployment judgment, and the ability to build a coherent platform rather than a one-off page.

### Selected features

#### 🌍 Explore (Interactive Globe)
- Three.js-based landing experience that gives the site a more distinctive and dynamic front door
- Theme-aware interface behavior across dark and light modes
- Custom motion and branding treatments used selectively to create a memorable first impression

#### 👨‍💼 /anand - Professional Profile

![Anand](screenshots/anand-dark.png?v=5)

<details><summary>☀️ Light Mode</summary>

![Anand Light](screenshots/anand-light.png?v=5)
</details>

- Custom responsive professional profile experience, built as a richer alternative to a static résumé page
- Structured presentation of leadership roles, education, and domain expertise
- Shared theming and reusable interface patterns across the broader platform
- Visual storytelling used to make dense information easier to scan and more distinctive

### Platform architecture
- Custom Node.js HTTP server powering routing, sessions, access control, and proxying
- Role-based authentication for public, private, and demo experiences
- Reverse proxy layer for internal dashboards and Home Assistant integrations
- WebSocket proxying for real-time telemetry
- Subdomain routing for separate public portfolio delivery
- Cloudflare CDN with SSL termination

---

## ⚡ Energy Dashboard

**Stack:** React · Vite · Three.js / React Three Fiber · WebSocket · Home Assistant API

Built a real-time energy intelligence system for whole-home monitoring, translating Home Assistant telemetry into a more legible operational dashboard. The project evolved through multiple iterations, from a 2D room-based breakdown to a full 3D floorplan environment.

![Energy V3](screenshots/energy-v3-dark.png?v=5)

<details><summary>☀️ Light Mode</summary>

![Energy V3 Light](screenshots/energy-v3-light.png?v=5)
</details>

**Problem:** Native energy views did not make it easy to understand room-level and circuit-level behavior at a glance, especially across different visualization modes.

**System:** I iterated from a room-based React dashboard to a 3D floorplan environment connected to live telemetry, with real-time updates flowing through WebSocket connections into a more intuitive operational interface.

**Outcome:** The dashboard provides a clearer live view of household energy behavior and turned a raw telemetry stream into something that is actually usable for monitoring and interpretation.

**Skills gained:** Product iteration, real-time systems integration, telemetry visualization, and the ability to turn complex operational data into a polished user experience.

### Key capabilities
- React + Vite SPA with real-time power consumption via WebSocket to Home Assistant
- Interactive room-by-room breakdown with animated transitions and theme-aware rendering
- Evolved into a Three.js 3D floorplan rendered from the actual home layout
- Multiple view modes: floorplan, satellite, and combined
- Live light-state rendering - room lights in 3D reflect real Home Assistant state
- Blender pipeline for 3D asset creation

---

## 📊 Custom Data Dashboard

**Stack:** Node.js · Chart.js · Custom API integrations

A standalone analytics webapp for longitudinal tracking, trend visualization, anomaly detection, and natural-language querying over private operational data.

**Problem:** Important data was fragmented across external apps, notifications, and manual checks, making it hard to see trends, reference baselines, or ask useful questions of the underlying data.

**System:** I built a dashboard that ingests multiple sources, normalizes event streams, visualizes time-series patterns, and layers in a natural-language query interface for faster interpretation.

**Outcome:** The result is a more interpretable, consolidated monitoring tool that replaces scattered workflows with a single deployable interface.

**Skills gained:** Data product thinking, API integration, event normalization, and the ability to build useful analytical tools under privacy constraints.

### Features
- Data ingestion through external APIs and event logs
- Growth and trend charts plotted against reference standards
- Frequency analysis and anomaly detection
- Natural-language querying over tracked data
- Installable PWA with a dedicated manifest and standalone UX

### Data pipeline
- API polling via Raspberry Pi 5 over a Tailscale-connected mesh network
- IoT notification ingestion written into JSONL event logs
- Proxied through the main server with trusted-header authentication

---

## 🏠 Automation and Home Operations Layer

**Stack:** Home Assistant · YAML Automations · REST API · Tailscale

Designed and maintained an integrated home-operations layer connecting devices, sensors, webhooks, and remote infrastructure into a reliable automation system.

**Problem:** Useful operational data and automation workflows were spread across local devices, smart-home platforms, and cloud services, with limited coordination between them.

**System:** I connected these systems through Home Assistant, webhooks, secure remote networking, and custom endpoints, creating a more unified automation and monitoring layer.

**Outcome:** The setup supports practical household operations, monitoring, alerts, and cross-system workflows rather than isolated one-off automations.

**Skills gained:** Systems integration, applied reliability thinking, API and webhook orchestration, and comfort operating across local and cloud infrastructure.

### What's automated
- Real-time energy monitoring across circuits and solar production
- Lighting scenes and routine-based automations
- Inventory monitoring with reorder alerts
- Smart-device integrations across locks, cameras, thermostats, and other IoT systems
- Webhook-driven triggers and notifications across services

### Infrastructure
- Home Assistant running on Raspberry Pi 5
- Tailscale mesh networking for secure remote access
- Custom webhook endpoints for cross-service communication
- Automated daily health checks

---

## 🔧 Selected Technical Investigations

### Data Portability and API Analysis
- Investigated undocumented application behavior to enable reliable personal-use data portability
- Built a polling and proxy layer that normalized external app data into local storage and downstream dashboards
- Turned a closed data source into a usable component within a broader monitoring system

### Event and Device Telemetry
- Captured and normalized device-generated notification payloads into structured event streams
- Modeled state transitions and event correlations to improve interpretation of noisy real-world signals
- Used this work to support higher-fidelity tracking across connected systems

---

## 🏗️ Infrastructure

### Cloud architecture
- OCI ARM64 instance hosting web applications, dashboards, and AI tooling
- Cloudflare for DNS, CDN, and SSL
- Tailscale mesh networking connecting cloud, home, laptop, and mobile environments
- Caddy reverse proxy with automatic HTTPS

### AI environment
- OpenClaw as the orchestration layer for AI-assisted workflows across Discord, web, and CLI surfaces
- Multi-model orchestration across frontier and local models for cost, latency, and resilience tradeoffs
- Automated fallback behavior when cloud APIs are unavailable

---

## 📈 Selected metrics

- ~36,000 lines of code across deployed projects and tooling
- 20+ handcrafted pages and dashboards
- 200+ git commits across repositories
- 6+ integrated external and internal APIs
- From zero modern web development experience to functional, deployed systems in ~6 weeks

---

## 🛠️ Working method

I use AI pair programming as a force multiplier, not a substitute for judgment.

My role across these projects:

- Defined the problem, constraints, and success criteria
- Translated product intent into highly specific implementation briefs
- Reviewed outputs for architecture, correctness, usability, and maintainability
- Iterated rapidly across desktop and mobile until the product actually worked
- Compared multiple model outputs on important systems and synthesized the best final approach
- Integrated code, infrastructure, data sources, and workflow logic into deployed systems

This workflow let me compress the time required to become effective in modern web development while still owning product direction, quality, and final technical decisions.

---

I built these projects to test how far strong product judgment, domain expertise, and AI-accelerated execution can go in a short period of time. I am especially interested in career opportunities where this combination can be applied to healthcare, biotech, operations, and technical product leadership.

## 📬 Contact

- **Email:** anand@kesavaraju.com
- **LinkedIn:** [linkedin.com/in/anandkes](https://linkedin.com/in/anandkes)
- **Website:** [anand.kesavaraju.com](https://anand.kesavaraju.com)

![Portfolio](screenshots/portfolio-dark.png?v=5)
