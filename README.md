📄 [Written Report (PDF)](PL4246_Final_Report_A0253130X.pdf)  
🎥 [Video Presentation (YouTube)](https://youtu.be/FBj2ucsbs4w)

---

## Research Question

> Within a partial-correlation network of STARS items, do Computation Self-Concept
> nodes act as structural bridges — as indicated by betweenness centrality and bridge
> centrality — between the Fear of Statistics Teachers and Fear of Asking for Help domains?

---

## Repository Structure

| Path | Description |
|---|---|
| `PL4246_STARS_Analysis_final.Rmd` | Main analysis script — knit this to reproduce all results |
| `PL4246_STARS_Analysis_final.html` | Pre-knitted HTML output for quick viewing |
| `PL4246_Final_Report_A0253130X.pdf` | Submitted written report |
| `stars-data_132_nodes_added.csv` | Analysis-ready dataset: 132 respondents × 51 STARS items |
| `output/stars_igraph.rds` | Saved igraph network object (load to skip re-estimation) |
| `output/stars_bootnet.rds` | Saved bootnet network object |
| `output/bridge_results.rds` | Saved bridge centrality results |
| `output/sessionInfo.txt` | R and package versions used |
| `tables/` | CSV exports of all four results tables |
| `figures/` | High-resolution PNG outputs for Figures 1 and 2 |

---

## How to Reproduce the Analysis

### Requirements
R (≥ 4.2 recommended). Install required packages once:
```r
install.packages(c("bootnet", "qgraph", "igraph", "networktools",
                   "tidyverse", "car"))
```

### Steps
1. Download or clone this repository and unzip it into a single folder.
2. Open `PL4246_STARS_Analysis_final.Rmd` in RStudio.
3. Set the working directory to the folder containing the `.Rmd` and `.csv` files:
   **Session → Set Working Directory → To Source File Location**
4. Click **Knit** (or run `rmarkdown::render("PL4246_STARS_Analysis_final.Rmd")`).

The script will recreate all figures, tables, and saved objects from scratch.

> ⚠️ **Slow chunks**: the ER null simulation, permutation tests, and bootnet
> bootstraps each take 1–5 minutes. They are marked `cache = TRUE` in the Rmd,
> so subsequent knits skip them automatically.

### Loading saved objects without re-running
If you only want to inspect results without re-running the full pipeline:
```r
g              <- readRDS("output/stars_igraph.rds")
stars_matrix   <- readRDS("output/stars_bootnet.rds")
bridge_results <- readRDS("output/bridge_results.rds")
```

---

## Data

**Source**: pooled from three semesters of PL4246 (2023–2026), administered to NUS
psychology undergraduates (n = 132).  
**Instrument**: Statistics Anxiety Rating Scale (STARS; Cruise, Cash, & Bolton, 1985) —
51 items on a 5-point Likert scale across six domains.  
**File**: `stars-data_132_nodes_added.csv` — columns are named STARS item labels
(e.g. `study`, `too_slow`); each row is one respondent.

---

## Analysis Pipeline Summary

1. **Network construction** — partial-correlation network estimated with `bootnet`,
   significance-thresholded at *p* < .05; converted to an `igraph` object.
2. **Macro-level descriptives** — density, clustering, ASPL; compared against 1,000
   Erdős–Rényi random networks.
3. **Domain-level descriptives** — mean degree and centrality per STARS domain.
4. **Node-level centrality** — weighted betweenness + bridge centrality
   (Jones, Ma, & McNally, 2021).
5. **Inferential tests** — label-permutation tests (10,000 iterations) comparing
   Computation Self-Concept against all other domains; Mann–Whitney U as a
   convergent check.
6. **Robustness** — edge-weight bootstrap and case-drop CS-coefficients (bootnet).

---

## AI Tool Declaration

See declaration at the bottom of `PL4246_STARS_Analysis_final.Rmd` and in the
written report (final page).
