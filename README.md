# Real-Time Crypto Price Prediction System

## Overview
This project aims to build a real-time machine learning system that predicts cryptocurrency prices 5 minutes into the future. The system is built using Python, Rust, large language models (LLMs), and Kubernetes.

## System Architecture
The system is divided into several components:

1. **Feature Pipelines**
   - **Technical Indicators**: Ingests market trades from a websocket API, aggregates them into 1-minute windows, and engineers technical indicators.
   - **Market Sentiment**: Scrapes news, parses sentiment scores using an LLM, and stores them.

2. **Training Pipeline**
   - Uses XGBoost to train a model on current technical indicators and market sentiment to predict future prices.

3. **Inference Pipeline**
   - **Prediction Generator**: Loads the model and generates predictions using the latest features.
   - **Prediction API**: Serves predictions to client applications.

4. **Monitoring Pipeline**
   - Monitors prediction errors by comparing real-time prices with predictions.

## Step-by-Step Guide to Building the Real-Time ML System

### Our Goal 🎯

Build an ML system that predicts crypto prices 5 minutes into the future using:
- Real-time market prices
- Real-time market news impacting blockchain or economic factors

### System Design 📐

The system is divided into four pipelines:

1️⃣ **Feature Pipelines**

- **Technical Indicators Pipeline**
  - Ingests market trades from a websocket API like Kraken Digital Asset Exchange.
  - Aggregates trades into 1-minute windows.
  - Engineers technical indicators to capture market momentum.
  - Pushes indicators to the Feature Store.

- **Market Sentiment Pipeline**
  - Scrapes news from websites like Coinbase.
  - Parses text into structured sentiment scores using an LLM.
  - Pushes scores to the Feature Store.

2️⃣ **Training Pipeline**

- Uses a boosting tree model like XGBoost to find patterns between:
  - Current technical indicators
  - Market sentiment
  - Future prices of BTC or ETH
- The final model is pushed to the model registry.

3️⃣ **Inference Pipeline**

- **Prediction Generator**
  - Loads the model from the registry.
  - Uses the latest features to generate predictions.
  - Pushes predictions to persistent storage like an Elasticsearch index.

- **Prediction API**
  - Receives requests from client apps.
  - Retrieves predictions from Elasticsearch.
  - Returns predictions to clients.

4️⃣ **Monitoring Pipeline**

- Monitors prediction errors by:
  - Listening to incoming price data.
  - Loading predictions from the database.
  - Computing errors.
  - Pushing errors into another Elasticsearch index.

## Deployment
The system is containerized using Docker and deployed on Kubernetes. Each component has its own Docker image and Kubernetes deployment.

## Getting Started

### Prerequisites
- Docker
- Kubernetes
- Python 3.9

### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/2series/crypto-price-prediction.git
   cd crypto-price-prediction
   ```

2. Build Docker images for each service:
   ```bash
   docker build -t technical-indicators:latest .
   docker build -t market-sentiment:latest .
   docker build -t train-model:latest .
   docker build -t prediction-generator:latest .
   docker build -t prediction-api:latest .
   docker build -t monitoring-service:latest .
   ```

3. Deploy to Kubernetes:
   ```bash
   kubectl apply -f k8s_deployment/
   ```

## Usage
- Access the prediction API to get real-time predictions.
- Monitor the system using the monitoring pipeline.

## Contributing
Contributions are welcome! Please fork the repository and submit a pull request.

## License
This project is licensed under the MIT License.
