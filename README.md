Ethiopian Bank Mobile App Review Analysis

Project Overview

This project analyzes user reviews from the mobile applications of three major Ethiopian banks—Commercial Bank of Ethiopia (CBE), Dashen Bank, and Bank of Abyssinia (BOA)—to derive insights into customer satisfaction and identify areas for improvement. Conducted as part of a fintech consulting engagement with Omega Consultancy, the project aims to enhance mobile banking experiences by providing actionable recommendations based on user feedback. The analysis pipeline includes:





Data Scraping: Collecting reviews from the Google Play Store using google-play-scraper.



Data Preprocessing: Cleaning and normalizing review data (e.g., removing duplicates, formatting dates).



Sentiment Analysis: Applying NLP techniques with DistilBERT to classify sentiments (positive, negative, neutral) and compute sentiment scores.



Thematic Analysis: Extracting keywords and clustering them into themes (e.g., UI, reliability) using TF-IDF and regex-based clustering.



Database Integration: Storing structured data in a PostgreSQL database (fallback from Oracle XE due to setup constraints).



Visualization: Generating charts to visualize sentiment distributions, rating trends, and thematic insights using Matplotlib and Seaborn.

The deliverables support strategic goals such as user retention, feature enhancement, and complaint management, aligning with fintech priorities for improving customer satisfaction.

Features





Scrapes 400+ reviews per bank (1200+ total) from the Google Play Store.



Preprocesses raw data to remove duplicates, handle missing values, and normalize dates to YYYY-MM-DD.



Performs sentiment analysis using DistilBERT (distilbert-base-uncased-finetuned-sst-2-english).



Extracts keywords with TF-IDF and clusters them into 3–5 themes per bank (e.g., Account Access Issues, Transaction Performance).



Stores cleaned data and analysis results in a normalized PostgreSQL database schema.



Generates visualizations, including rating distributions, sentiment trends, and keyword clouds.



Modular Python scripts for scraping, preprocessing, analysis, database loading, and visualization.



Version-controlled with Git, using branches (task-1, task-2, etc.) and meaningful commit messages.

Repository Structure

ethiopian-bank-review-analysis/
├── data/
│   ├── raw/                      # Raw scraped reviews (e.g., ethiopian_bank_reviews.csv)
│   └── processed/                # Cleaned and analyzed data (e.g., ethiopian_reviews_analyzed.csv)
├── outputs/                      # Generated plots and reports (e.g., rating_distribution.png)
├── scripts/
│   ├── scrape.py                 # Google Play review scraper
│   ├── analyze_nlp.py            # Sentiment and thematic analysis
│   ├── store_db.py               # PostgreSQL database loader
│   └── visualize.py              # Data visualization scripts
├── notebooks/                    # Jupyter notebooks for exploration (e.g., scrape.ipynb)
├── sql/
│   └── schema.sql                # Database schema and setup scripts
├── .gitignore                    # Git ignore rules
├── requirements.txt              # Python dependencies
└── README.md                     # Project documentation (this file)

Setup & Installation

Prerequisites





Python 3.8+



PostgreSQL (or Oracle XE if available) installed locally or via Docker



Git



Optional: Jupyter for running notebooks

Install Python Dependencies

pip install -r requirements.txt

Required packages include:

pandas
numpy
google-play-scraper
transformers
torch
scikit-learn
spacy
psycopg2-binary
matplotlib
seaborn
wordcloud
jupyter  # Optional for notebooks

Install spaCy Model

python -m spacy download en_core_web_sm

Database Setup





Install PostgreSQL or run a PostgreSQL Docker container:

docker run -d --name bank_reviews_db -p 5432:5432 -e POSTGRES_PASSWORD=your_password postgres



Create a database named bank_reviews:

psql -U postgres -c "CREATE DATABASE bank_reviews;"



Apply the schema from sql/schema.sql:

CREATE TABLE banks (
    bank_id SERIAL PRIMARY KEY,
    bank_name VARCHAR(100) NOT NULL UNIQUE,
    app_title VARCHAR(200) NOT NULL,
    package_name VARCHAR(100) NOT NULL UNIQUE
);

CREATE TABLE reviews (
    review_id VARCHAR(100) PRIMARY KEY,
    bank_id INTEGER REFERENCES banks(bank_id),
    content TEXT,
    rating INTEGER CHECK (rating BETWEEN 1 AND 5),
    review_date DATE,
    thumbs_up INTEGER DEFAULT 0,
    app_version VARCHAR(50),
    source VARCHAR(50) NOT NULL,
    sentiment_label VARCHAR(20),
    sentiment_score FLOAT,
    themes TEXT,
    keywords TEXT
);

Usage





Scrape Reviews

python scripts/scrape.py





Scrapes reviews for CBE, BOA, and Dashen Bank.



Outputs: data/raw/ethiopian_bank_reviews.csv.



Sentiment and Thematic Analysis

python scripts/analyze_nlp.py





Processes raw reviews for sentiment (DistilBERT) and themes (TF-IDF + regex).



Outputs: data/processed/ethiopian_reviews_analyzed.csv.



Load Data to Database

python scripts/store_db.py





Loads cleaned and analyzed data into PostgreSQL tables (banks, reviews).



Visualize Insights

python scripts/visualize.py





Generates plots (e.g., rating distributions, sentiment trends, keyword clouds).



Outputs: Saved in outputs/ (e.g., rating_distribution.png).

Methodology





Data Collection: Uses google-play-scraper to collect 400+ reviews per bank (1200+ total) from the Google Play Store, targeting English reviews from Ethiopia (lang='en', country='et').



Preprocessing: Removes duplicates by review_id, handles missing data, and normalizes dates to YYYY-MM-DD.



Sentiment Analysis: Applies DistilBERT to classify reviews as positive, negative, or neutral and compute confidence scores.



Thematic Analysis: Extracts 1-2 gram keywords with TF-IDF and clusters into themes (e.g., Account Access Issues, Transaction Performance) using regex patterns.



Database Storage: Stores data in a normalized PostgreSQL schema with banks and reviews tables.



Visualization: Creates 3–5 plots using Matplotlib and Seaborn to highlight sentiment trends, rating distributions, and thematic insights.

Key Deliverables





Task 1: Scraped and preprocessed 1200+ reviews, saved as ethiopian_bank_reviews.csv with <5% missing data.



Task 2: Sentiment scores and 3–5 themes per bank, saved as ethiopian_reviews_analyzed.csv.



Task 3: Populated PostgreSQL database with >1000 review entries.



Task 4: Visualizations and a 7-page final report (due 10 June 2024) with actionable recommendations.

Scenarios Addressed





Retaining Users: Analyzes slow transfer complaints (e.g., 20% of BOA reviews mention delays) to recommend performance optimizations.



Enhancing Features: Identifies feature requests (e.g., fingerprint login in 15% of BOA reviews) to prioritize development.



Managing Complaints: Tracks reliability issues (e.g., login errors in 20% of BOA 1-star reviews) to guide AI chatbot integration.

Ethical Considerations





Bias: Negative reviews may be overrepresented, as dissatisfied users are more likely to post.



Language Limitation: Analysis focuses on English reviews, potentially missing Amharic feedback.



Data Quality: Ensured <5% missing data through preprocessing, but incomplete reviews (e.g., very short texts) may affect analysis.

Git Workflow





Branches: task-1 (scraping), task-2 (NLP analysis), task-3 (database), task-4 (visualizations).



Commits: Frequent with descriptive messages (e.g., "Add sentiment analysis with DistilBERT").



Pull Requests: Merge tasks to main after validation.



Issues: Used for task tracking and collaboration.

