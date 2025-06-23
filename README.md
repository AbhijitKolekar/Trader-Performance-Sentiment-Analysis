# Junior Data Scientist - Trader Behavior Insights

## Project Overview

This project explores the intricate relationship between cryptocurrency trader performance and broader market sentiment. Leveraging historical trading data and the Bitcoin Fear & Greed Index, the analysis aims to uncover hidden patterns, identify key correlations, and deliver actionable insights that can inform smarter trading strategies.

## Assignment Objective

The primary objective of this assignment was to:
* Work with two primary datasets: Bitcoin Market Sentiment and Historical Trader Data.
* Explore the relationship between trader profitability/activity and market sentiment classifications (Extreme Fear, Fear, Neutral, Greed, Extreme Greed).
* Uncover hidden patterns in trader behavior across different market sentiment phases.
* Deliver insights that could potentially drive more effective trading strategies.

## Data Sources

Two primary datasets were utilized for this analysis:

1.  **Bitcoin Market Sentiment Data (`fear_greed_index.csv`):**
    * Provides daily sentiment classifications (e.g., Fear, Greed) based on the Bitcoin Fear & Greed Index.
2.  **Historical Trader Data (`historical_data.csv`):**
    * Contains granular trading records from a Hyperliquid mainnet account, including `Closed PnL`, `Account` information, `Timestamp`, and other trade details.

## Methodology

The analysis was performed using Python with libraries such as `pandas` for data manipulation, and `matplotlib` along with `seaborn` for data visualization. The key steps involved:

1.  **Data Loading & Preparation:**
    * Both datasets were loaded into Pandas DataFrames.
    * Timestamp columns were converted to datetime objects, and set as DataFrame indices for time-series analysis.
    * Missing 'leverage' column (as per the PDF description) was noted to be absent in `historical_data.csv` and excluded from relevant analysis to prevent errors.
2.  **Exploratory Data Analysis (EDA):**
    * Initial checks on data distributions and value counts (`Coin`, `Side`) were performed.
    * A histogram of `Closed PnL` was generated to understand its overall distribution.
3.  **Data Alignment and Merging:**
    * The granular trader data was aggregated to a daily level, calculating `total_closedPnL` (sum of daily profits/losses) and `trade_count` (number of trades per day).
    * This daily trader performance data was then merged with the daily sentiment data based on their respective dates, ensuring an accurate alignment of trading activity with market sentiment.
4.  **Relationship Exploration and Pattern Uncovery:**
    * **Performance by Sentiment:** Trader performance metrics (average and median daily PnL) were calculated for each sentiment classification.
    * **Visualizing PnL Distribution:** Box plots were used to visualize the distribution of `total_closedPnL` across different sentiment categories.
    * **Correlation Analysis:** Market sentiment was mapped to a numerical score, and a correlation matrix was generated to quantify the relationship between `total_closedPnL`, `trade_count`, and `Sentiment_Score`.
    * **Time-Series Overlay:** Daily `total_closedPnL` was plotted over time, with sentiment classifications overlaid to visually track performance trends against market mood.

## Key Findings & Insights

Based on the analysis, the following key insights were observed:

* **Counter-intuitive Profitability during "Fear":** Days categorized as **'Fear'** showed the highest average daily `Closed PnL`, suggesting that some trading strategies might be more profitable during periods of market apprehension.
* **Strong PnL-Trade Count Correlation:** There is a very strong positive correlation ($0.98$) between `total_closedPnL` and `trade_count`, indicating that higher trading activity generally aligns with higher total daily PnL (though the direction of causation would require further analysis).
* **Weak Sentiment-Performance Correlation:** The numerical `Sentiment_Score` showed a very weak negative correlation with `total_closedPnL` and `trade_count` (around -0.04 to -0.05). While slight, this further supports the observation that positive sentiment doesn't necessarily lead to proportionally higher PnL for the traders in this dataset.
* **Median PnL Near Zero:** For most sentiment categories, the median daily PnL was zero, implying that while some days had significant gains (pulling up the mean), a large number of days had net PnL close to break-even. This highlights the presence of outliers (highly profitable days) in the data.

These insights suggest that effective trading strategies might involve counter-cyclical approaches or specific risk management during different sentiment phases.

## How to Run the Code

To replicate this analysis, follow these steps:

1.  **Prerequisites:**
    * Ensure you have Python installed (Python 3.x recommended).
    * Install the necessary libraries:
        ```bash
        pip install pandas matplotlib seaborn
        ```
2.  **Data Files:**
    * Download `historical_data.csv` and `fear_greed_index.csv`.
    * Place both CSV files in the same directory as your Python script.
3.  **Run the Script:**
    * Save the provided Python code (e.g., as `sentiment_analysis.py`).
    * Open a terminal or command prompt, navigate to the directory where you saved the files, and run the script:
        ```bash
        python sentiment_analysis.py
        ```

The script will print various data summaries and performance metrics to the console, and it will generate the following visualization files in the same directory:

* `closed_pnl_distribution.png`
* `pnl_by_sentiment_boxplot.png`
* `correlation_heatmap.png`
* `pnl_with_sentiment_overlay.png`

## Visualizations

The following plots are generated by the script:

* **`closed_pnl_distribution.png`**: Shows the frequency distribution of daily closed PnL.
* **`pnl_by_sentiment_boxplot.png`**: Illustrates the spread of daily total closed PnL across different market sentiment categories.
* **`correlation_heatmap.png`**: Displays the correlation coefficients between total closed PnL, trade count, and the sentiment score.
* **`pnl_with_sentiment_overlay.png`**: Plots daily total closed PnL over time, with sentiment classifications highlighted.

---

**[Abhijit Kolekar]**
