# Spotify Recommendation System

## Project Overview

This project implements a Spotify-style music recommendation system using audio features, along with data analysis and machine learning techniques.

The main objective is to recommend songs that are musically similar to a given input track by combining:

- audio feature similarity
- genre similarity
- artist similarity

In addition, the project includes:
- SQL-based analytics
- Exploratory Data Analysis (EDA)
- Unsupervised learning using KMeans clustering
- Evaluation of recommendation quality

---

## Dataset

The dataset used in this project is the **Spotify Tracks Genre** dataset from Kaggle:

https://www.kaggle.com/datasets/thedevastator/spotify-tracks-genre-dataset

The dataset contains Spotify track information such as:
- `track_id`
- `artists`
- `album_name`
- `track_name`
- `popularity`
- `duration_ms`
- `explicit`
- `danceability`
- `energy`
- `loudness`
- `mode`
- `speechiness`
- `acousticness`
- `instrumentalness`
- `liveness`
- `valence`
- `tempo`
- `time_signature`
- `track_genre`

For this project, a cleaned sample of **5000 songs** was used.

---

## Recommendation System

A hybrid recommendation system was implemented combining:

- **Cosine similarity** on scaled audio features
- **Genre similarity**
- **Artist similarity**

---

### Feature Processing

- Features were standardized using `StandardScaler`
- Dimensionality reduction was applied using **PCA**

PCA Details:
- Number of components: 5  
- Total explained variance: ~75.5%

This helps reduce noise and improves similarity computation.

---

### Scoring Mechanism

The final recommendation score is computed as:

`final_score = 0.7 * audio_similarity + 0.2 * genre_score + 0.1 * artist_score`

Where:

- **Audio similarity**: cosine similarity between songs
- **Genre score**:
  - 1.0 if genres match
  - 0.2 otherwise
- **Artist score**:
  - 1.0 if same artist appears
  - 0.3 otherwise

This hybrid approach improves recommendation quality by combining musical and contextual similarity.

---

## Recommendation Evaluation

The recommender system was evaluated using **Precision@K (k=10)**.

### Results:

- Mean Precision@10: **0.652**
- Standard Deviation: **0.357**

This indicates that, on average, **65.2% of recommended songs share the same genre as the input song**.

This suggests that the recommender is able to capture meaningful musical similarity based on genre consistency.

A distribution analysis shows variability depending on the input track, which is expected in real-world recommendation systems.

---


## SQL Analytics

SQLite was used to perform analytical queries on the dataset.

Example insights:

- Genres with the highest average popularity
- Genres with highest energy
- Highly danceable and popular songs
- Artists with the most unique tracks
- Genres above average popularity

---

## Exploratory Data Analysis (EDA)

EDA was performed to understand feature distributions and relationships using:

- Popularity distribution histogram
- Correlation heatmap of audio features
- Scatter plot (danceability vs energy)
- Feature comparison between input and recommended songs

---

### Key Observations:

- Popularity is skewed, with fewer highly popular songs
- Danceability and valence show a moderate positive correlation
- Energy and acousticness show a strong negative correlation

These findings align with real-world musical characteristics.

---

## Unsupervised Learning

KMeans clustering was applied to group songs based on audio features.

### Model Selection:

- Elbow Method
- Silhouette Score

Both methods indicated:

- Optimal number of clusters: **k = 2**

### Interpretation:

- Cluster 1: higher energy and danceability
- Cluster 2: higher acousticness and lower energy

PCA visualization confirms clear separation between clusters.

---

## Technologies Used

- Python
- Pandas
- NumPy
- Scikit-learn
- Matplotlib
- Seaborn
- SQLite

---

## Files

- `analysis.ipynb` → main notebook  
- `spotify_project.db` → SQLite database  

---

## Notes

The full dataset is not included in this repository due to its size.  
Please download it from Kaggle and place it in the project directory if needed.

---

## Limitations

- The evaluation is based on genre similarity as a proxy for relevance, since user interaction data is not available.
- The system does not incorporate collaborative filtering or user preferences.

---
