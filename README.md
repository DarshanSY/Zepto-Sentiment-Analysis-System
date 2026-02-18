# Zepto

A complete end-to-end AI system for analyzing customer sentiment from Zepto reviews.

## Features
- **Real-time Analysis**: Analyze single reviews instantly.
- **Batch Processing**: Upload CSV files for bulk analysis.
- **Multilingual Support**: Handles Hinglish and social media text using `twitter-xlm-roberta-base-sentiment`.
- **Insights Dashboard**: Visualizations of sentiment distribution, top complaints, and AI recommendations.
- **Issue Tagging**: Automatically detects issues like "Late Delivery", "Wrong Item", etc.

## Tech Stack
- **Backend**: FastAPI, HuggingFace Transformers, PyTorch
- **Frontend**: Streamlit, Plotly
- **Deployment**: Docker, Docker Compose

## Installation & Running

### Prerequisites
- Docker & Docker Compose (Recommended)
- OR Python 3.9+

### Option 1: Run with Docker (Easiest)
1. Build and start the containers:
   ```bash
   docker-compose up --build
   ```
2. Access the application:
   - **Frontend Dashboard**: [http://localhost:8501](http://localhost:8501)
   - **Backend API Docs**: [http://localhost:8000/docs](http://localhost:8000/docs)

### Option 2: Run Locally
1. **Backend Setup**:
   ```bash
   cd backend
   pip install -r requirements.txt
   uvicorn app.main:app --reload
   ```
2. **Frontend Setup** (in a new terminal):
   ```bash
   cd frontend
   pip install -r requirements.txt
   streamlit run app.py
   ```

## Usage
1. Open the Dashboard at `http://localhost:8501`.
2. Use **Live Analysis** to test individual sentences.
3. Use **Batch Analysis** to upload the provided `sample_reviews.csv` to see bulk processing.
4. Check **Dashboard Insights** for aggregated metrics.

## API Endpoints
- `POST /analyze`: Analyze a single text string.
- `POST /upload_csv`: Upload a CSV file with a `text` column.
- `GET /insights`: Get aggregated stats and recommendations.


