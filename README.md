# Integrated Black-Litterman & Machine Learning Framework for Quantitative Portfolio Optimization

## 📌 Project Overview
This project implements a hybrid quantitative investment strategy combining the **Black-Litterman model**, **mean-variance optimization**, and **machine learning (Learning-to-Rank)**.  
The goal is to construct robust and diversified portfolios that outperform a market benchmark while maintaining lower volatility and stronger downside protection.

The strategy is backtested on CRSP/Compustat data, covering U.S. equities from **2015–2024**.

---

## 📊 Methodology

### 1. Data Processing
- Assign sector labels to each stock  
- Align JKP factor data with market data  
- Generate next-period stock returns  
- Normalize rankings (0–100) for LTR model training  

---

### 2. Black-Litterman Model
The BL model integrates:
- **Market equilibrium returns** (via reverse optimization)
- **Investor views** (generated using Learning-to-Rank)

Formulations used:
- Implied equilibrium returns:  
  `m = λ · Σ · w_cap`
- Prior uncertainty:  
  `Ψ = τ · Σ`

Parameters:
- **τ = 0.01**  
- **Ω = 0.0001** (high confidence in equilibrium)

---

### 3. Learning-to-Rank (LTR)
We train an **XGBoost pairwise ranking model** to:
- Learn relative ordering of stocks  
- Produce an LTR score used as a view in the BL framework  
- Enhance the allocation process by emphasizing top-ranked stocks  

---

### 4. Portfolio Optimization
A **mean-variance optimizer** is applied on the Black-Litterman posterior returns.

Constraints include:
- Full-budget constraint  
- Max 10% weight per asset  
- Sector exposure caps (max 20%)  
- Size-dependent bounds  
- Turnover limitation  
- Liquidity & volume filters  
- Market-cap reference weights  

---

## 📈 Backtesting
Performance metrics:
- Cumulative returns  
- Rolling 3-year performance  
- Sharpe ratio  
- Volatility  
- Drawdowns  
- Bull vs. Bear market behavior  
- Turnover  

Two versions of the strategy:
- **BL Gross** (without transaction costs)  
- **BL Net** (with transaction costs)

---

## 📉 Results Summary
The Black-Litterman strategies deliver:

- Higher annual & cumulative returns than the benchmark  
- Lower overall volatility  
- Better Sharpe ratios  
- More resilience in bear markets (e.g., COVID crash)  
- Smaller drawdowns  
- Low turnover (minimal difference between gross & net)

The strategy demonstrates robustness, diversification, and practical implementability.

---

## 📚 Data Sources
Data retrieved through **WRDS**:
- **CRSP US Stock Database**  
- **Compustat Global**  
- **JKP Factors**

---

## 🛠 Technologies Used
- Python  
- NumPy / Pandas  
- XGBoost (LTR)  
- CVXOPT / SciPy (Optimization)  
- Matplotlib  
- WRDS API 
