 
# Reddit Sentiment Analysis with PostgreSQL

This project is focused on performing sentiment analysis on Reddit posts using the Reddit API (`praw`) and analyzing the sentiment using `TextBlob`. The results are stored in a PostgreSQL database for further analysis and visualization.

## Project Overview

1. **Reddit Sentiment Analysis**:
   - Fetches the latest Reddit posts from the specified subreddit using the Reddit API.
   - Analyzes the sentiment of each post using `TextBlob`.
   - Inserts the post text along with its sentiment score into a PostgreSQL database.

2. **PostgreSQL Database**:
   - A PostgreSQL database (`sentiment_analysis`) is created to store the Reddit posts along with their sentiment scores.
   - The `tweets` table has been created with the following columns:
     - `id` (Primary Key)
     - `tweet_text` (Text of the Reddit post)
     - `sentiment_score` (Sentiment polarity score)
     - `created_at` (Timestamp of when the post was fetched)

3. **Sentiment Analysis**:
   - Sentiment analysis is done using `TextBlob`, which provides the polarity of the text. The polarity score ranges from `-1` (negative) to `1` (positive), with `0` indicating neutral sentiment.

## Steps Taken

### 1. **Setup Reddit API**:
   - Created a Reddit application via [Reddit's Developer Portal](https://www.reddit.com/prefs/apps).
   - Used the credentials (`client_id`, `client_secret`, `user_agent`) to authenticate and interact with the Reddit API using the `praw` library.

### 2. **Setup PostgreSQL Database**:
   - A PostgreSQL database called `sentiment_analysis` was created.
   - A table `tweets` was created with columns for `id`, `tweet_text`, `sentiment_score`, and `created_at`.
   - Used the `psycopg2` library to connect and interact with the PostgreSQL database.

### 3. **Fetch Reddit Posts**:
   - Fetched the 10 most recent posts from the subreddit `all` using `praw`.
   - For each post, the `title` of the post was extracted (text posts could also be used).

### 4. **Sentiment Analysis**:
   - Used `TextBlob` to calculate the sentiment polarity of each Reddit post.
   - The sentiment score is inserted into the `tweets` table along with the text of the post.

### 5. **Store Data in PostgreSQL**:
   - Inserted the Reddit posts and their corresponding sentiment scores into the PostgreSQL database.
   - Ensured that the database connection was closed after the operation was completed.

## Requirements

- **Python 3.x** or above
- **Libraries**:
  - `praw` for accessing Reddit API
  - `textblob` for performing sentiment analysis
  - `psycopg2` for connecting to PostgreSQL
  - `matplotlib` or `plotly` for data visualization (optional)

## Installation

1. Install Python 3.x if not already installed: [Download Python](https://www.python.org/downloads/).

2. Install required Python libraries:
   ```bash
   pip install praw textblob psycopg2 matplotlib plotly
   ```

3. Install PostgreSQL if not already installed: [PostgreSQL Download](https://www.postgresql.org/download/).

4. Create a PostgreSQL database (`sentiment_analysis`) and table (`tweets`):
   ```sql
   CREATE DATABASE sentiment_analysis;
   \c sentiment_analysis
   CREATE TABLE tweets (
       id SERIAL PRIMARY KEY,
       tweet_text TEXT,
       sentiment_score FLOAT,
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   ```

5. Set up your Reddit application and get the following credentials:
   - `client_id`
   - `client_secret`
   - `user_agent`

6. Replace the credentials in the script with your own credentials.

## Usage

1. Run the script to fetch Reddit posts and perform sentiment analysis:
   ```bash
   python reddit_sentiment_analysis.py
   ```

2. The script will fetch the latest 10 posts from the `all` subreddit, analyze their sentiment, and insert them into the PostgreSQL database.

3. (Optional) You can visualize the sentiment distribution by running a script that queries the database and creates a histogram:
   ```bash
   python visualize_sentiment.py
   ```

## Next Steps

1. **Build a Dashboard**: You can create a real-time dashboard using libraries like Dash or Flask to display the sentiment analysis results.

2. **Automate the Process**: Schedule the script to run periodically (e.g., using a cron job or task scheduler) to fetch and analyze new Reddit posts continuously.

3. **Advanced Sentiment Analysis**: Consider using more sophisticated sentiment analysis models, like VADER or Hugging Face transformers, to improve the accuracy of sentiment classification.
 
 
