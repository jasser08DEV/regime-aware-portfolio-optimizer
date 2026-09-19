#Regime-Aware Portfolio Optimizer (v1)

A small project combining Modern Portfolio Theory (Markowitz mean-variance optimization) with an unsupervised ML layer (K-Means clustering) to detect market regimes. This is a v1 / scoped submission — see Limitations & Next Steps for what's planned beyond this version.

What This Project Does
Portfolio Optimization (Finance): Pulls historical price data for a basket of assets and uses Modern Portfolio Theory to compute the efficient frontier and identify the max-Sharpe-ratio portfolio — the allocation that gives the best risk-adjusted return.
Regime Detection (AI/ML): Uses K-Means clustering on rolling volatility and rolling return of a market index to label historical periods as "calm" or "volatile" market regimes, without any hand-labeled data.
Programming: The full pipeline — data acquisition, optimization, clustering, and visualization — is implemented as a reproducible Python pipeline.
Why This Matters

Static portfolio allocation (set weights once, forget about it) ignores the fact that markets behave very differently in calm vs. turbulent periods. This project is a first step toward adaptive allocation: using unsupervised learning to detect the market's current regime as an input to how a portfolio should be positioned.

Methodology

Data: Daily adjusted close prices for a diversified basket of ~10 assets (equities, an ETF, and a bond/gold proxy) pulled via the yfinance API, covering a multi-year historical window that includes at least one known high-volatility period (e.g., 2020 or 2022) for validation.

Portfolio Optimization: Expected returns and the covariance matrix are computed from historical prices. PyPortfolioOpt is used to solve for the max-Sharpe-ratio portfolio along the efficient frontier, following classical Markowitz mean-variance optimization.

Regime Detection: Two features are engineered from a market index (e.g., SPY): rolling N-day volatility and rolling N-day return. K-Means clustering (K=2) is applied to these features to separate historical time periods into two regimes. Clusters are labeled post-hoc as "calm" or "volatile" based on which one has higher average volatility.

Validation approach: Regime labels are visually checked against known market events. If the "volatile" cluster reliably captures known crash/high-volatility periods, the clustering is considered a reasonable, if simple, regime signal.

Results

(Fill in after running the notebook — include the efficient frontier plot, the regime timeline plot, and 2-3 sentences on what the regime labels captured.)

Efficient frontier plot: outputs/efficient_frontier.png
Regime timeline plot: outputs/regime_timeline.png
Max-Sharpe portfolio weights: (insert table/values)
Repository Structure
regime-aware-portfolio-optimizer/
├── README.md
├── requirements.txt
├── notebook.ipynb          # full pipeline: data → optimization → regime detection → plots
├── data/                   # cached price data (optional, for reproducibility)
└── outputs/                # saved chart images
How to Run
Create a virtual environment and install dependencies: pip install -r requirements.txt
Open notebook.ipynb and run all cells top to bottom.
Charts will render inline and save to outputs/.