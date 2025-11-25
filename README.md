# 🎬 Movie Recommendation System

A content-based movie recommendation system that suggests movies similar to a user's selection. The application uses **Streamlit** for the interactive web interface and fetches real-time movie posters and plot summaries using the **OMDB API**.

## 🚀 Features

  * **Content-Based Filtering:** Suggests movies based on genres, keywords, and overviews using TF-IDF and Cosine Similarity.
  * **Interactive UI:** User-friendly interface built with Streamlit.
  * **Rich Movie Details:** Displays movie posters and plot summaries dynamically fetched from the OMDB API.
  * **Logging:** Tracks preprocessing and recommendation events in the `logs/` directory.

## 📂 Project Structure

  * **`main.py`**: The main Streamlit application file.
  * **`preprocess.py`**: Script to clean data, vectorize text, and generate similarity models.
  * **`recommend.py`**: Contains the logic to load models and generate recommendations.
  * **`omdb_utils.py`**: Helper functions to interact with the OMDB API.
  * **`config.json`**: Configuration file for storing API keys.
  * **`movies.csv`**: The raw dataset (required in the root directory).
  * **`models/`**: Directory where processed data (`.pkl` files) is saved.
  * **`logs/`**: Directory where application logs are stored.

## 🛠️ Installation & Setup

### 1\. Prerequisites

Ensure you have Python installed. You will also need an API key from [OMDB](http://www.omdbapi.com/).

### 2\. Install Dependencies

Create a `requirements.txt` file (if not already present) with the following libraries, then install them:

```bash
pip install -r requirements.txt
```

*Suggested `requirements.txt`:*

```text
streamlit
pandas
scikit-learn
nltk
requests
joblib
```

### 3\. Configuration

Open `config.json` and replace the placeholder with your actual OMDB API key:

```json
{
  "OMDB_API_KEY": "your_actual_api_key_here"
}
```

## 🏃‍♂️ Usage

Follow these steps to run the application:

### Step 1: Preprocess the Data

Before running the app for the first time, you must generate the similarity models. This script creates the `models/` directory and saves `df_cleaned.pkl`, `tfidf_matrix.pkl`, and `cosine_sim.pkl`.

```bash
python preprocess.py
```

### Step 2: Run the App

Start the Streamlit server:

```bash
streamlit run main.py
```

## 🧠 How It Works

1.  **Preprocessing**: The `preprocess.py` script combines the 'genres', 'keywords', and 'overview' columns from `movies.csv`. It cleans the text (removing stopwords and non-alphabetic characters).
2.  **Vectorization**: It uses `TfidfVectorizer` (limited to 5000 features) to convert the text data into numerical vectors.
3.  **Similarity Calculation**: It calculates the Cosine Similarity between all movie vectors to determine which movies are most alike.
4.  **Recommendation**: When a movie is selected in the app, `recommend.py` looks up the top 5 movies with the highest similarity scores.

## 📝 Logging

Check the `logs/` folder for `preprocess.log` and `recommend.log` to troubleshoot issues or monitor application flow.
