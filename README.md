# Polymarket Data Pipeline

## 🎯 Project Goal: Insider Trading Surveillance Feature Store

The primary objective of this repository is to establish a reliable, historical data backbone required for a machine learning model designed to detect informed trading (insider activity) on prediction markets.

We are treating this repository as the **Data Engineering (ETL) layer**, responsible for transforming raw API responses into clean, relational database tables.

## 💾 Core Data Categories (Database Schema)

The code here focuses on populating three core tables using the Polymarket REST API:

1. **Category I: Market Context (`markets`)**

   * **Data:** Static metadata (Question, Category, Resolution Time) and derived time-series metrics (historical Volatility, Open Interest snapshots).

   * **Purpose:** Provides the necessary contextual features for the ML model.

2. **Category II: Trade Events (`trades`)**

   * **Data:** Every confirmed transaction (Trade ID, Timestamp, Price, Size, Market ID, Taker Wallet Address).

   * **Purpose:** This table holds the **events** that will become the individual rows of our ML training set.

3. **Category III: Wallet Features (`wallets`)**

   * **Data:** Cumulative performance profiles (Realized P&L, Win Rate, Average Position Size) for every active trader.

   * **Purpose:** Provides the "trader history" features, calculated using the historical data in the `trades` table, essential for preventing look-ahead bias in backtesting.

## 🚀 Next Steps (Beyond this Repository)

Once this pipeline is complete and stable, the next phase, which will rely on the clean data stored in this database, will be:

1. **Feature Joining:** Writing the final query to join Categories I, II, and III into the single, wide ML training table.

2. **Labeling:** Defining the target variable Is Informed Trader based on post-trade P&L analysis.

3. **Backtesting & ML:** Training and validating the model using a time-series rolling window approach.

