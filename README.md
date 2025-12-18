# 🎮 Cookie Cats A/B Testing – Decision‑Focused Experimentation (Industry Grade)

## 📌 Project Overview

This project presents an **end‑to‑end, industry‑style A/B testing analysis** conducted on the *Cookie Cats* mobile game dataset (~90,000 users). The goal was to evaluate whether moving a progression gate from **Level 30 (Control)** to **Level 40 (Treatment)** improves engagement **without harming user retention**.

Unlike typical notebook‑only analyses, this project mirrors how **product data science teams** operate:

* Experiment sanity checks (SRM)
* Robust statistical inference
* Power validation
* Business impact estimation
* Clear ship / no‑ship recommendation

---

## 🧠 Business Context

In free‑to‑play mobile games, **early retention directly drives lifetime value (LTV)**. Progression gates are often introduced to increase engagement, but excessive friction can lead to churn.

**Business Question:**

> Should the progression gate be moved from Level 30 to Level 40?

**Primary Metric (North Star):**

* **7‑day retention** (proxy for long‑term value)

**Secondary / Guardrail Metrics:**

* 1‑day retention
* Engagement (number of game rounds)

---

## 🧪 Experiment Design

* **Control:** Gate at Level 30 (`gate_30`)
* **Treatment:** Gate at Level 40 (`gate_40`)
* **Users:** ~90,189 players
* **Split:** Approximately 50/50 randomized allocation

---

## 🔍 Analysis Workflow & Results

### 1️⃣ Sanity Check – Sample Ratio Mismatch (SRM)

Before analyzing outcomes, experiment integrity was validated using a **chi‑square SRM test**.

**Observed allocation:**

* gate_30: 44,700 users
* gate_40: 45,489 users

**SRM Test Result:**

* p‑value = **0.0086** (statistically detectable imbalance)

**Interpretation:**
With a large sample size (~90k users), small allocation deviations (~1%) can become statistically detectable. The imbalance magnitude was operationally small and did not materially affect directional conclusions.

To ensure robustness, results were validated using:

* Bootstrap‑based uncertainty estimation
* Power analysis confirming sufficient sensitivity
* Consistent effect direction across metrics

📌 **Conclusion:** Results are treated as **directionally reliable**, with a recommendation to audit the experimentation pipeline before rerunning.

---

### 2️⃣ Data Cleaning & Exploration

* Engagement (`sum_gamerounds`) is **highly right‑skewed**
* One extreme outlier (~49k rounds) heavily distorts averages

**Action Taken:**

* Removed the extreme outlier to enable robust comparisons
* Used log‑scaled visualizations for interpretability

---

### 3️⃣ Retention Analysis (Bootstrap Inference)

Retention metrics are binary and influenced by skewed engagement behavior.

**Method:**

* Non‑parametric bootstrap (1,000 iterations)
* Estimated distribution of Treatment − Control differences

#### 📊 Results

**1‑Day Retention**

* gate_30: **44.82%**
* gate_40: **44.23%**
* Probability treatment is worse: **95.3%**

**7‑Day Retention (Primary Metric)**

* gate_30: **19.02%**
* gate_40: **18.20%**
* Absolute difference: **−0.82%**
* Probability treatment is worse: **99.9%**

📌 Interpretation: Gate 40 shows a **clear and highly confident negative impact** on long‑term retention.

---

### 4️⃣ Engagement Analysis (Mann–Whitney U Test)

Engagement is heavy‑tailed and non‑normal.

**Method:** Mann–Whitney U test (non‑parametric)

**Results:**

* Avg rounds (gate_30): 51.34
* Avg rounds (gate_40): 51.30
* p‑value: 0.0509

📌 Interpretation: **No meaningful engagement improvement**, despite increased friction.

---

## 📊 Experiment Power Analysis

To validate experimental sensitivity, a power analysis was conducted.

**Assumptions:**

* Baseline 7‑day retention ≈ 18%
* Minimum Detectable Effect (MDE): 1% absolute
* Power: 80%, α = 0.05

**Result:**

* Required sample per group: ~23,664
* Actual sample per group: ~45,094

✅ **Conclusion:** Experiment was sufficiently powered to detect business‑relevant effects.

---

## 💰 Business Impact Simulation

Statistical significance alone is insufficient for decision‑making.

**Illustrative Assumptions:**

* Each 7‑day retained user ≈ ₹500 lifetime value

**Estimated Impact:**

* ~0.82% absolute drop in 7‑day retention
* ~818 fewer retained users per 100k players
* **Estimated revenue risk:** ~₹4.1 lakh per 100k users

📌 Even small retention drops translate into **material long‑term revenue loss**.

---

## 🔎 Segmented Analysis

Users were segmented by engagement level (above vs below median rounds).

**Findings:**

* Absolute retention drop is larger among **high‑engagement users**
* Low‑engagement users remain fragile overall, compounding churn risk

📌 Insight: Average effects hide risk; segmentation reveals who is most impacted.

---

## 🧾 Final Decision Memo

**Primary Metric:** 7‑day retention
**Guardrail Metric:** Engagement

* Retention ↓ (statistically & practically significant)
* Engagement ≈ flat
* Downside risk outweighs any potential upside

### ✅ Final Recommendation

**DO NOT DEPLOY** — retain the progression gate at **Level 30**.

---

## 🚧 Limitations

* Observational analysis on historical experiment data
* Revenue values are simulated for illustration
* No long‑term cohort or monetization breakdown

---

## 🚀 Future Work

* Audit and rerun experiment to address SRM
* Targeted gating experiments for high‑engagement users

---

## 🧠 Key Skills Demonstrated

* Experiment design & validation (SRM, power analysis)
* Non‑parametric statistical inference
* Bootstrap uncertainty estimation
* Segmentation & decision analysis
* Translating metrics into business impact

