# Imperial College London – ML/AI Course  
## BBO Capstone Project – Stage 2

---

## Project Overview

The Black Box Optimisation (BBO) Capstone Project focuses on optimising eight unknown objective functions under strict constraints. The internal structure of these functions is not known, meaning all optimisation decisions must be based purely on observed input-output pairs.

The goal is to iteratively identify input values that maximise the output of each function. Each week, a single query is submitted per function, and the returned result is used to improve future decisions.

This project reflects real-world machine learning scenarios where:
- data is limited  
- function evaluation is expensive  
- decisions must be made sequentially  

It is directly applicable to problems such as hyperparameter tuning, system optimisation and resource allocation.

---

## Navigating this Repository

## Navigating this Repository

- 📁 [`data/`](./data/)  
  Contains initial datasets and processed data.

- 📄 [`docs/`](./docs/)  
  Contains project documentation:  
  - 📊 [`Datasheet.md`](./docs/Datasheet.md)  
  - 🤖 [`ModelCard.md`](./docs/ModelCard.md)  

- 📓 [`notebooks/`](./notebooks/)  
  Contains weekly optimisation workflows.

- 📦 [`outputs/`](./outputs/)  
  Contains query submissions and results.

- ⚙️ [`src/`](./src/)  
  Contains reusable functions such as Gaussian Process, UCB, and helper utilities.

- 📘 [`README.md`](./README.md)  
  Main project overview and documentation.  

---

## Inputs and Outputs

### Inputs

Each function receives a query vector:

- Values between 0 and 1  
- Rounded to 6 decimal places  
- Hyphen-separated format  

Example (2D):
0.742533-0.325988

Example (8D):
0.070633-0.111808-0.152301-0.000000-0.866908-0.360084-0.290190-0.999999

---

### Outputs

Each query returns a scalar value representing function evaluation.

Examples:
- Function 2 → ~0.70  
- Function 7 → ~3.06  
- Function 8 → ~9.95  
- Function 5 → ~8662  

These outputs act as the optimisation signal.

---

## Challenge Objective

The objective is to maximise the output of each function under the following constraints:

- Only one query per function per week  
- Limited total number of queries  
- Unknown function structure  
- Sequential decision-making  

This introduces a core trade-off:

- Exploration → discovering new regions  
- Exploitation → refining known good regions  

---

## Why Bayesian Optimisation

This problem is well suited to Bayesian Optimisation because:

- Dataset is very small  
- New observations are expensive  
- Function is unknown  

The approach allows:

- Building a surrogate model (Gaussian Process)  
- Quantifying uncertainty  
- Selecting promising regions  
- Iteratively improving performance  

---

## Technical Approach

The optimisation framework uses:

- NumPy  
- GaussianProcessRegressor (Scikit-learn)  
- RBF kernel (via ConstantKernel)  
- Upper Confidence Bound (UCB) acquisition function  

Candidate generation combines:

- Global random sampling (exploration)  
- Local sampling near best point (exploitation)  

---

## Strategy Evolution (Actual Week-by-Week Work)

### Week 1–4: Exploration Phase  
📓 notebooks/01_capstone_workflow_Week1_to_Week4.ipynb  

- Focused on understanding search space  
- Broad exploration  
- No strong model reliance  

---

### Week 5: Model Introduction  
📓 notebooks/02_capstone_workflow_Week5.ipynb  

- Introduced Gaussian Process  
- Started model-guided decisions  
- Mixed global + local sampling  

---

### Week 6: Refinement  
📓 notebooks/03_capstone_workflow_Week6.ipynb  

- Improved surrogate usage  
- Better candidate generation  
- Early signs of useful patterns  

---

### Week 7: Transition to Exploitation  
📓 notebooks/04_capstone_workflow_Week7.ipynb  

- Began refining promising regions  
- Reduced unnecessary exploration  
- Improved stability  

---

### Week 8: Major Strategic Shift  
📓 notebooks/05_capstone_workflow_Week8.ipynb  

- Identified function-specific behaviour  
- Introduced different strategies per function  
- Detected boundary optimisation (Function 5)  

---

### Week 9: Strong Signal Confirmation  
📓 notebooks/06_capstone_workflow_Week9.ipynb  

- Function 5 confirmed as boundary-driven  
- Function 7 and 8 showed strong improvement  
- Increased exploitation  

---

### Week 10: Mature Adaptive Strategy  
📓 notebooks/07_capstone_workflow_Week10.ipynb  

Final strategy:

| Function | Strategy |
|----------|---------|
| F5 | Deterministic boundary (0.999999) |
| F7, F8 | Strong local exploitation |
| F2 | Controlled refinement |
| F1, F3, F4, F6 | Continued exploration |

---

## Key Observations

- Boundary behaviour can dominate (Function 5)  
- Local refinement is effective once signal is strong  
- Exploration is still required for uncertain functions  
- Strategy must adapt per function  

---

## Documentation

- Datasheet: docs/DATASHEET.md  
- Model Card: docs/MODEL_CARD.md  

---

## Datasheet and Model Card Integration

### Datasheet

Documents:
- Query history  
- Dataset composition  
- Collection process  

Key insight:
Sampling becomes increasingly biased toward high-performing regions.

---

### Model Card

Documents:
- Optimisation strategy  
- Model choices  
- Evolution across rounds  

---

### Assumptions and Limitations

Assumptions:
- Functions are smooth enough for GP  
- Local regions provide useful signals  

Limitations:
- Sampling-based optimisation  
- High-dimensional complexity  
- Dependency on early sampling  

---

## Alternatives Considered

- Logistic Regression → not suitable for non-linear data  
- SVM → sensitive to noise  
- Deep Learning → not suitable for small datasets  

---

## Learning Outcomes

- Practical Bayesian optimisation  
- Sequential decision-making  
- Model-based exploration  
- Handling uncertainty in ML systems   

---
