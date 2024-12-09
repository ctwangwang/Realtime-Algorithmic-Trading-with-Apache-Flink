# Flink Algorithmic Trading System

This project implements an algorithmic trading system using Apache Flink, Kafka, and the Alpaca trading API. It processes market news and generates trading signals based on sentiment analysis.

## Components

1. **News Producer** (`news-producer.py`): Fetches historical news data from Alpaca API and publishes it to a Kafka topic.
2. **Signal Handler** (`signal_handler.py`): Consumes trading signals from Kafka, processes them, and executes trades using the Alpaca API.

## Setup

1. Create and activate a virtual environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
2. Install the required python libraries:
   ```bash
   pip install alpaca_trade_api kafka-python requests pandas
   pip install alpaca-py
   pip install nltk
   pip install pyflink apache-flink
   python -c "import nltk; nltk.download('vader_lexicon')"
   pip install backtrader
   pip install matplotlib

3. Configure Alpaca API credentials and other settings in `alpaca_config/keys.py`.

4. Download the Flink Kafka connector JAR and place it in the `libs/` directory:
- `flink-sql-connector-kafka-3.1.0-1.18.jar`

## Usage

1. Build up Docker environment:
   ```bash
   docker compose up -d --build

2. Produce news and prices stream to RedPanda(Kafka)
   ```bash
   python news-producer.py
   python prices-producer.py

3. Run Flink SQL Client
   ```bash
   docker compose run sql-client
   (copy ddl.sql and run it on terminal to create tables and views)

4. Create Slack channel and app
   (copy channel ID and token to keys.py)

5. Run signal_handler.py to send trade signal to Slack channel
   ```bash
   python signal_handler.py
   
## Features

- Historical news data ingestion
- Real-time signal processing with Apache Flink
- Sentiment analysis on news headlines
- Integration with Alpaca trading API for order execution
- Slack notifications for trading signals
- Time window-based signal filtering to avoid acting on outdated information
- Backtesting mode for historical data analysis

## Notes

- Ensure proper error handling and logging in a production environment.
- Thoroughly test the system in a simulated environment before using it with real funds.
- Regularly update dependencies and API integrations to maintain system security and functionality.


