# Ethiopian Bank Mobile App Reviews Analysis

A data-driven fintech consulting simulation project evaluating customer feedback on Ethiopian banks' mobile applications. The analysis includes data scraping, sentiment analysis, thematic NLP, and structured database storage using Oracle DB, culminating in visual insights and strategic recommendations.

## 📁 Project Structure

ethiopian-bank-review-analysis/
│
├── data/
│   ├── raw/                      # Raw scraped reviews
│   └── clean/                    # Cleaned review CSV files
│
├── outputs/                      # Generated plots and reports
│
├── src/
│   ├── scraper.py                # Google Play review scraper
│   ├── sentiment_analysis.py     # Sentiment scoring and labeling
│   ├── db_load.py                # Oracle DB loader using cx_Oracle
│   └── visualize.py              # Data visualization scripts
│
├── requirements.txt              # Python dependencies
├── README.md                    # Project documentation (this file)
└── .gitignore                   # Git ignore rules

## 🚀 Tasks Overview

### ✅ Task 1 – Scraping
- Scraped 500–1000 reviews per bank (CBE, BOA, Dashen) from Google Play.
- Saved data in `data/raw/`.

### ✅ Task 2 – NLP Processing
- Cleaned text, removed stopwords.
- Applied Vader for sentiment scoring.
- Labeled reviews as Positive, Neutral, or Negative.
- Visualized sentiment distribution with `matplotlib` and `seaborn`.

### ✅ Task 3 – Oracle DB
- Defined schema in `schema.sql`:
  - `banks(id, name)`
  - `reviews(id, bank_id, review_text, rating, review_date, sentiment_label, sentiment_score)`
- Loaded processed data using `cx_Oracle`.

### ✅ Task 4 – Insight & Reporting
- Generated visual insights on:
  - Sentiment by bank
  - Review trends over time
  - Common complaint themes
- Saved plots to `outputs/`.

## 🛠️ Technologies Used

- **Languages**: Python, SQL
- **Libraries**: pandas, seaborn, matplotlib, nltk, VaderSentiment, cx_Oracle
- **Database**: Oracle XE
- **Environment**: VS Code, Jupyter

## 🧠 Insights

- Dashen Bank had the highest proportion of negative reviews.
- Users frequently complained about login failures and UI issues.
- Positive sentiment was associated with recent updates and speed improvements.

## 💡 Recommendations

- **CBE**: Improve session stability and reduce crashes.
- **BOA**: Address UI lag and bugs on Android 11+.
- **Dashen**: Focus on onboarding issues and payment feature clarity.

## 📦 Setup Instructions

```bash
# Clone repository
git clone https://github.com/<your-username>/ethiopian-bank-reviews.git
cd ethiopian-bank-reviews

# Create virtual environment
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows

# Install dependencies
pip install -r requirements.txt

# Run scraper
python src/scraper.py

# Run NLP processing
python src/nlp_analysis.py

# Load to Oracle DB (Oracle XE must be running)
python src/db_load.py
