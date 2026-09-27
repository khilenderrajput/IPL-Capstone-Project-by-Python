# 🏏 IPL Data Analysis — Capstone Project

![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge\&logo=python\&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge\&logo=pandas\&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-013243?style=for-the-badge\&logo=numpy\&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C?style=for-the-badge\&logo=plotly\&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-Statistical%20Visualization-4C72B0?style=for-the-badge)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge\&logo=jupyter\&logoColor=white)

---

## 📌 Project Overview

This project is an exploratory **IPL (Indian Premier League) Data Analysis** project developed using Python, Pandas, NumPy, Matplotlib, Seaborn, and Jupyter Notebook.

The objective of this project is to explore IPL match-level data and extract meaningful insights related to:

* 🏆 Team match-winning performance
* 🪙 Toss decisions
* 🎯 Relationship between toss winner and match winner
* 🏏 Winning methods
* ⭐ Player of the Match performance
* 📊 Top run scorers
* 🎳 Bowling performance
* 🏟️ Venue-wise match distribution
* 🔎 Highest winning margins
* 🔥 Highest individual scores
* 🎯 Best bowling figures

The analysis combines **data cleaning, exploratory data analysis (EDA), aggregation, grouping, filtering, and data visualization** to understand different aspects of IPL matches.

---

# 🎯 Project Objectives

The main objectives of this project are:

1. Analyze IPL match data using Python.
2. Understand the distribution and structure of the dataset.
3. Check the dataset for missing values.
4. Identify teams with the highest number of match victories.
5. Analyze common toss decisions.
6. Determine how frequently the toss winner also wins the match.
7. Understand whether matches are generally won by runs or another method.
8. Identify players receiving the most Player of the Match awards.
9. Analyze the leading run scorers based on aggregated high scores.
10. Examine bowling performances using wickets and bowling figures.
11. Identify venues hosting the most matches.
12. Extract additional insights using custom analytical questions.
13. Present findings through clear and interpretable visualizations.

---

# 🗂️ Project Structure

```text
IPL-Data-Analysis/
│
├── Capstone_Project(1).ipynb
├── IPL.csv
└── README.md
```

### Files Description

| File                        | Description                                                             |
| --------------------------- | ----------------------------------------------------------------------- |
| `Capstone_Project(1).ipynb` | Complete Jupyter Notebook containing Python analysis and visualizations |
| `IPL.csv`                   | IPL match-level dataset used for the analysis                           |
| `README.md`                 | Complete project documentation                                          |

---

# 🧰 Technologies & Libraries

The project is implemented using the following technologies:

### 🐍 Python

Python is used as the primary programming language for data loading, manipulation, analysis, and visualization.

### 🐼 Pandas

Pandas is used extensively for:

* Loading the CSV dataset
* Inspecting the dataset
* Handling missing values
* Counting categorical values
* Grouping data
* Sorting results
* Filtering records
* Creating derived columns

### 🔢 NumPy

NumPy is imported for numerical computing and compatibility with analytical workflows.

### 📊 Matplotlib

Matplotlib is used to create charts and visualize analytical results.

### 🎨 Seaborn

Seaborn is used to create statistical and categorical visualizations such as:

* Bar plots
* Count plots

### 📓 Jupyter Notebook

Jupyter Notebook provides the interactive environment where the complete analysis is performed.

---

# 📥 Dataset

The project uses an IPL match-level CSV dataset named:

```text
IPL.csv
```

The notebook loads the dataset using:

```python
df = pd.read_csv("IPL.csv")
```

The dataset contains match-related information used for team, toss, player, bowling, venue, and winning-margin analysis.

Important columns used throughout the project include:

```text
match_id
match_winner
toss_winner
toss_decision
won_by
margin
player_of_the_match
top_scorer
highscore
best_bowling
best_bowling_figure
venue
```

---

# 🔍 Data Loading & Initial Exploration

The first stage of the project focuses on importing the required Python libraries and loading the IPL dataset.

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
import warnings

