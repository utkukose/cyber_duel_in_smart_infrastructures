# ⚡ Cyber Duel in Smart Infrastructures
### Security Analysis with XAI and Digital Twin Perspective
**Simulation Platform for CPS Adversarial Security Scenarios**

> *A zero-dependency, single-file interactive research platform for evaluating adversarial attack and defense dynamics across Cyber-Physical Systems — from smart energy grids to biomedical IoMT devices.*

---

## 🔬 Overview

This platform provides a browser-based simulation environment for studying adversarial machine learning security in Cyber-Physical Systems (CPS). It models the attack-defense interaction as a multi-round duel, integrating **Explainable AI (XAI)** via SHAP attribution and a **Digital Twin** topology layer to visualize how attacks propagate through infrastructure nodes.

The tool was developed as part of a research study on whether ML-based anomaly detection systems are robust against ML-based attacks, and whether XAI and Digital Twin methodologies can provide meaningful contributions to CPS security analysis across domains.

**Key result:** Across 49 attack×defense combinations and 1,470 independent experiments, FDI-Stealthy (physics-constrained False Data Injection) was the only attack to achieve meaningful evasion (avg. ASR 3.6%), while all gradient-based attacks were fully detected. For inverter-based systems, THD dominated SHAP feature attribution at 81.6% across all combinations.

---

## 🚀 Quick Start

No installation, no build step, no dependencies to install.

```bash
git clone https://github.com/YOUR_USERNAME/cyber_duel_in_smart_infrastructures.git
cd cyber_duel_in_smart_infrastructures
open index.html   # or just double-click it
```

The only external resource loaded at runtime is **Chart.js 4.4.1** from the Cloudflare CDN. The platform works offline if you replace that with a local copy.

---

## 🖥️ Interface Tabs

| Tab | Description |
|-----|-------------|
| 🎯 **THREAT-DEFENSE** | Main simulation arena — configure attack/defense, run rounds, watch live canvas animation and battle feed |
| 🔍 **XAI** | SHAP feature attribution per round and globally; perturbation anatomy visualizer |
| 🏗 **DIGITAL TWIN** | Node-level topology showing BREACH / ANOMALY / NORMAL states across the infrastructure graph |
| 📊 **METRICS** | Aggregated statistics: ASR matrix, DR matrix, L₂ norm trends, strength evolution charts |
| 📚 **REFERENCES** | Full annotated bibliography with peer-reviewed status indicators and DOI links |

---

## ⚙️ Configurable Parameters

### Attack Side
| Parameter | Range | Description |
|-----------|-------|-------------|
| Perturbation ε | 0.005 – 0.35 | Perturbation budget (lower = stealthier) |
| Attack Method | 8 options | See attack methods table below |
| Attack Iterations | 1 – 40 | Active only for PGD and GAN-GRID; automatically disabled for single-pass methods (FGSM, JSMA, C&W, FDI-Stealthy, AutoAttack, RL-Agent) |

### Defense Side
| Parameter | Options | Description |
|-----------|---------|-------------|
| Defense Strategy | 7 options | See defense methods table below |

### Physics / Experiment
| Parameter | Range | Description |
|-----------|-------|-------------|
| Voltage Tolerance | ±2% – ±20% | DER voltage deviation limit — relabeled *Dosing Rate Tolerance* in IoMT scenario, *Pulse Amplitude Tolerance* in Pacemaker scenario |
| Frequency Tolerance | ±0.5% – ±5% | DER frequency deviation limit — relabeled *Glucose Range Tolerance* in IoMT scenario, *Pacing Rate Tolerance* in Pacemaker scenario |
| Number of Rounds | 4 – 24 | Rounds per experiment run |

---

## ⚔️ Attack Methods

