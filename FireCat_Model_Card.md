---
# Hugging Face Model Card metadata (edit as needed)
language:
- en
license: mit
tags:
- fire-risk
- urban-risk
- catboost
- tabular-classification
- interpretability
- shap
datasets:
- NFIRS (2012–2022)
- US Census ZIP-level socioeconomic/building/business data
- NOAA weather
- Meteostat weather
model_name: FireCat
---

# Model Card for FireCat (Urban Building Fire Consequence Prediction)

## Model Summary
**FireCat** is a tree-based, tabular machine learning framework for **event-level prediction of building-fire consequences** in U.S. cities. It predicts three outcomes from National Fire Incident Reporting System (NFIRS) incidents enriched with community, building-stock, business, and weather features: **fire spread**, **human injury risk**, and **economic loss risk**.

## Model Details

### Model Description
This work integrates **over one million** U.S. building fire incident reports (2012–2022) with ZIP-code–level socioeconomic indicators, business composition, building inventories, and weather conditions, and develops a city-level risk framework plus FireCat for consequence prediction.

- **Developed by:** Chenzhi Ma, Shengzhi Luan, Ensheng Dong, Lauren M. Gardner, Hongru Du, Thomas Gernay
- **Model type:** Tree-based gradient boosting for tabular multi-class classification (CatBoost in the released code)
- **Language(s):** English (documentation/code/comments)
- **License:** MIT
- **Finetuned from model:** Not applicable (not an LLM)

### Model Sources
- **Repository / code & data:** https://github.com/Chenzhi-Ma/Fire_risk
- **Paper (arXiv):** *From Occurrence to Consequence: A Comprehensive Data-driven Analysis of Building Fire Risk* (arXiv:2503.22689)

## Uses

### Direct Use
FireCat is intended for **event-level classification** of:
1) **Fire spread** severity (categorical levels defined in the paper),  
2) **Human injury** risk level (Low/Moderate/High),  
3) **Economic loss** risk level (Low/Moderate/High).

Potential users include fire-safety researchers, city risk analysts, and public agencies who need interpretable, data-driven consequence predictions from incident + contextual features.

### Downstream Use
- Integrating FireCat outputs into **city-level risk dashboards** or **resource prioritization** workflows.
- Using FireCat as a baseline model for transfer to other regions (subject to data compatibility and domain shift).

### Out-of-Scope Use
- Real-time emergency dispatch decision-making without additional validation.
- Predictions outside the U.S. NFIRS reporting context (different reporting schemas, building codes, or response systems).
- High-stakes individual-level decisions (e.g., insurance pricing, legal liability) without careful auditing and governance.

## Bias, Risks, and Limitations
- **Reporting bias & missingness:** NFIRS is voluntary and can vary across jurisdictions; recorded incident attributes and loss estimates can be incomplete or noisy. The paper categorizes economic loss partly to reduce reporting uncertainty.
- **Generalization limits:** Model behavior may shift across time, regions, or cities with different reporting practices and built environments.
- **Correlated features:** Many community and incident variables can be correlated; importance/attribution should be interpreted cautiously.
- **Ablation studies not included (paper scope):** The study emphasizes baseline distribution comparison and SHAP-based interpretability, rather than systematically removing feature groups/components. 

### Recommendations
- Validate performance on your target jurisdiction/time period before deployment.
- Use probability thresholds (the paper shows accuracy improves with higher confidence thresholds) when decisions require higher reliability.
- Pair outputs with interpretability (SHAP) and uncertainty-aware policies.

## How to Get Started

### From the released repository
The repo provides notebooks to reproduce the analyses and train models:
- `step2_consequence_fire_spread.ipynb`
- `step2_ceosequence_injury_severity.ipynb`
- `step2_consequence_loss.ipynb`

Minimal starter snippet (adjust paths to your local clone):

```python
import pandas as pd

# Example: load a processed dataset used for consequence modeling
df = pd.read_pickle("data/step2_consequence_fire_spread.pkl")

print(df.shape)
print(df.columns[:30])
```

## Training Details

### Training Data
The study integrates five categories of information:
1) NFIRS incident reports (incident-level building/fire attributes),
2) ZIP-code–level social determinants,
3) ZIP-code–level business proportions,
4) ZIP-code–level building inventories,
5) Weather conditions (NOAA + Meteostat).

Coverage includes 2012–2022 and a large fraction of U.S. metropolitan/micropolitan areas (CBSA-based definition in the paper).

### Training Procedure
- **Algorithm:** CatBoost (tree-based boosting)
- **Targets:** Fire spread (4-class), injury risk (3-class), loss risk (3-class)
- **Baselines:** Probabilistic baseline based on target distribution
- **Interpretability:** SHAP to quantify feature contributions (incident-specific factors tend to dominate)

#### Training Hyperparameters
Hyperparameters are defined in the notebooks in the repository.

#### Software / Dependencies
From the repository documentation (edit if your environment differs):
- Python 3.10+
- catboost
- numpy, pandas, scikit-learn
- shap / matplotlib (for interpretability and plots)
- R + mgcv/gratia (for GAM analyses in the occurrence module, if reproducing that portion)

## Evaluation

### Metrics
Reported metrics include **accuracy, F1, precision, MSE/WMSE, Brier score, and rank probability score (RPS)**.

### Results (from the paper)
FireCat improves over the baseline across all three consequence tasks. Example accuracies reported:
- Fire spread: baseline 0.513 → FireCat 0.574  
- Fire injury: baseline 0.414 → FireCat 0.553  
- Fire loss: baseline 0.401 → FireCat 0.562  

The paper also notes that increasing the **prediction confidence threshold** increases accuracy (useful for selective prediction / abstention strategies).

## Model Examination
SHAP analyses indicate that **incident-specific factors** generally have higher mean SHAP values than local/community factors for consequence prediction.

## Environmental Impact
Not reported. (If desired, estimate CO₂eq using https://mlco2.github.io/impact#compute with your actual training runtime/hardware.)

## Citation

**BibTeX (arXiv):**
```bibtex
@article{ma2025firecat,
  title={From Occurrence to Consequence: A Comprehensive Data-driven Analysis of Building Fire Risk},
  author={Ma, Chenzhi and Du, Hongru and Luan, Shengzhi and Dong, Ensheng and Gardner, Lauren M. and Gernay, Thomas},
  journal={arXiv preprint arXiv:2503.22689},
  year={2025}
}
```

## Model Card Contact
Use the corresponding author contacts listed in the paper, or open an issue on the GitHub repository.
