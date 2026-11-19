# Anti-Money Laundering Detection

A project that looks at 5 million bank transactions and tries to find the ones that are part of money laundering. It uses rules, graph analysis, and machine learning to spot suspicious patterns.

Built with Python, LightGBM, and a Streamlit dashboard.

## What It Does

Money launderers leave patterns in transaction data. This project looks for those patterns in three ways:

1. **Rules** — things like money going in circles between accounts, or one account receiving from many sources and sending to many destinations
2. **Anomaly detection** — finding accounts that behave differently from the rest
3. **Machine learning** — a LightGBM model trained on known cases to predict new ones

The results show up in a Streamlit dashboard where you can explore suspicious accounts.

## Results

Out of 5.1 million transactions, about 0.1% are money laundering. The rule-based detectors catch patterns with 34% precision. The machine learning model reaches 99% precision in its top 100 predictions.

## Getting Started

You need Python 3.10+.

```bash
python -m venv .venv
.venv/Scripts/python -m pip install -r requirements.txt -e .
```

Put the data files in `data/raw/` or set your Kaggle API token. Then run:

```bash
python -m aml.cli data     # load and prepare the data
python -m aml.cli features  # build features
python -m aml.cli detect    # run detectors
python -m aml.cli train     # train the model
python -m aml.cli app       # start the dashboard
```

## How It Works

The raw transaction data is loaded and converted to a common currency (USD). Then the system builds a graph of who sent money to whom. It looks for suspicious patterns like cycles, fan-in/fan-out structures, and pass-through accounts. Features are extracted and fed into both unsupervised anomaly detection and a supervised LightGBM model. All scores land in the dashboard.

## License

MIT