| Method | Source | ε | Characteristics |
|--------|--------|---|-----------------|
| **GAN-GRID** | Efatinasab et al., ESORICS 2024 | 0.08 | First GAN-based attack for DER; stays within PMU distribution; 99% black-box ASR in original paper |
| **AutoAttack** | Croce & Hein, ICML 2020 | 0.09 | Parameter-free ensemble of APGD-CE + APGD-DLR + FAB + Square Attack; adversarial robustness gold standard |
| **JSMA** | Mutua et al., CRITIS 2024 | 0.10 | Jacobian Saliency Map Attack; sparse — targets top-2 most influential features |
| **FDI-Stealthy** | Tian et al., IEEE TDSC 2024 | 0.13 | Physics-constrained FDI; preserves ΔP∝ΔV and droop control relationships; lowest L₂ with highest ASR |
| **PGD** | Madry et al., ICLR 2018 | 0.10 | Projected Gradient Descent; iterative strong baseline; generates adversarial training data |
| **FGSM** | Goodfellow et al., ICLR 2015 | 0.05 | Fast Gradient Sign Method; single-step; speed-effect comparison reference |
| **C&W** | Carlini & Wagner, IEEE S&P 2017 | 0.08 | L₂-minimizing optimization attack; stealth-focused; low ASR against Mahalanobis detectors |
| **RL-Agent** ⚠ | Hypothetical (IEEE TDSC 2024-based) | 0.07 | Q-learning adaptive attacker; learns from defender feedback each round; counterfactual analysis only |

> ⚠ RL-Agent and the Pacemaker ICD scenario are hypothetical constructs for counterfactual analysis. No real-world AI-based DER attack of this type is documented.

---

## 🛡️ Defense Methods

| Method | Category | Source | Avg. DR |
|--------|----------|--------|---------|
| **Bayesian-LSTM + JEM** | Deep learning + Bayesian uncertainty | Efatinasab et al., SEGAN 2025 | 99.6% |
| **GRU Adversarial Training** | Deep learning + adversarial training | Efatinasab et al., SEGAN 2025 | 99.4% |
| **Ensemble-XAI** | Ensemble ML + SHAP attribution | Farsi et al., Sci. Reports 2026 | 98.9% |
| **AdvTrain** | PGD-based adversarial training | Madry et al., ICLR 2018 | 98.8% |
| **MTD** | Moving Target Defense (non-ML) | Abdi, HBKU 2024 | 100.0% |
| **Feature Squeezing** | Pre-processing heuristic (non-ML) | Classic literature | 100.0% |
| **Randomization** | Input transformation (non-ML) | Classic literature | 99.6% |

---

## 🌍 Real-World Scenarios

Eight scenarios are pre-loaded via the scenario strip. Clicking a scenario auto-fills all parameters.

| # | Scenario | Attack | Defense | Domain Standard |
|---|----------|--------|---------|-----------------|
| 0 | 🇺🇸 sPower / Utah 2019 | JSMA | Ensemble-XAI | IEEE 1547-2018 / NERC CIP |
| 1 | 🔌 EV Fleet Hijack | GAN-GRID | Bayesian-LSTM | IEC 61851-1 / OCPP 2.0.1 |
| 2 | ☀️ Solar Farm SCADA | AutoAttack | Ensemble-XAI | IEEE 1547-2018 / VDE 4105 |
| 3 | ⚡ Microgrid Freq Attack | PGD | MTD | ENTSO-E P1 / IEC 62898 |
| 4 | 🌬️ German Wind 2022 | FDI-Stealthy | GRU-AdvTrain | VDE-AR-N 4120 / NC RfG |
| 5 | 🤖 AI-Augmented sPower ⚠ | RL-Agent | Bayesian-LSTM | IEEE 1547-2018 (hypothetical) |
| 6 | 🏥 Hospital IoMT / Insulin Pump | FDI-Stealthy | Bayesian-LSTM | FDA 21 CFR 820 / IEC 60601-1 |
| 7 | 💓 Pacemaker ICD Attack ⚠ | JSMA | Ensemble-XAI | ISO 14117 / IEC 60601-2-31 |

---

## 🧠 Technical Implementation

### Architecture
The entire platform is a **single HTML file (~995 lines)** with no build toolchain, no framework, and no backend. Everything runs client-side.

