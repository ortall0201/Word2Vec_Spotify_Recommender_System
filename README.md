# 🎵 Artist-Based Recommender System for Spotify using Word2Vec

This repository contains my **final data science course project**, where I developed an **artist-based recommender system** using **Word2Vec**.  
The goal of this project is to train word embeddings that capture relationships between **music artists** based on user-created Spotify playlists.

---

## 🚀 **Project Overview**
- **Objective**: To recommend similar artists based on playlist data using Word2Vec embeddings.  
- **Dataset**: Publicly available **Spotify playlist dataset** from **Kaggle**.  
- **Key Steps**:
  1. **Exploratory Data Analysis (EDA)**: Understanding and preprocessing the dataset.
  2. **Data Cleaning & Normalization**: Removing noise, handling missing values, and standardizing text.
  3. **Word2Vec Model Training**: Learning artist relationships based on co-occurrences in playlists.
  4. **Evaluation & Recommendations**: Using similarity metrics to generate artist recommendations.

---

## 📊 **Dataset Information**
- **Source**: [Kaggle - Spotify Playlist Dataset](https://www.kaggle.com/datasets/andrewmvd/spotify-playlists)  
- **Contents**:
  - **User ID**
  - **Track Name**
  - **Artist Name**
  - **Playlist Name**
- **Size**: Originally **12 million rows**, cleaned down to **~10 million rows** after preprocessing.  
- **Data Cleaning**:
  - Removed missing values: ~33,572 artist names, 88 track names, and 1,246 playlist names were missing.
  - **Standardized text**: Converted to lowercase, removed duplicates, stripped extra spaces.
  - **Removed outliers**: Excluded **"Starred" playlist**, which contained 1.3M tracks and contributed to noise.
  - **Filtered user data**: Eliminated extreme heavy users who skewed the data distribution.

---

## 🔧 **Notebook Workflow**
### **1️⃣ Data Preprocessing**
- Performed **EDA** to examine the dataset distribution.
- Standardized all text fields (lowercase conversion, string cleaning).
- Filtered **short artist names** and **noise words**.
- Dropped missing values (except artists, where "Unknown Artist" was assigned).

### **2️⃣ Training Word2Vec Model**
- **Approach**: **Skip-Gram Word2Vec** to learn artist embeddings.
- **Hyperparameters**:
  - `vector_size=100`
  - `window=5`
  - `min_count=5`
  - `sg=1` (Skip-gram)
- **Training Goal**: Capture the similarity between artists based on playlist co-occurrences.

### **3️⃣ Evaluating Recommendations**
- Used **cosine similarity** to find **the most similar artists** for a given input.
- Example:
  ```python
  model.wv.most_similar
