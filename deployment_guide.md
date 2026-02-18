# Deployment Guide for Zepto Sentiment Analysis System

This guide covers deploying the backend to Render and the frontend to Streamlit Cloud.

## 1. Backend Deployment (Render)

Render is a great platform for hosting Python APIs (FastAPI).

1.  **Push your code to GitHub**: Ensure your project is in a GitHub repository.
2.  **Create a New Web Service** on [Render Dashboard](https://dashboard.render.com/).
3.  **Connect your Repository**.
4.  **Configure the Service**:
    *   **Root Directory**: `backend`
    *   **Runtime**: Python 3
    *   **Build Command**: `pip install -r requirements.txt && python -m nltk.downloader stopwords punkt`
    *   **Start Command**: `uvicorn app.main:app --host 0.0.0.0 --port 10000`
5.  **Environment Variables**:
    *   Add any necessary env vars (e.g., `MONGODB_URL` if you are using a cloud DB like MongoDB Atlas).
6.  **Deploy**: Click "Create Web Service". Render will build and deploy your API.
7.  **Copy the URL**: Once deployed, copy the service URL (e.g., `https://zepto-backend.onrender.com`).

## 2. Frontend Deployment (Streamlit Cloud)

Streamlit Cloud is the easiest way to deploy Streamlit apps.

1.  **Push your code to GitHub** (same repo as above).
2.  **Sign in to [Streamlit Cloud](https://share.streamlit.io/)**.
3.  **Deploy an App**:
    *   **Repository**: Select your repo.
    *   **Branch**: `main` (or your branch).
    *   **Main file path**: `frontend/app.py`
4.  **Advanced Settings (Secrets)**:
    *   You need to tell the frontend where the backend is.
    *   In the "Secrets" section of Streamlit Cloud, add:
        ```toml
        BACKEND_URL = "https://zepto-backend.onrender.com"
        ```
    *   *Note*: You will need to update `frontend/app.py` to read this from `st.secrets` or an environment variable if you haven't already.
        *   Update `frontend/app.py`:
            ```python
            import os
            BACKEND_URL = os.getenv("BACKEND_URL", "http://localhost:8000")
            # Or check st.secrets
            if "BACKEND_URL" in st.secrets:
                BACKEND_URL = st.secrets["BACKEND_URL"]
            ```

## 3. Docker Deployment (Any VPS/Cloud)

If you have a VPS (AWS EC2, DigitalOcean, etc.) with Docker installed:

1.  **Clone the repo** on the server.
2.  **Run Docker Compose**:
    ```bash
    docker-compose up -d --build
    ```
3.  **Access**:
    *   Frontend: `http://<server-ip>:8501`
    *   Backend: `http://<server-ip>:8000`

## 4. MongoDB Atlas (Optional)

For a persistent database in production:

1.  Create a free cluster on [MongoDB Atlas](https://www.mongodb.com/atlas).
2.  Get the connection string (e.g., `mongodb+srv://<user>:<password>@cluster0.mongodb.net/...`).
3.  Update your `docker-compose.yml` or Render Environment Variables with `MONGODB_URL`.