```
index.html
├── CSS (lines 8–104)       — CSS variables, grid layouts, animations
├── HTML (lines 106–289)    — Tab panels, scenario strip, control cards
└── JavaScript (lines 290–1027)
    ├── Physics engine       — Cholesky-correlated PMU synthesis
    ├── Attack algorithms    — FGSM, PGD, C&W, GAN-GRID, AutoAttack, JSMA, FDI, RL
    ├── Defense / detection  — Mahalanobis + dynamic threshold + defense-specific logic
    ├── XAI engine           — SHAP attribution, perturbation anatomy
    ├── Digital Twin         — Node state management, topology rendering
    ├── Canvas animation     — requestAnimationFrame battle visualization
    ├── Chart.js charts      — Strength, ASR/DR trends, SHAP bars, L₂ scatter
    └── Scenario manager     — 8 scenario presets with real-world context
```

### Physics Model
PMU feature synthesis uses **Cholesky decomposition** of a 6×6 correlation matrix (IEEE Std 1159 / IEC 61000-4-30 compliant):

```
Features: [Voltage (pu), Frequency (pu), Active Power (pu), THD (pu), Phase Imbalance, RoCoF]

Key correlations modeled:
  V ↔ P:    ρ ≈ 0.65  (voltage sag with active power drop)
  f ↔ RoCoF: ρ ≈ 0.78  (frequency and rate-of-change are mathematically linked)
  V ↔ THD:  ρ ≈ 0.45  (inverter-based DER V-THD coupling)
```

Noise scale and operating point offset vary per scenario (e.g., tighter for microgrid islanding, noisier for EV EVSE metering).

### Anomaly Detection
Detection uses **Mahalanobis distance** with a **Welford online algorithm** sliding window (n=30) that continuously updates μ and σ — mimicking real IDS adaptive behavior (Liang et al. 2017; Tian et al. IEEE TDSC 2024).

```javascript
// Dynamic threshold formula
const learnFactor = Math.max(0.75, 1 - (DYN.n / 120) * 0.25);
const thr = BASE_THR[strategy] * learnFactor * (1 - defenderStrength * 0.22);
```

Defense-specific augmentations:
- **Bayesian-LSTM**: Joint Entropy + Mutual Information uncertainty term added to anomaly score
- **Ensemble-XAI**: SHAP-weighted feature distance boost
- **MTD**: Time-varying feature basis rotation (φ = f(Date.now()))
- **Feature Squeezing**: 3-bit quantization pre-processing
- **Randomization**: Gaussian noise injection at inference time

### FDI-Stealthy Implementation
Physics-constrained perturbation that preserves AC power flow feasibility:

```javascript
function fdi(s, e) {
  const dv = (Math.random() - 0.5) * e * 0.8;
  const df = dv * 0.25 + ...;   // f-V droop control coupling
  const dp = dv * 1.75 + ...;   // P-V sensitivity
  p[3] += Math.abs(dv) * 0.12;  // THD increases with V distortion
  p[4] += Math.abs(dp) * 0.08;  // Phase imbalance follows P change
}
```

### RL-Agent
Q-learning attacker with ε-greedy policy. Action space = `[target_feature, ε_multiplier]` pairs. Reward: +1 for successful evasion, −1 for detection. Q-table persists across rounds within a single run.

---

## 📊 Key Experimental Findings

Results from 49 combinations × 30 repetitions × 20 rounds = **29,400 simulation rounds**:

| Finding | Result |
|---------|--------|
| Only effective attack | FDI-Stealthy — avg. ASR **3.6%** (all others <0.1%) |
| Best overall defense | MTD + FeatureSqueeze — **100% DR** |
| Best ML defense | Bayesian-LSTM — **99.6% DR**, ASR 2.5% vs FDI |
| Most vulnerable combination | FDI-Stealthy vs. AdvTrain — ASR **8.3%** |
| Top SHAP feature | THD — **81.6%** of all combinations |
| MTD anomaly score | **122.0** (vs. 7–15 for all others) — alarm fatigue risk |
| Domain convergence | Biomedical + energy grid scenarios behave similarly — framework is domain-independent |

---

## 📁 Repository Structure

```
cyber_duel_in_smart_infrastructures/
│
├── index.html          ← Entire platform (single file, ~995 lines)
├── README.md           ← This file
└── LICENSE             ← MIT License (see below)
```

No `package.json`, no `node_modules`, no build output. The repo is intentionally minimal — clone and open.