warnings.filterwarnings("ignore")

df = pd.read_csv("IPL.csv")
df.head(5)
```

The first five records are displayed using:

```python
df.head(5)
```

This provides an initial understanding of the dataset and its available fields.

---

# 📋 Dataset Information

The project uses:

```python
df.info()
```

to inspect:

* Column names
* Data types
* Non-null values
* Dataset structure

The dataset dimensions are checked using:

```python
df.shape
```

The notebook also prints the number of rows and columns:

```python
print(f"your rows are {df.shape[0]} and your coloumns are {df.shape[1]}")
```

This gives an initial overview of the size of the dataset before performing detailed analysis.

---

# 🧹 Missing Value Analysis

Missing values are checked using:

```python
df.isnull().sum()
```

This helps identify whether any columns contain missing observations.

Checking missing values is an important step before performing aggregations and visualizations because incomplete records can affect analytical results.

---

# 🏆 Team Performance Analysis

## 1. Which Team Won the Most Matches?

The first major analytical question is:

> **Which team won the most matches?**

The project uses:

```python
match_wins = df["match_winner"].value_counts()
```

`value_counts()` calculates the number of matches won by each team.

The results are visualized using a horizontal bar chart:

```python
sns.barplot(
    x=match_wins.values,
    y=match_wins.index,
    palette="viridis"
)

plt.title("Most match win by team")
```

### 📊 Visualization

The resulting chart allows the number of victories for each team to be compared visually.

This analysis helps identify teams with a larger number of recorded match victories within the dataset.

---

# 🪙 Toss Decision Analysis

## 2. Toss Decision Trends

The next analysis investigates the decisions made after winning the toss.

The notebook uses:

```python
sns.countplot(
    x=df["toss_decision"],
    palette="rainbow"
)

plt.title("Toss winner")
```

This visualization displays the frequency of the different toss decisions present in the dataset.

### 🎯 Purpose

The analysis helps understand the preferred decision taken after winning the toss.

---

# 🪙🏏 Toss Winner vs Match Winner

## 3. Does the Toss Winner Also Win the Match?

The project investigates how often the team winning the toss also becomes the match winner.

The analysis counts records where:

```python
df["toss_winner"] == df["match_winner"]
```

The count is calculated using:

```python
count = df[
    df["toss_winner"] == df["match_winner"]
]["match_id"].count()
```

The corresponding percentage is calculated as:

```python
percentage = (count * 100) / df.shape[0]
```

and rounded to two decimal places:

```python
percentage.round(2)
```

### 📌 Analytical Purpose

This provides a simple measure of the relationship between winning the toss and winning the match.

It does **not** establish causation; it simply measures how frequently the two outcomes coincide within the dataset.

---

# 🏏 Match Winning Method

## 4. How Do Teams Win?

The project examines the `won_by` column to understand the recorded winning method.

```python
sns.countplot(x=df["won_by"])

plt.title("Won By")
```

The count plot shows the frequency of the different winning methods represented in the dataset.

This helps provide an overview of how matches were won.

---

# ⭐ Key Player Performance Analysis

A separate section of the notebook focuses on individual player performances.

---

## 5. Most Player of the Match Awards

The project identifies the top players based on the number of Player of the Match awards.

```python
count = df["player_of_the_match"].value_counts().head(10)
```

The top 10 players are then visualized:

```python
sns.barplot(
    x=count.values,
    y=count.index,
    palette="mako"
)

plt.title("Top 10 player of the match")
```

### 📊 What This Shows

The analysis highlights players who appear most frequently as the Player of the Match in the dataset.

This provides a useful view of recurring match-level individual performances.

---

# 🏏 Top Run Scorers

## 6. Top 2 Scorers

The notebook analyzes the `top_scorer` and `highscore` columns.

The high scores are aggregated for each player:

```python
high = df.groupby("top_scorer")["highscore"] \
        .sum() \
        .sort_values(ascending=False) \
        .head(2)
