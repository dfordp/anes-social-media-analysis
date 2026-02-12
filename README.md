# Participation and Visibility in Online Platforms (2020–2024)

## Overview

This project examines how conclusions about online platforms change when analysis moves beyond counting users to accounting for **engagement intensity and visibility**.

Using publicly released data from the **American National Election Studies (ANES) 2020 and 2024 Time Series**, the analysis distinguishes between:

* platform users,
* frequent visitors, and
* high-intensity contributors (posters).

The core finding is structural rather than topical: **visible content on social media platforms is produced by a much smaller and more active subset of users**, and trends inferred from visible activity can diverge substantially from trends at the population level.

While elections provide the measurement context, the project’s focus is on **participation inequality, engagement concentration, and measurement**, not political outcomes.

---

## Motivation

Most analyses of social media rely on one of two data sources:

1. platform-generated metrics or scraped content, which over-represent highly active users, or
2. surveys that capture adoption but not intensity.

This creates a common interpretive error: **treating visible content as representative of platform users or the broader population**.

ANES offers a rare opportunity to address this problem. It combines:

* nationally representative sampling,
* repeated measurement across time,
* platform-specific usage indicators, and
* frequency measures for both use and posting.

This makes it possible to study social media as a **layered participation system**, rather than a flat public square.

---

## What This Project Does

The analysis focuses on three related questions:

1. How has overall participation in major social media platforms changed between 2020 and 2024?
2. How does platform composition differ when measured at the level of users, visits, and posts?
3. How does engagement concentration affect the interpretation of visible online activity?

To answer these, the project constructs three engagement tiers:

* **User-weighted estimates** (who is on a platform),
* **Visit-weighted estimates** (who consumes content most frequently),
* **Post-weighted estimates** (who produces most visible content).

This approach highlights how conclusions can shift depending on the unit of analysis.

---

## Data

* **Source:** American National Election Studies (ANES)

  * 2020 Time Series Study
  * 2024 Time Series Study
* **Population:** U.S. citizens aged 18+ residing in households
* **Sampling:** Address-based probability samples, administered online and face-to-face
* **Weights:** Post-election full-sample weights provided by ANES

All data used in this project are **publicly available** and accessed in accordance with ANES documentation and usage guidelines.

> Note: Findings describe U.S. citizens and are not intended to generalize to all adults or to non-U.S. contexts.

---

## Methodology

### Engagement Weighting

Survey weights are combined with frequency-derived intensity scores to approximate differences between:

* platform audiences,
* engagement volume, and
* visible content production.

Frequency categories are mapped to relative intensity values to construct visit- and post-weighted estimates. These are intended to be **illustrative**, not to model platform algorithms or exposure mechanisms.

### Analytical Scope

* All analyses are **descriptive**
* No causal claims are made
* Results focus on compositional change and measurement implications

Robustness checks include light winsorization of survey weights and effective sample size corrections for uncertainty estimation.

---

## Key Takeaways

* Overall platform participation has declined modestly, while usage has become more fragmented.
* Activity has become increasingly concentrated among a smaller subset of highly engaged users.
* The composition of visible content can differ sharply from the composition of platform users.
* Engagement-aware metrics are essential for interpreting trends in online discourse.

These patterns suggest that changes in what is seen online often reflect **who remains active**, rather than broad shifts in population behavior.

---

## Why ANES?

ANES serves as an enabling measurement infrastructure rather than a topical focus. Comparable analyses are difficult to replicate in many other countries due to the absence of datasets that combine:

* national representativeness,
* repeated waves,
* platform-specific usage, and
* activity-frequency measures.

As a result, this project should be understood as a **methodological case study** enabled by unusually strong data, not a universal template.

---

## Limitations

* Analysis is limited to platforms included in ANES questionnaires.
* Activity weighting approximates relative intensity and does not capture algorithmic amplification.
* Results are specific to the U.S. context and measurement environment.

---

## Code and Reproducibility

This repository contains code used to reproduce all figures and summaries presented in the accompanying analysis using publicly released ANES data.

The code is provided for transparency and reproducibility and does not include any proprietary data or tools.

---

## Attribution and Scope

This project is an **independent analysis** of publicly available ANES data.
It does not represent an official ANES publication, nor does it involve original data collection.

Related descriptive analyses using the same data exist; this project focuses specifically on **measurement and interpretation** rather than novel data or causal inference.