---

## 📚 Selected References

**Attack Methods**
- Efatinasab et al. (2024). GAN-GRID. *ESORICS 2024*, LNCS 14982. https://doi.org/10.1007/978-3-031-70879-4_19
- Croce & Hein (2020). AutoAttack. *ICML 2020*, PMLR 119. https://proceedings.mlr.press/v119/croce20b.html
- Goodfellow et al. (2015). FGSM. *ICLR 2015*. https://arxiv.org/abs/1412.6572
- Madry et al. (2018). PGD / Adversarial Training. *ICLR 2018*. https://arxiv.org/abs/1706.06083
- Carlini & Wagner (2017). C&W. *IEEE S&P 2017*. https://doi.org/10.1109/SP.2017.49
- Tian et al. (2024). FDI-Stealthy / LESSON. *IEEE TDSC 21*(4). https://doi.org/10.1109/TDSC.2022.3213012

**Defense Methods**
- Efatinasab et al. (2025). Bayesian-LSTM + GRU-AdvTrain. *SEGAN 43*, 101799. https://doi.org/10.1016/j.segan.2025.101799
- Farsi et al. (2026). Ensemble-XAI. *Scientific Reports*. https://doi.org/10.1038/s41598-026-35449-x

**CPS Security & Digital Twin**
- Mchirgui et al. (2024). The Applications and Challenges of Digital Twin Technology in Smart Grids: A Comprehensive Review. *Applied Sciences 14*(23). [https://doi.org/10.3390/app142410933](https://doi.org/10.3390/app142310933)
- Salazar et al. (2024). Industroyer I/II analysis. *IEEE S&P 2024*. https://doi.org/10.1109/SP54263.2024.00162

**Biomedical CPS**
- Halperin et al. (2008). Pacemaker/ICD attacks. *IEEE S&P 2008*. https://doi.org/10.1109/SP.2008.31
- Camara et al. (2015). IMD security survey. *J. Biomed. Informatics 55*. https://doi.org/10.1016/j.jbi.2015.04.007

Full annotated bibliography with peer-reviewed status is available inside the **REFERENCES** tab of the application.

---

## ⚠️ Limitations & Scope

- All results are **simulation-based**. No real PMU measurements, clinical telemetry, or live infrastructure data are used.
- Attack algorithms approximate their originals: JSMA uses a gradient proxy vector (GR[]) rather than a true neural network Jacobian; C&W does not run full optimization.
- Biomedical scenarios (IoMT, Pacemaker) use the same Cholesky correlation matrix as energy grid scenarios. They demonstrate **framework extensibility**, not clinical validation.
- RL-Agent and Pacemaker scenarios are labeled ⚠ **Hypothetical** — no real-world counterpart exists for direct comparison.
- Fixed ε values are used across all experiments; real attackers would optimize ε dynamically.
- Single physics profile (sPower/Utah 34.5 kV, 60 Hz, IEEE 1547-2018) used for the systematic 49-combination sweep.

---

## 🔭 Future Work

- Per-scenario 49-combination sweeps (8 × 49 = 392 total combinations)
- ε range scan [0.01, 0.35] — stealth-effectiveness trade-off map
- Validation against real datasets (IEEE 57-bus, ORNL PowerCyber, Arzamasov 2018)
- Bayesian-LSTM + MTD layered defense systematic test
- XAI reporting framework standardization for NIS2 / FDA compliance

---

## 👤 Author

**Prof. Dr. Utku Kose**
SDU, Turkey | UND, USA | VelTech, India | UP, Mexico
utkukose@gmail.com · utkukose@sdu.edu.tr · www.utkukose.com

---

## 📄 License

MIT License — free to use, modify, and distribute with attribution.

```
Copyright (c) 2026 Utku Kose

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
```

---

## 🏷️ Topics

`adversarial-machine-learning` `cyber-physical-systems` `smart-infrastructures` `smart-grid-security` `xai` `explainable-ai` `digital-twin` `iot-security` `iomt-security` `intrusion-detection` `fdi-attack` `gan-grid` `mahalanobis` `shap` `bayesian-lstm` `moving-target-defense` `simulation` `research-tool`
