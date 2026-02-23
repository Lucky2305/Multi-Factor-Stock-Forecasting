# Multi-Factor Portfolio Management with XGBoost & FinBERT

A quantitative trading strategy using Sentiment, Macro, and Technical data.
The strategy focuses on a high-liquidity, 6-stock universe from the Indian market, covering diverse sectors to ensure structural diversification:

Technology: Infosys (INFY)

Banking: HDFC Bank (HDFCBANK)

Consumer Goods: Hindustan Unilever (HUL)

Energy: Reliance Industries (RELIANCE)

Telecom: Bharti Airtel (BHARTIARTL)

Automotive: Mahindra & Mahindra (M&M)

## 1. Multi-Source Data Ingestion
I built a data engine that pulls from four distinct sources:

Technical: Historical price and volume data via Yahoo Finance.

Fundamental: Quarterly financial ratios (ROE, Debt/EBITDA) from MoneyControl.

Macro: Global and domestic economic indicators (VIX, Repo Rate, US 10Y Yield) from FRED.

Sentiment: Daily news headlines processed through FinBERT to quantify market mood.

## 2. Predictive Modeling (XGBoost)
Instead of simple linear models, I utilized an XGBoost Regressor to capture non-linear relationships between macro trends and individual stock returns.

Validation: Used a 70/30 temporal split to prevent data leakage.

Feature Selection: Identified the top 12 most impactful features (including S&P500 returns and Sentiment Scores) from an initial set of 33.

## 3. Portfolio Management & Strategy
I converted raw price forecasts into a managed portfolio:

Top-K Selection: The model ranks the universe daily and selects the top 3 stocks with the highest predicted returns.

Equal-Weight Allocation: Capital is distributed equally (33.3% each) among the top 3 picks to mitigate idiosyncratic risk.

Daily Rebalancing: The portfolio is updated every 24 hours to stay aligned with the latest news and macro shifts.

## Performance Highlights
Total Return: 15.74% (3 Months)

Sharpe Ratio: 6.37

Max Drawdown: -2.18%

## Source
Model: XGBoost Regressor

NLP: FinBERT (HuggingFace)

Data: Yahoo Finance, MoneyControl, FRED API
# Equity Curve: Strategy vs. Benchmark
<img width="963" height="263" alt="Screenshot 2026-02-23 at 6 51 09 PM" src="https://github.com/user-attachments/assets/7711d495-750b-4d46-a6f9-8022b85c3413" />

The strategy achieved a 15.74% return, significantly outperforming the equal-weight benchmark during the test period.


# Daily Retruns of Portfolio
<img width="1262" height="214" alt="Screenshot 2026-02-23 at 11 23 17 PM" src="https://github.com/user-attachments/assets/1a97f5af-9ff6-499c-8d5c-0fe18f9f340a" />

This bar chart illustrates the daily percentage fluctuations of the strategy. Key takeaways include:

Positive Skew: A visual confirmation of the 73.77% Hit Ratio, with green bars (gains) significantly outnumbering red bars (losses).

Volatility Clustering: The model successfully navigated periods of market stress (late October), maintaining controlled return variance.

Outlier Management: Most daily returns are contained within the +/- 1.5% range, demonstrating that the strategy avoids "fat-tail" risks and extreme volatility.
# Portfolio Weight Allocation
<img width="1219" height="480" alt="Screenshot 2026-02-23 at 11 23 30 PM" src="https://github.com/user-attachments/assets/e90e797d-39e5-427e-bc8c-5aa994dcec82" />
The heatmap above visualizes the dynamic rebalancing logic of the strategy across the 6-stock universe.

Allocation Logic
Active Rotation: The model does not follow a "Buy and Hold" approach. Instead, it performs daily rebalancing based on the updated predictions from the XGBoost regressor.

Top-3 Equal Weighting: On any given day, the strategy identifies the three stocks with the highest predicted returns. Each of these three stocks is assigned a 33.3% weight.

Zero-Weight Filter: Stocks that do not rank in the top three—or those with negative predicted returns—are assigned a weight of 0%. This aggressive filtering is what allowed the portfolio to maintain a Max Drawdown of only -2.18%.
