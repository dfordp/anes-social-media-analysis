# Measuring Participation and Visibility in Social Media (ANES 2020–2024)

Link to Paper: [https://drive.google.com/file/d/10vgVEdyvrXEGHSyHmr9WOG7fjswMYZgU/view?usp=sharing](https://drive.google.com/file/d/1uayeDXQC_7SDqXD5hGX4Utdc8hmBdrFJ/view?usp=sharing)

## Overview

This project analyzes how the structure of social media participation has changed between 2020 and 2024 by distinguishing between **platform adoption**, **engagement intensity**, and **visible content production**.

Rather than treating social media platforms as flat populations of users, the analysis explicitly separates:

* who is *on* a platform,
* who *uses it frequently*, and
* who *produces most visible content*.

The project uses publicly available data from the **American National Election Studies (ANES) 2020 and 2024 Time Series**. Elections serve as a **measurement context**, not the substantive focus. The goal is to understand **participation inequality and engagement concentration** in large-scale online platforms.

All analyses are implemented in a **single Jupyter notebook**, emphasizing transparency and reproducibility over software abstraction.

---

## Why ANES?

ANES provides an unusually strong measurement foundation for studying social media participation because it combines:

* nationally representative probability sampling,
* consistent questions across time,
* platform-specific usage indicators,
* frequency measures for both use and posting, and
* validated post-election survey weights.

This combination makes it possible to examine how **visible online activity diverges from platform audiences**, something that cannot be reliably inferred from scraped platform data alone.

---

## Analytical Framework

The core methodological idea is that **visible content is not produced by the same population that adopts platforms**.

To make this explicit, the analysis constructs three engagement tiers:

1. **User-weighted estimates**
   Who reports using a given platform.

2. **Visit-weighted estimates**
   Who consumes content most frequently.

3. **Post-weighted estimates**
   Who produces the majority of visible content.

All estimates use ANES-provided survey weights and are purely descriptive.

---

## Data

* **Source:** American National Election Studies

  * 2020 Time Series
  * 2024 Time Series
* **Population:** U.S. citizens aged 18+ residing in households
* **Mode:** Online and face-to-face interviews
* **Weights:** Post-election full-sample weights (provided by ANES)

All data used are publicly released and accessed in accordance with ANES documentation.

---

## Methodology

### 1. Harmonization Across Waves

Variables are harmonized across 2020 and 2024 to ensure comparability. This includes:

* demographics (age, gender, race/ethnicity, education),
* platform usage indicators,
* frequency of use and posting.

```python
def harmonize_binary(series):
    s = pd.to_numeric(series, errors="coerce")
    return s.where(s.isin([0, 1]))
```

---

### 2. Weighted Estimation

All estimates apply ANES post-election weights. Weighted means and proportions are computed directly rather than relying on unweighted counts.

```python
def weighted_mean(x, w):
    mask = np.isfinite(x) & np.isfinite(w) & (w > 0)
    return np.sum(x[mask] * w[mask]) / np.sum(w[mask])
```

Uncertainty is adjusted using **Kish’s effective sample size** to account for unequal weighting.

---

### 3. Engagement Weighting

To approximate differences between users, visitors, and posters, frequency categories are mapped to relative intensity scores.

Example mapping:

```python
VISIT_FREQ_MAP = {
    "Multiple times per day": 35,
    "Once per day": 21,
    "A few times per week": 7,
    "Once per week": 3,
    "Less than once a week": 1,
    "Never": 0
}

POST_FREQ_MAP = {
    "Multiple times per day": 20,
    "Once per day": 10,
    "A few times per week": 5,
    "Once per week": 2,
    "Never": 0
}
```

Survey weights are multiplied by these intensity values to construct **visit-weighted** and **post-weighted** estimates.

```python
df["visit_weight"] = df["anes_weight"] * df["visit_intensity"]
df["post_weight"] = df["anes_weight"] * df["post_intensity"]
```

These weights are **illustrative** and do not model algorithmic ranking or exposure.

---

### 4. Participation Inequality

The analysis compares:

* platform composition among all users,
* composition among frequent visitors,
* composition among frequent posters.

This reveals how visible discourse can diverge sharply from the user base.

```python
def weighted_share(mask, weight):
    mask = np.asarray(mask, bool)
    w = np.asarray(weight, float)
    ok = np.isfinite(w) & (w > 0)
    return w[ok & mask].sum() / w[ok].sum()
```

---

### 5. Affective Extremity and Activity

The notebook also examines how posting frequency varies with **attitudinal extremity**, using feeling-thermometer differences as a continuous measure.

Respondents are grouped into bins, and weighted mean posting rates are computed within each bin.

```python
bins = np.linspace(0, 100, 9)
df["polarization_bin"] = pd.cut(df["affective_distance"], bins)
```

This shows that while overall posting declines, visible activity becomes increasingly concentrated among highly opinionated users.

---

## Key Findings (Structural)

* Overall social media participation declined modestly between 2020 and 2024.
* Platform use fragmented rather than consolidating.
* Activity became more concentrated among a smaller group of highly engaged users.
* The composition of visible content diverges sharply from the composition of platform audiences.

These patterns suggest that changes in online discourse often reflect **who remains active**, not broad population shifts.

---

## Why This Cannot Be Directly Replicated in India

This analysis depends on the existence of a dataset that combines:

* national representativeness,
* repeated waves,
* platform-specific usage,
* and activity-frequency measures.

No equivalent dataset currently exists for India. Most Indian social media research relies on either:

* platform data (which over-represents high-activity users), or
* surveys that capture adoption but not intensity.

On messaging-first platforms like WhatsApp, where much interaction is private, engagement cannot be measured at scale without institutional access.

---

## Limitations

* All measures are self-reported.
* Engagement weighting approximates intensity, not exposure.
* Results are specific to the U.S. measurement context.
* No causal claims are made.

---

## Reproducibility

All analyses are contained in a single Jupyter notebook.
Running the notebook end-to-end reproduces all figures and summary tables using publicly released ANES data.

---

## Attribution

This is an **independent analysis** of publicly available ANES data.
It does not represent an official ANES publication and does not involve original data collection.

Related descriptive analyses using the same data exist; this project focuses specifically on **measurement and interpretation**, not novelty of data.

just say the word.
