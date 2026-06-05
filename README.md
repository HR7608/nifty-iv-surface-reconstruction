# NIFTY Options IV Surface Reconstruction
## FinClub IIT Roorkee — Open Project 2026

## Problem Statement
Predict missing Implied Volatility (IV) values in the NIFTY 50 
options chain dataset covering January 2026 expiry cycle.

- **Dataset:** 975 timestamps × 28 option columns × 5460 missing values
- **Metric:** Mean Squared Error (MSE) — lower is better
- **Best Kaggle Score:** 0.0002694642

---

## Methodology

### Key Discovery
The IV surface is a **2-factor model**:
- Factor 1: 97.4% variance = overall volatility level  
- Factor 2: 99.3% cumulative = skew steepness

### Models Tried

| Model | Kaggle MSE |
|-------|------------|
| Linear interpolation | 0.0020717237 |
| Neighbour averaging | 0.0014434083 |
| Combined time + strike | 0.0012539798 |
| Extended combined (2 steps) | 0.0005527288 |
| **Rank-2 Iterative PCA** | **0.0002694642** |

### Best Model — Rank-2 Iterative PCA
1. Initialize missing values with column mean
2. Fit Rank-2 PCA on complete matrix
3. Reconstruct using only 2 factors
4. Update missing values with reconstruction
5. Repeat until convergence (converges at iteration 83)

---

## Financial Insights
- CE options exhibit volatility smile (U-shaped curve)
- PE options exhibit volatility skew (downward slope)
- IV evolves smoothly over 5-minute intervals
- Low-rank structure confirms 2-factor IV surface theory

---

## Repository Structure
- `iv_prediction.ipynb` — main notebook with all models
- `submission-converter.ipynb` — converts filled dataset to Kaggle format
- `dataset.csv` — NIFTY options IV dataset

---

## How to Run
1. Open `iv_prediction.ipynb`
2. Run all cells top to bottom
3. `filled_dataset.csv` will be generated
4. Run `submission-converter.ipynb` to generate `submission.csv`
5. Upload `submission.csv` to Kaggle