```

The resulting values are displayed and visualized using:

```python
high.plot(kind="barh")
```

### 📌 Analytical Approach

The project groups the records by the player identified as the top scorer and calculates the sum of the recorded `highscore` values.

The top two results are then selected after sorting in descending order.

---

# 🎳 Bowling Performance Analysis

## 7. Best Bowling Figures

The notebook analyzes the `best_bowling_figure` column.

The bowling figure is processed to extract the wickets component:

```python
df["highest_wickets"] = df["best_bowling_figure"].apply(
    lambda x: x.split("--")[0]
)

df["highest_wickets"] = df["highest_wickets"].astype(int)
```

The transformed value is then aggregated by bowler:

```python
top_bolwer = df.groupby("best_bowling")[
    "highest_wickets"
].sum().sort_values(
    ascending=False
).head(10)
```

The top bowling performances are visualized using:

```python
top_bolwer.plot(kind="barh")
```

### 🎯 Purpose

This analysis uses the recorded bowling figures to identify bowlers associated with higher aggregated wicket counts in the dataset.

---

# 🏟️ Venue Analysis

## 8. Most Matches Played by Venue

The project also investigates the number of matches associated with each venue.

The analysis uses:

```python
venue_count = df["venue"].value_counts()
```

The venue counts are then visualized using:

```python
sns.barplot(
    x=venue_count.values,
    y=venue_count.index,
    palette="rainbow"
)
```

### 📍 Purpose

This analysis provides a venue-wise view of the dataset and identifies venues appearing most frequently in the match records.

---

# 🔎 Custom Questions & Insights

The project concludes with additional questions designed to extract specific insights from the dataset.

---

# 🏃 Q1. Which Team Won by the Highest Margin in Runs?

The notebook filters matches where the winning method is recorded as `Runs`:

```python
df[df["won_by"] == "Runs"]
```

The results are sorted according to the winning margin:

```python
.sort_values(
    by="margin",
    ascending=False
)
```

The highest-margin match is then selected:

```python
.head(1)
```

The analysis displays:

```python
[
    "match_winner",
    "margin"
]
```

### 📌 Output Interpretation

This identifies the team associated with the largest recorded winning margin by runs in the dataset.

---

# 🔥 Q2. Which Player Had the Highest Individual Score?

The notebook finds the maximum value in the `highscore` column:

```python
df["highscore"].max()
```

It then selects the corresponding player and score:

```python
df[
    df["highscore"] == df["highscore"].max()
][
    ["top_scorer", "highscore"]
]
```

### 📊 Purpose

This identifies the player associated with the highest individual score recorded in the dataset.

---

# 🎯 Q3. Which Bowler Had the Best Bowling Figures?

The notebook uses the previously created `highest_wickets` column to identify the maximum wicket value:

```python
df[
    df["highest_wickets"] == df["highest_wickets"].max()
][
    ["best_bowling", "best_bowling_figure"]
]
```

### 📌 Purpose

This retrieves the bowler and the corresponding bowling figure associated with the maximum extracted wicket value.

---

# 📊 Exploratory Data Analysis Workflow

The overall workflow followed in this project can be summarized as:

```text
              IPL.csv
                 │
                 ▼
        Load Dataset with Pandas
                 │
                 ▼
       Initial Dataset Inspection
                 │
        ┌────────┴────────┐
        ▼                 ▼
   Shape / Info      Missing Values
        │                 │
        └────────┬────────┘
                 ▼
          Exploratory Analysis
                 │
      ┌──────────┼──────────┐
      │          │          │
      ▼          ▼          ▼
    Teams      Toss      Players
      │          │          │
      ▼          ▼          ▼
    Wins     Decisions    Batting
                           │
                           ▼
                        Bowling
                 │
                 ▼
               Venues
                 │
                 ▼
        Custom Questions
                 │
                 ▼
        Insights & Visualizations
