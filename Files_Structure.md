**The following File_Structure.md, is for testing foundation, but BMC1
decided to go ahead and use Remix IDE for faster deployment, therefore
see the Remix_IDE.md file structure instead for references.*


BMC1-XEdgeV1/

            │
            ├── README.md
            ├── LICENSE
            ├── .gitignore
            ├── config/
            │   ├── config.yaml           #– API keys, timeframes, backtesting parameters
            │   └── tokens.yaml           #– Internal staking, holding thresholds for BMC1 & Trinity simulation.
            │
            ├── data/
            │   ├── raw/                  # Raw market data CSV/JSON – Original API downloads.
            │   └── processed/            # Processed/cleaned data – Cleaned data ready for strategy engine.
            │
            ├── src/
            │   ├── __init__.py
            │   ├── main.py               # Entry point for R&D engine
            │   ├── data_ingestion/       # Pull market data from exchanges. Polygon-ready DEX endpoints. Clean and normalize data.
            │   │   ├── __init__.py
            │   │   ├── cex_api.py        # CEX API data ingestion
            │   │   ├── dex_api.py        # DEX API data ingestion (Polygon compatible)
            │   │   └── data_cleaner.py   # Data cleaning & normalization
            │   │
            │   ├── indicators/           #Compute technical indicators modularly: EMA, ATR, RSI, Stochastic, 
            |   |   |                        # ADX.Each function returns timestamped values for signal engine.
            │   │   ├── __init__.py
            │   │   ├── ema.py
            │   │   ├── atr.py
            │   │   ├── rsi.py
            │   │   ├── stochastic.py
            │   │   └── adx.py
            │   │
            │   ├── strategy/                  # Implement signal logic:
            │   │   ├── __init__.py
            │   │   ├── trend_following.py      #→ EMA crossover + MACD trend confirmation.
            │   │   ├── volatility_breakout.py  #→ ATR / Donchian breakout detection.
            │   │   ├── mean_reversion.py       #→ RSI/Stochastic pullback signals.
            │   │   └── regime_switch.py        #→ Determines if market is trending, ranging, or high-volatility → selects which strategy layer is active.
            │   │
            │   ├── risk/              #Simulate: Position sizing, Max drawdown monitoring, ATR-based risk scaling, No actual trades yet.
            │   │   ├── __init__.py
            │   │   ├── position_sizing.py
            │   │   ├── drawdown_monitor.py
            │   │   └── volatility_risk.py
            │   │
            │   ├── logging_engine/
            │   │   ├── __init__.py
            │   │   ├── signal_logger.py   # Logs all signals with metadata, snapshots, parameters, timestamp, version.
            │   │   └── version_control.py # Tracks versions and parameters, → Ensures reproducibility and traceable changes.
            │   │
            │   └── utils/                # Helpers, math utilities, plotting functions, metrics.
            │       ├── __init__.py
            │       ├── helpers.py
            │       └── math_tools.py
            │
            ├── docs/
            │   ├── architecture.md       # System architecture diagram and description
            │   ├── tokenomics.md         # Internal token utility design, Tokenomics simulations (holding + staking + burn + Trinity)
            │   ├── r&d_manual.md         # Internal R&D workflow & operating rules
            │   └── changelog.md          # Internal version tracking log
            │
            ├── tests/                        # Unit tests for every module: Ensures engine stability internally. Covers future upgrades.
            │   ├── test_data_ingestion.py
            │   ├── test_indicators.py
            │   ├── test_strategy.py
            │   ├── test_risk.py
            │   └── test_logging.py
            │
            └── notebooks/
                ├── exploratory_data_analysis.ipynb   #Exploratory data analysis
                ├── strategy_backtesting.ipynb        #Backtesting strategies
                └── risk_simulations.ipynb            #Risk simulation visualizations, Internal experimentation
