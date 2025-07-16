# Aave V2 Wallet Credit Scoring System

## Overview
This repository contains a machine learning solution for assigning credit scores (0-1000) to Ethereum wallets based on their transaction history with Aave V2. The system evaluates wallet behavior patterns to assess creditworthiness.

## Methodology

### Data Processing Pipeline
1. **Data Loading**: Reads raw JSON transaction data
2. **Feature Extraction**:
   - Transaction counts (deposits, borrows, repayments)
   - Financial ratios (deposit/borrow, borrow/repay)
   - Time-based features (activity duration, transaction frequency)
   - Risk indicators (liquidation events)
3. **Feature Engineering**:
   - Logarithmic transforms for monetary values
   - Composite metrics (health ratio, behavior score)
4. **Scoring Model**:
   - Isolation Forest for anomaly detection
   - Behavior score for positive patterns
   - Weighted combination of both approaches

### Key Features Considered
- **Responsible Behavior**:
  - High deposit-to-borrow ratios
  - Consistent repayments
  - Long activity duration
- **Risky Behavior**:
  - Frequent liquidations
  - High borrowing with low repayment
  - Short-term "flash loan" patterns

## Usage

### Requirements
- Python 3.7+
- Libraries: pandas, numpy, scikit-learn, matplotlib, seaborn, tqdm

### Installation
pip install -r requirements.txt
Running the Analysis
python credit_scoring.py

Outputs
wallet_credit_scores.csv: All wallets with their credit scores

score_distribution.png: Visualization of score distribution

analysis.md: Summary of findings and example wallets

Score Interpretation
Score Range	Risk Level	Characteristics
900-1000	Excellent	High deposits, consistent repayments, no liquidations
700-899	Good	Healthy ratios, occasional borrowing
400-699	Moderate	Some risky behavior but with mitigations
200-399	Risky	High borrowing, low repayment
0-199	Very Risky	Frequent liquidations, exploit-like patterns

Limitations
Only considers on-chain Aave V2 activity

Doesn't incorporate wallet history outside Aave

Short timeframes may affect score stability

First-time borrowers may be under-scored

Future Improvements
Incorporate DeFi portfolio diversity

Add time-weighted scoring

Include off-chain credit data

Implement real-time scoring updates