```

---

# 📈 Visualizations Used

The project uses multiple visualization techniques to make the analysis easier to understand.

### Bar Charts

Used for:

* Team match wins
* Player of the Match rankings
* Top scorer analysis
* Bowling analysis
* Venue analysis

### Count Plots

Used for:

* Toss decisions
* Winning methods

### Horizontal Bar Charts

Used when comparing multiple teams or players where category names are easier to read horizontally.

---

# 🧠 Key Analytical Areas

The project covers several important data analytics concepts:

### 1. Data Loading

```python
pd.read_csv()
```

### 2. Dataset Inspection

```python
df.head()
df.info()
df.shape
```

### 3. Missing Value Detection

```python
df.isnull().sum()
```

### 4. Frequency Analysis

```python
value_counts()
```

### 5. GroupBy Analysis

```python
df.groupby()
```

### 6. Sorting

```python
sort_values()
```

### 7. Filtering

```python
df[df["column"] == value]
```

### 8. Aggregation

```python
sum()
count()
max()
```

### 9. Feature Transformation

The bowling figure is transformed into a numerical wicket value using string processing and type conversion.

### 10. Data Visualization

The project uses Matplotlib and Seaborn to convert analytical results into visual representations.

---

# 🧪 Example Python Workflow

A simplified version of the project's analytical workflow is:

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv("IPL.csv")

# Dataset inspection
df.head()
df.info()
df.shape

# Missing values
df.isnull().sum()

# Team wins
match_wins = df["match_winner"].value_counts()

# Toss analysis
df["toss_decision"].value_counts()

# Toss winner vs match winner
count = df[
    df["toss_winner"] == df["match_winner"]
]["match_id"].count()

percentage = (count * 100) / df.shape[0]

# Player of the Match
df["player_of_the_match"].value_counts().head(10)

# Top scorers
high = df.groupby("top_scorer")["highscore"] \
         .sum() \
         .sort_values(ascending=False) \
         .head(2)
```

---

# 💡 Business / Analytical Perspective

Although this is a sports dataset, the project demonstrates general-purpose data analytics skills that can be applied to business datasets.

The same analytical concepts can be used for:

* Customer analysis
* Sales analysis
* Marketing analytics
* Product performance analysis
* Employee analytics
* Financial analytics
* E-commerce analytics

For example:

```text
IPL Team Wins
      ↓
Category Performance

Player Performance
      ↓
Individual Performance

Venue Analysis
      ↓
Location-Based Analysis

Toss Analysis
      ↓
Event / Decision Analysis

Winning Margin
      ↓
Performance Gap Analysis
```

---

# 🎓 Skills Demonstrated

This project demonstrates practical experience with:

* Python programming
* Data analysis
* Exploratory Data Analysis
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Data aggregation
* GroupBy operations
* Data filtering
* Sorting
* Frequency analysis
* Missing-value inspection
* Feature transformation
* Statistical exploration
* Data visualization
* Analytical questioning
* Insight generation
* Jupyter Notebook

---

# 🚀 How to Run the Project

## Step 1 — Clone the Repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
```

## Step 2 — Navigate to the Project

```bash
cd IPL-Data-Analysis
```

## Step 3 — Install Required Libraries

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

## Step 4 — Start Jupyter Notebook

```bash
jupyter notebook
```

## Step 5 — Open the Notebook

Open:

```text
Capstone_Project(1).ipynb
```

Make sure:

```text
IPL.csv
```

is available in the same working directory.

---

# ▶️ Running in Google Colab

The notebook can also be executed in Google Colab.

### Steps

1. Open Google Colab.
2. Upload `Capstone_Project(1).ipynb`.
3. Upload `IPL.csv`.
4. Run the notebook cells sequentially.

If the dataset is not located in the notebook's working directory, update the CSV path accordingly.

---

# 📁 Recommended Repository Structure

For a clean GitHub repository, the project can be organized as:

```text
📦 IPL-Data-Analysis
│
├── 📓 Capstone_Project(1).ipynb
├── 📊 IPL.csv
├── 📄 README.md
└── 📁 images/
    └── analysis_visualizations.png
