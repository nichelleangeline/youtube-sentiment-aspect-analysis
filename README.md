# YouTube Sentiment & Aspect Analysis

This repository contains the implementation of a sentiment and aspect analysis pipeline applied to YouTube comments as part of an academic project.

The case study analyzes public reactions to the topic **“Jokowi Ditunjuk sebagai Dewan Penasihat Global Bloomberg New Economy”** using Natural Language Processing (NLP) techniques.

---

## 📌 Project Overview

The objective of this project is to understand public opinion and discussion patterns on YouTube by combining:
- Sentiment analysis (negative, neutral, positive)
- Aspect extraction and topic modeling
- Aspect-based sentiment analysis

The analysis is designed to capture not only overall sentiment, but also *which aspects* are being discussed and *how people feel about each aspect*.

---

## 📊 Data Collection

- **Source**: YouTube comments  
- **Method**: YouTube Data API  
- **Scope**:
  - 9 relevant YouTube videos
  - Top-level comments only (no replies)
- **Initial target**: ~3,000 comments  
- **Collected**: 1,898 unique comments  
- **Final dataset after preprocessing**: 1,842 comments  

**Stored fields**:
- Video ID  
- Comment ID  
- Username  
- Comment text  
- Like count  
- Publication time  

Raw data is not included in this repository for ethical and privacy reasons.

---

## 🧹 Preprocessing Pipeline

Preprocessing was designed with two parallel text representations:

### 1️⃣ Sentiment Text
- Basic cleaning (duplicates, empty comments)
- Normalization of repeated words (e.g., *HOAXXXXX → hoax*)
- Slang normalization
- Emoji, URL, mention removal
- Stopwords **not aggressively removed** to preserve sentiment context

### 2️⃣ Aspect Text
- Additional stopword removal
- Focus on entities, topics, and issues
- Designed for topic modeling and aspect extraction

Short comments (< 4 characters) were removed to reduce noise.

---

## 📈 Exploratory Data Analysis (EDA)

EDA was conducted to validate data quality and relevance:
- Token distribution (unigram, bigram, trigram)
- Comment length distribution (before vs after preprocessing)
- Comparison between sentiment and aspect representations

Results show that dominant tokens and n-grams strongly align with the research topic, confirming dataset relevance.

---

## 😊 Sentiment Analysis

### Lexicon-Based Labeling (Lexicon++)
A customized lexicon-based approach was used to generate weak labels:
- Expanded Indonesian sentiment lexicon
- Domain-specific terms (e.g., *hoax, palsu, bangga*)
- Handling of negation and intensifiers

Sentiment classes:
- Negative
- Neutral
- Positive

---

## 🤖 Supervised Sentiment Models

The following models were trained and evaluated:

- **BiLSTM**
- **TF-IDF (unigram + bigram) + LinearSVC**
- **Ensemble (Calibrated SVM + BiLSTM, soft voting)**

**Best performance** was achieved by the ensemble model:
- Accuracy ≈ 0.64  
- Macro F1-score ≈ 0.63  

The neutral class was the most challenging due to its ambiguous nature.

---

## 🧩 Aspect Analysis

### Unsupervised Topic Modeling
- **Method**: Non-negative Matrix Factorization (NMF)
- **Features**: TF-IDF (unigram + bigram)
- **Number of topics**: 8

The topics capture:
- Core news discussion
- Political comparisons
- Economic and national context
- Supportive and controversial narratives

### Supervised Multi-label Aspect Classification
- TF-IDF + One-vs-Rest Logistic Regression
- Weak supervision using seed keywords
- High performance (Micro F1 ≈ 0.93)

---

## 🔍 Aspect-Based Sentiment Analysis

Sentiment distribution was analyzed per aspect to reveal indications of:
- Public support
- Polarization
- Controversial issues
- Topic-dependent sentiment patterns

This approach provides deeper insight compared to global sentiment analysis alone.

---

## 🛠️ Tools & Technologies

- **Programming Language**: Python  
- **NLP & ML**:
  - Scikit-learn
  - TensorFlow / Keras (BiLSTM)
- **Text Representation**:
  - TF-IDF (unigram & bigram)
- **Topic Modeling**:
  - NMF
- **Data Handling**:
  - Pandas, NumPy
- **Development Environment**:
  - Google Colab
