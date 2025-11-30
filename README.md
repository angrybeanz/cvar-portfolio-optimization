# CVaR Portfolio Optimization in Python  
*A Convex Optimization Approach to Tail-Risk Minimization*
---

## Overview

This project implements **portfolio optimization using Conditional Value-at-Risk (CVaR)** — a modern risk measure widely used across quantitative finance, asset management, and risk regulation (Basel III / FRTB).

The notebook constructs and compares:

1. **Mean–Variance Optimization (Markowitz Model)**  
2. **CVaR Optimization (Rockafellar–Uryasev Model)**  

using real price data from:
AAPL, MSFT, GOOG, AMZN, TSLA (2023)


The workflow includes:

- Return computation  
- Mean–variance optimization  
- CVaR minimization (convex)  
- Out-of-sample validation  
- Bootstrap weight stability analysis  
- Sensitivity studies  
- Efficient frontier visualization  

This gives a complete, graduate-level demonstration of **risk modeling, convex optimization, and portfolio analysis**.

---

## Motivation

Variance penalizes upside and downside volatility equally — a known weakness of classical Markowitz portfolios.

👉 **CVaR focuses specifically on extreme downside losses.**  
It answers:

> “On the worst 5% of days, how much do we expect to lose?”

This makes CVaR indispensable for:

- Risk management  
- Hedge funds  
- Stress testing  
- Regulatory reporting  
- Portfolio construction under downside-risk constraints  

---

## Mathematical Formulation

### **Mean–Variance Optimization (Markowitz)**

\[
\max_{w} \ \mu^\top w - \gamma w^\top \Sigma w
\]

subject to:

- \( w_i \ge 0 \)  
- \( \sum_i w_i = 1 \)  
- \( w_i \le 0.3 \)  

---

### **CVaR Optimization (Rockafellar–Uryasev)**

Define portfolio loss:

\[
L_t = -r_t^\top w
\]

Minimize empirical CVaR:

\[
\min_{w, v, u} \ \ v + \frac{1}{\alpha N} \sum_{t=1}^{N} u_t
\]

subject to:

- \( u_t \ge 0 \)  
- \( u_t \ge L_t - v \)  
- \( w_i \ge 0, \ \sum_i w_i = 1, \ w_i \le 0.3 \)  

This formulation is **convex** and solved using **CVXPY (CLARABEL solver)**.

---

## Project Structure

CVaR-Portfolio-Optimization/
│
├── notebooks/
│ └── CVaR.ipynb # Full analysis, optimization, plots
│
├── figures/
│ ├── weights_comparison.png
│ ├── test_loss_hist.png
│ ├── weights_bootstrap_box.png
│ ├── sensitivity_plot.png
│ └── weights_vs_probability.png
│
└── README.md # You are here


---

## Results Summary

### **Mean–Variance vs CVaR Weights**

- CVaR de-allocates from **TSLA** (highest tail risk)  
- CVaR increases weight in **AAPL**, which had comparatively lower downside tail risk in 2023

### **Risk Metrics (Full Sample)**

| Metric | Mean–Variance | CVaR |
|-------|---------------|------|
| Annual Volatility | 0.224 | **0.206** |
| CVaR(5%) | 0.0238 | **0.0237** |
| Sharpe Ratio | 2.86 | **2.88** |

➡ **CVaR achieves similar returns but lower tail risk and lower total volatility.**

---

## Out-of-Sample Backtest

- CVaR portfolio generalizes well  
- Tail-loss estimates remain stable across test set  
- Risk reduction persists even without retraining  

---

## Installation

```bash
git clone https://github.com/yourusername/CVaR-Portfolio-Optimization.git
cd CVaR-Portfolio-Optimization
pip install -r requirements.txt
```
## License
MIT License 

## Acknowledgements
This implementation is inspired by the Rockafellar–Uryasev CVaR formulation and classical portfolio optimization literature.
