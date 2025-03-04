# 🎵 Natural Language Processing for Music Recommendation: A Word2Vec Approach

![presentationSlide](presentation/presentationSlide.png)

## Overview
This repository contains a **Word2Vec-based recommender system** that applies **Natural Language Processing (NLP) exclusively to textual data** in the dataset.  
The model learns relationships **only from strings of natural language**, specifically using the following **four textual features**:
- **User ID** (as a reference, not used in NLP processing)
- **Track Name** (song titles in natural language)
- **Artist Name** (artist names as text-based entities)
- **Playlist Name** (curated user-generated textual metadata)

By leveraging **crowdsourced user playlist data**, the system learns artist relationships and recommends **top 10 songs** that are most similar to the user's artist-based preference.


### 🔥 Future Work:
A **hybrid recommender system** is planned, which will refine recommendations further by:
- Expanding beyond artist relations.
- Using **track-based** cosine similarity instead of artist similarity alone.
- Improving the overall diversity and personalization of song recommendations.

---

## 📌 Objective
1. **User Input**: The user provides an artist and track preference in the form of `"artistname:trackname"`.
2. **Recognizing Artist Preference**: The model identifies that the user likes a particular artist.
3. **Recommendation Generation**:  
   - The **Word2Vec model** trained on massive user playlists predicts the **top 10 songs** (with high cosine similarity) related to the user's artist preference.
   - These recommendations reflect **collective music taste trends** (חוכמת ההמונים - "wisdom of the crowd").
4. **Future Expansion**:  
   - Improve recommendations by analyzing track-based relationships in addition to artist-based similarities.

---

## 📊 Dataset Information
- **Source**: Open dataset from [Kaggle](https://www.kaggle.com/datasets/andrewmvd/spotify-playlists/data?select=spotify_dataset.csv).  
- **Original Data**:  
  - 12+ million rows  
  - 4 string-based columns: User ID, Track Name, Artist Name, Playlist Name  
- **Cleaning & Processing**:  
  - Removed missing values (~33,572 missing artists, 88 missing track names, 1,246 missing playlist names).  
  - Standardized text (lowercasing, trimming spaces, removing duplicates).  
  - Filtered out playlists with extreme bias (e.g., "starred" playlist contained **over 1.3 million songs**).  
  - Kept ~10 million cleaned rows for training.  

---

## ⚙️ Model Training: Word2Vec
- **Approach**: Skip-gram architecture to learn artist and track relationships.  
- **Key Parameters**:  
  - `vector_size`: **100** (dimension of word embeddings)  
  - `window`: **5** (context size)  
  - `min_count`: **10** (ignore words with low occurrences)  
  - `sg`: **1** (skip-gram model used)  
- **Training Strategy**:  
  - Input: `"artistname:trackname"` tokens.  
  - Output: Vectorized song embeddings that capture similarity relationships.

### 🛠 Data Split  
- The dataset was **split 80-20**:
  - **80% of tokens** were used for training the Word2Vec model.  
  - **20% were held out** to evaluate embeddings.  
- **Validation Strategy**:
  - Instead of randomly validating all tokens, validation was conducted on a **subset of 1,000 users** from the ground truth dataset.  
  - This approach ensures that evaluation reflects **real user preferences** rather than random token similarities.  

---

## 🎯 How to Use
1. **Clone the Repository**  
   ```
   git clone https://github.com/your-username/spotify-word2vec-recommender.git
   cd spotify-word2vec-recommender
   ```

2. **Install Dependencies**
```
pip install -r requirements.txt
```

3. **Run Jupyter Notebook**
```
jupyter notebook
```

4. **Get Recommendations**
- Open the notebook and input an "artistname:trackname".
- The model will return the top 10 recommended songs based on artist similarity.
- Example Usage:

  ![exampleUsage](presentation/exampleUsage.png)

---

## 🔍 Results & Next Steps

**Current Outcome:**  
- The model **successfully recommends songs** based on user preferences.  
- It relies on **artist similarity**, meaning recommendations focus on songs by the same or similar artists.
- **Fuzzy Matching (Threshold: 60)**:  
  - Used to **prevent mismatches in the trackname part** of the concatenated string (`"artistname:trackname"`).  
  - Ensures that **Word2Vec learns artist-based relationships first**, without being influenced by trackname variations.  
  - Helps avoid incorrect associations where the model could mistakenly link tracks instead of artists at this stage.
  - Fuzzy threshold was chosen carefully:
    
 ![fuzzyElbow](presentation/fuzzyElbow.png)
    

**Future Development:**  
- Implement a **hybrid recommender system**:
  - **Step 1: Artist-based filtering (current approach)**  
    - Uses **Word2Vec embeddings** and **fuzzy matching (threshold: 60)** to refine **artist identification**.  
    - Generates **top 10 track recommendations** related to the identified artist.  
  - **Step 2: Track-based cosine similarity**
    - Expanding recommendations beyond artist similarity by incorporating **song-to-song relationships**.
   
---

## 📜 License
This project is licensed under the **[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0)** – free to use and modify under permitted terms.  
For more details, see the [`LICENSE`](LICENSE) file in this repository.

---

## 🔗 References
- **Word2Vec Research Paper**: [Efficient Estimation of Word Representations in Vector Space](https://arxiv.org/abs/1301.3781)  
- **Gensim Word2Vec Documentation**: [Gensim Official Docs](https://radimrehurek.com/gensim/models/word2vec.html)  
- **Spotify Playlists Dataset**: [Kaggle Dataset](https://www.kaggle.com/datasets/andrewmvd/spotify-playlists/data?select=spotify_dataset.csv)  

---

## 📢 Data Disclaimer
This project is for **educational and research purposes only**.  
The dataset used in this repository was obtained from **[Kaggle](https://www.kaggle.com/datasets/andrewmvd/spotify-playlists/data?select=spotify_dataset.csv)** and contains publicly available playlist data.  

**All rights to the original data belong to Spotify.**  
This repository does **not** distribute, modify, or claim ownership over any Spotify content.

---

## 🎧 **Have a favorite artist? Let’s see if AI can guess your next jam!** 🎶  