```

---

# 🔮 Future Improvements

The current notebook focuses primarily on exploratory analysis. The project can be extended with additional analytical techniques.

Possible future improvements include:

### 📊 Advanced EDA

Explore additional relationships between:

* Teams
* Toss decisions
* Match outcomes
* Players
* Venues
* Winning margins

### 📈 Interactive Dashboards

The analysis could be converted into an interactive dashboard using tools such as:

* Power BI
* Tableau
* Plotly
* Streamlit

### 🏏 Player-Level Analysis

Additional analysis could include:

* Player consistency
* Batting performance by season
* Bowling performance by season
* Player performance across venues

### 🏟️ Venue-Level Analysis

Further analysis could investigate:

* Average winning margin by venue
* Winning methods by venue
* Toss decisions by venue

### 🪙 Toss Analysis

The relationship between:

```text
Toss Decision
        ↓
Match Result
```

could be investigated in greater detail.

### 📅 Season-Wise Analysis

If season information is available, the project could be expanded to compare IPL seasons over time.

---

# ⚠️ Analytical Notes

This project is primarily an **exploratory data analysis** exercise.

Some calculations in the notebook represent aggregated observations rather than advanced statistical conclusions.

For example, the toss analysis measures how frequently the toss winner and match winner are the same. This should be interpreted as an observed association in the dataset rather than proof that winning the toss causes a team to win the match.

Similarly, the top-scorer analysis uses the sum of the `highscore` field grouped by `top_scorer`, following the calculation implemented in the notebook.

---

# 📌 Project Highlights

### 🏆 Team Analysis

Identified and visualized teams according to their recorded number of match victories.

### 🪙 Toss Analysis

Analyzed toss decisions and the relationship between toss winners and match winners.

### ⭐ Player Analysis

Identified players with the highest number of Player of the Match appearances.

### 🏏 Batting Analysis

Aggregated recorded high scores to identify the top two results.

### 🎳 Bowling Analysis

Processed bowling figures and analyzed wicket-related performance.

### 🏟️ Venue Analysis

Examined the frequency of matches across different venues.

### 🔎 Custom Insights

Answered targeted questions related to winning margins, individual scores, and bowling figures.

---

# 📚 Learning Outcomes

Through this project, the following practical concepts were applied:

```text
Raw Dataset
     ↓
Data Loading
     ↓
Data Inspection
     ↓
Data Quality Check
     ↓
Data Transformation
     ↓
Aggregation
     ↓
Filtering & Sorting
     ↓
Visualization
     ↓
Analytical Questions
     ↓
Insights
```

The project provides hands-on practice in transforming raw match-level data into understandable analytical outputs.

---

# 👨‍💻 Author

## Khilender Rajput

**Aspiring Data Analyst | Data Analytics Enthusiast**

Interested in:

* Data Analytics
* Python
* SQL
* Data Visualization
* Machine Learning
* Business Intelligence

### 🔗 Connect

**GitHub:**
https://github.com/khilenderrajput

**LinkedIn:**
https://www.linkedin.com/in/khilendr-rajput-936519337/

---

# ⭐ If You Found This Project Useful

If you found this project interesting or useful, consider giving the repository a ⭐ on GitHub.

Your feedback and suggestions are always welcome.

---

## 🏏 Final Summary

This IPL Data Analysis project demonstrates a complete exploratory workflow starting from loading a raw CSV dataset and performing initial data inspection through to data transformation, aggregation, visualization, and custom analytical questions.

Using **Python, Pandas, NumPy, Matplotlib, and Seaborn**, the project explores team performance, toss decisions, match outcomes, player achievements, batting scores, bowling figures, venues, and winning margins.

The project serves as a practical demonstration of foundational **Data Analytics and Exploratory Data Analysis (EDA)** skills using a real-world sports dataset.
