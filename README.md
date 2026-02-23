#Multi-Factor Portfolio Management with XGBoost & FinBERT

A quantitative trading strategy using Sentiment, Macro, and Technical data.
The strategy focuses on a high-liquidity, 6-stock universe from the Indian market, covering diverse sectors to ensure structural diversification:

Technology: Infosys (INFY)

Banking: HDFC Bank (HDFCBANK)

Consumer Goods: Hindustan Unilever (HUL)

Energy: Reliance Industries (RELIANCE)

Telecom: Bharti Airtel (BHARTIARTL)

Automotive: Mahindra & Mahindra (M&M)

1. Multi-Source Data Ingestion
I built a data engine that pulls from four distinct sources:

Technical: Historical price and volume data via Yahoo Finance.

Fundamental: Quarterly financial ratios (ROE, Debt/EBITDA) from MoneyControl.

Macro: Global and domestic economic indicators (VIX, Repo Rate, US 10Y Yield) from FRED.

Sentiment: Daily news headlines processed through FinBERT to quantify market mood.

2. Predictive Modeling (XGBoost)
Instead of simple linear models, I utilized an XGBoost Regressor to capture non-linear relationships between macro trends and individual stock returns.

Validation: Used a 70/30 temporal split to prevent data leakage.

Feature Selection: Identified the top 12 most impactful features (including S&P500 returns and Sentiment Scores) from an initial set of 33.

3. Portfolio Management & Strategy
I converted raw price forecasts into a managed portfolio:

Top-K Selection: The model ranks the universe daily and selects the top 3 stocks with the highest predicted returns.

Equal-Weight Allocation: Capital is distributed equally (33.3% each) among the top 3 picks to mitigate idiosyncratic risk.

Daily Rebalancing: The portfolio is updated every 24 hours to stay aligned with the latest news and macro shifts.

#Performance Highlights
Total Return: 15.74% (3 Months)

Sharpe Ratio: 6.37

Max Drawdown: -2.18%

#Source
Model: XGBoost Regressor

NLP: FinBERT (HuggingFace)

Data: Yahoo Finance, MoneyControl, FRED API
