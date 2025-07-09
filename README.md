# 🎬 Netflix Recommendation System

This project is a **Content-Based Recommendation System** that suggests movies/shows based on user preferences. It uses metadata such as **title**, **description**, **genres**, **cast** and **director** to recommend similar movies using Natural Language Processing techniques.

## 📁 Project Structure

- `Recommendation System.ipynb` — Jupyter Notebook containing the full implementation.
- `netflix_titles.csv` — Dataset containing metadata about netflix movies/shows, collected from Kaggle.

## 💡 How It Works

The system uses the following steps:
1. **Data Preprocessing**:
   - Merging relevant features into a single "tags" column.
   - Cleaning text (lowercasing, removing punctuation and stop words, stemming).
   
2. **Feature Extraction**:
   - Vectorizing the cleaned text using `CountVectorizer`.
  
3. **Label Generation**
   - Applies **KMeans clustering** to group movies with similar characteristics
   - Leverages **Google Gemini** to auto-generate descriptive genres from top keywords in each cluster

3. **Similarity Calculation**:
   - Cosine similarity is used to find the most similar content based on tag vectors.

4. **Recommendation Function**:
   - Given a title, the function returns the top N most similar content.

## Technologies Used

### Core Libraries
- `pandas` — For data loading and manipulation
- `numpy` — Numerical computations
- `sklearn`
  - `CountVectorizer` — Converts cleaned movie metadata into a bag-of-words model
  - `cosine_similarity` — Computes similarity between movie vectors
  - `KMeans` — Clusters movies into thematic groups
- `nltk`
  - `stopwords` — For removing common stop words
  - `PorterStemmer` — For stemming tokens
 
### External Tools
- **Gemini by Google (LLM)** — Used to generate meaningful, human-readable genre labels for each cluster based on most frequent keywords.

## 🔍 Clustering & Genre Enrichment

To enhance content recommendations:
1. **KMeans** clusters were created using vectorized tag data.
2. For each cluster, top tokens were extracted using the cluster centroid weights.
3. These tokens were passed into **Google Gemini** to summarize each cluster with a **genre-like label**, e.g.:
   - Cluster 0 → "Thriller"
   - Cluster 1 → "Drama"
4. These enriched genres improve filtering, labeling, and user experience.

## 📊 Sample Output

```python
get_similar_movies("The Haunting of Bly Manor")
