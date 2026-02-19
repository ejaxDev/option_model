# 🚀 SPY 0DTE Options Profitability Prediction Model

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![XGBoost](https://img.shields.io/badge/ML-XGBoost-orange.svg)](https://xgboost.readthedocs.io/)

A machine learning system for predicting SPY 0-Day-to-Expiration (0DTE) options profitability using real-time market data and technical indicators.

## 🎯 Overview

This project implements a comprehensive machine learning pipeline to predict whether SPY options will be profitable by 3:30 PM Eastern on their expiration date. The model uses high-frequency market data, technical indicators across multiple timeframes, and walk-forward validation to provide realistic performance estimates.

### 🎪 Key Features

- **Real-time Data**: Polygon.io API integration for live SPY and options pricing
- **Multi-timeframe Analysis**: Features across 5m, 10m, 15m, 30m, 1h, and 2h windows
- **Rigorous Validation**: Walk-forward time series validation prevents data leakage
- **Production Ready**: Model calibration and comprehensive performance metrics
- **0DTE Focus**: Specialized for same-day expiration options trading

## 📊 Model Performance

- **Overall Accuracy**: ~57-62% (varies by market conditions)
- **AUC Score**: 0.55-0.65 (consistently above random)
- **Training Period**: 2022-2025 market data
- **Prediction Horizon**: Intraday to 3:30 PM Eastern

## 🛠 Technical Architecture

### Data Sources
- **Underlying**: SPY ETF 5-minute aggregated data
- **Options**: 0DTE SPY calls and puts within ±2% of opening price
- **Provider**: Polygon.io real-time and historical market data

### Feature Engineering (48 features)
1. **Price Features**: Current prices, position in daily/rolling ranges
2. **Technical Indicators**: Rolling mins/maxs, volatility across timeframes
3. **Momentum**: Price changes over multiple lookback windows
4. **Directional Volatility**: Volatility weighted by price direction
5. **Timing**: Time since market open, time until close
6. **Performance**: Cumulative returns since market open
7. **Moneyness**: Side-aware distance from At-The-Money

### Model Framework
- **Algorithm**: XGBoost Gradient Boosted Trees
- **Task**: Binary Classification (Profitable vs Unprofitable)
- **Validation**: Walk-forward time series validation
- **Calibration**: Probability calibration assessment

## 🚀 Quick Start

### Prerequisites
```bash
pip install -r requirements.txt
```

### Required Packages
- `pandas`, `numpy` - Data manipulation
- `xgboost` - Machine learning model
- `sklearn` - Model evaluation metrics
- `matplotlib` - Visualization
- `polygon-api-client` - Market data (requires API key)

### Environment Setup
1. Obtain Polygon.io API key
2. Create `.env` file:
```env
POLYGON_API_KEY=your_api_key_here
```

### Execution
```python
# Open and run the Jupyter notebook
option_model.ipynb
```

## 📁 Repository Structure

```
option_model/
│
├── option_model.ipynb          # Main analysis notebook
├── option_model_analysis.ipynb # Additional analysis (optional)
├── requirements.txt            # Python dependencies
├── README.md                  # This file
└── .env                       # API credentials (create this)
```

## 🔄 Workflow

1. **Data Collection**: Fetch SPY minute data + options universe
2. **Feature Engineering**: Calculate 48 technical indicators across timeframes
3. **Target Definition**: Binary profitability by 3:30 PM
4. **Model Training**: XGBoost with walk-forward validation
5. **Performance Analysis**: Accuracy, AUC, calibration assessment
6. **Export Results**: Save predictions for backtesting/deployment

## 📈 Use Cases

- **Algorithmic Trading**: Automated 0DTE options selection
- **Risk Management**: Probability-based position sizing
- **Market Research**: Understanding intraday options dynamics
- **Educational**: Learning options pricing and ML feature engineering

## ⚠️ Important Disclaimers

1. **Educational Purpose**: This model is for educational and research purposes
2. **No Financial Advice**: Not intended as investment advice
3. **Past Performance**: Historical results don't guarantee future performance
4. **Market Risk**: Options trading involves substantial risk of loss
5. **API Costs**: Polygon.io may charge for high-volume data usage

## 🔧 Advanced Configuration

### Model Parameters
The XGBoost model uses conservative parameters to prevent overfitting:
- `n_estimators`: 300 (boosting rounds)
- `max_depth`: 4 (tree depth)
- `learning_rate`: 0.05 (conservative)
- `min_child_weight`: 15 (regularization)

### Feature Customization
Features can be modified in the `train_columns` list:
- Add/remove timeframe windows
- Adjust rolling calculation periods
- Include additional technical indicators

### Validation Methodology
Walk-forward validation ensures realistic performance:
- Train on historical years
- Test on future years
- No data leakage
- Chronological integrity maintained

## 📚 Research Background

This project builds on quantitative finance research in:
- **Options pricing models** (Black-Scholes extensions)
- **Technical analysis** (momentum, mean reversion)
- **Machine learning in finance** (feature engineering, validation)
- **High-frequency trading** (intraday patterns)

## 🤝 Contributing

Contributions welcome! Areas for enhancement:
- Alternative ML algorithms (Random Forest, Neural Networks)
- Additional technical indicators
- Options Greeks integration
- Real-time deployment infrastructure
- Backtesting framework

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 📞 Support

For questions or issues:
1. Check existing GitHub issues
2. Create new issue with detailed description
3. Include error messages and environment details

---

**⚡ Ready to explore the fascinating world of 0DTE options prediction!**

*Remember: Options trading involves substantial risk. Always do your own research and consider consulting with financial professionals.*
