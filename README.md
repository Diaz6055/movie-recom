# 🎬 Movie Recommender

A full-stack movie recommendation system powered by **TF-IDF content-based filtering** and the **TMDB API**, with a FastAPI backend and Streamlit frontend.

---

## 📸 Preview

> Search for any movie → get instant suggestions → explore similar movies via TF-IDF and genre-based recommendations.

---

## 🧠 How It Works

The system uses two recommendation strategies:

| Strategy | Description |
|---|---|
| **TF-IDF (Content-Based)** | Computes cosine similarity between movies using a pre-trained TF-IDF matrix on movie metadata |
| **Genre-Based (TMDB)** | Fetches popular movies in the same genre from the TMDB Discover API |

---

## 🗂️ Project Structure

```
movie-rec/
├── main.py              # FastAPI backend
├── app.py               # Streamlit frontend
├── df.pkl               # Movie DataFrame (pre-processed)
├── indices.pkl          # Title → index mapping
├── tfidf_matrix.pkl     # Pre-computed TF-IDF sparse matrix
├── tfidf.pkl            # Fitted TF-IDF vectorizer
├── .env                 # Environment variables (TMDB API key)
└── requirements.txt
```

---

## ⚙️ Setup & Installation

### 1. Clone the repository

```bash
git clone https://github.com/your-username/movie-rec.git
cd movie-rec
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Add your TMDB API key

Create a `.env` file in the root directory:

```
TMDB_API_KEY=your_api_key_here
```

Get a free API key at [https://www.themoviedb.org/settings/api](https://www.themoviedb.org/settings/api).

### 4. Add the pre-trained model files

Place the following pickle files in the root directory:

- `df.pkl` — DataFrame with a `title` column
- `indices.pkl` — Dict or pandas Series mapping titles to DataFrame indices
- `tfidf_matrix.pkl` — Scipy sparse TF-IDF matrix
- `tfidf.pkl` — Fitted `TfidfVectorizer`

---

## 🚀 Running the App

### Start the FastAPI backend

```bash
uvicorn main:app --reload --port 8000
```

API docs available at: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

### Start the Streamlit frontend

```bash
streamlit run app.py
```

Frontend available at: [http://localhost:8501](http://localhost:8501)

---

## 🔌 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/health` | Health check |
| `GET` | `/home` | Trending / popular / top-rated movies |
| `GET` | `/tmdb/search` | Search TMDB for movies by keyword |
| `GET` | `/movie/id/{tmdb_id}` | Full details for a movie |
| `GET` | `/recommend/tfidf` | TF-IDF recommendations by title |
| `GET` | `/recommend/genre` | Genre-based recommendations by TMDB ID |
| `GET` | `/movie/search` | Combined bundle: details + TF-IDF + genre recs |

### Example

```bash
# Get recommendations for "Inception"
curl "http://localhost:8000/movie/search?query=Inception&tfidf_top_n=10&genre_limit=10"
```

---

## 🌐 Deployment

The backend is deployed on **Render**:

```
https://movie-rec-466x.onrender.com
```

To point the Streamlit app at a different backend, update `API_BASE` in `app.py`:

```python
API_BASE = "https://your-backend-url.onrender.com"
```

---

## 📦 Requirements

```
fastapi
uvicorn
httpx
pandas
numpy
scikit-learn
python-dotenv
pydantic
streamlit
requests
scipy
```

---

## 🛠️ Tech Stack

- **Backend:** FastAPI, Python, Scipy, NumPy, Pandas
- **Frontend:** Streamlit
- **Recommendations:** TF-IDF cosine similarity (scikit-learn)
- **Movie Data:** [TMDB API](https://www.themoviedb.org/documentation/api)
- **Deployment:** Render (backend)

---

## 📄 License

MIT License. Feel free to use, modify, and distribute.

---

> Built with ❤️ using FastAPI + Streamlit + TMDB
