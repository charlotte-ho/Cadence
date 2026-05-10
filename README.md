# Cadence
**Demand Flexibility at Fleet Scale**

A software platform that coordinates demand flexibility across a fleet of AI data centers — reducing peak grid load, earning capacity market revenue, and preventing the rebound problem that makes uncoordinated site-level flexibility counterproductive at scale.

Built for PS5715 · Intelligent Energy Systems · Columbia SIPA and SUMA, Spring 2026.

## The Problem

When a grid stress signal reaches 20 large data centers simultaneously, each operator rationally defers load into the same overnight window. Organic diversity in load shapes collapses into artificial synchrony. The resulting rebound spike can exceed the original peak it was designed to relieve.

Uncoordinated flexibility does not eliminate peaks — it moves them.

## The Solution

Cadence holds fleet-level visibility across all enrolled facilities and assigns staggered dispatch windows so no two sites return load simultaneously. This converts hidden data center capacity into reliable, ISO-auditable grid relief — something architecturally impossible for any single-site tool acting alone.

## Live Demo

**[charlotte-ho.github.io/Cadence](https://charlotte-ho.github.io/Cadence/)**

Five enrolled Ashburn colocation facilities · 465 MW total load · No login required.

## Dashboard Screens

| Screen | What It Shows |
|--------|--------------|
| **Fleet Command Center** | Live BMS telemetry per site, fleet flexibility envelope (117 MW), Ashburn corridor map, fleet load curve |
| **Dispatch Engine** | Simulated PJM grid stress event — uncoordinated rebound (+53%) vs. Cadence stagger (−21 MW) |
| **Workload Classifier** | Per-site load breakdown by deferability category, Alibaba PAI empirical grounding, queue wait histogram |
| **Trust — Contract Engine** | Contract terms per site, live LMP oracle, settlement history, human vs. contract-governed dispatch |
| **Revenue Analytics** | Demand charge savings, 5-year ARR trajectory, Q1 2026 dispatch log, FERC Order 2222 tracker |
| **Engine Architecture** | Four proprietary modules, patent pending status, build vs. integrate decision matrix |

## Architecture

**Site layer** — Classifies load into three deferability categories: Critical (real-time inference, firm), Flexible (training jobs, 4–12 hr window), Deferrable (batch inference, 1–4 hr window). Phase 1 operates on BMS telemetry alone.

**Fleet coordination engine** — Four proprietary modules, all patent pending:
- **Workload Classifier** — translates scheduler telemetry into ISO-readable flexibility signals
- **Flexibility Forecaster** — predicts deferrable MW on a 4–6-hour horizon (gradient boosting)
- **Stagger Optimizer** — assigns unique deferral windows fleet-wide via Google OR-Tools
- **Baseline Defense Engine** — computes ISO-auditable counterfactual load for PJM M&V compliance

**Market layer** — Demand charge reduction (Day 1) → PJM capacity market (Year 2) → queue acceleration advisory and utility flexibility data (Year 3+).

## Prototype Parameters

| Parameter | Value |
|-----------|-------|
| Enrolled sites | Stack Infrastructure · Digital Realty · CoreWeave · Equinix · QTS Data Centers |
| Total enrolled load | 465 MW |
| Committed flex | 117 MW (~25% of total load) |
| Stagger windows | 5 unique windows across 8 hours (10pm – 6:30am) |
| Dispatch horizon | 4–12-hour rolling window |
| Q1 2026 dispatch log | 14 events · $329/MW-day PJM clearing · $68,200 fleet earnings |

## Technology

Single-file React 18 application. Open `index.html` directly in any browser — no build step, no backend.

- **Visualization** — Hand-drawn SVG (charts, Gantt timelines, Ashburn corridor map)
- **Fonts** — Space Grotesk · DM Mono
- **Optimizer** — Google OR-Tools constraint satisfaction (simulated in prototype)

## Market Context

- **$2.5B TAM** across four revenue layers (demand charges, capacity market, utility data, queue advisory)
- **$329/MW-day** PJM RPM clearing price, 2026/27 auction
- **26%** of Virginia's statewide electricity from Ashburn corridor facilities
- Regulatory tailwinds: White House Ratepayer Protection Pledge (March 2026) · FERC Large Load Rulemaking (April 2026)

## Team

Charlotte Ho · Corey McDonald · Lars Birhanzel · Yifei Wang
Instructor: Prof. Joe Hao

## Key References

- Weng et al. *MLaaS in the Wild.* USENIX NSDI 2022. [Alibaba PAI gpu-v2020 trace](https://github.com/alibaba/clusterdata)
- Shehabi et al. *2024 US Data Center Energy Usage Report.* LBNL.
- PJM Interconnection. *RPM Capacity Auction Results 2026/27.*
- White House. *Ratepayer Protection Pledge.* March 2026.
- FERC. *Large Load Interconnection Rulemaking.* April 2026.
