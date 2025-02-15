# Overview

Welcome to my deep dive into the data job market with a focus on data analyst roles. This project was born out of a desire to navigate and understand the ever-evolving job market and to pinpoint the skills that truly matter. By exploring the top-paying and most in-demand skills, I aim to reveal the optimal paths for data analysts seeking rewarding opportunities.

The data for this project comes from Luke Barousse's Python Course—a rich source that provides detailed information on job titles, salaries, locations, and essential skills. Using a series of Python scripts, I’ve tackled key questions such as the most demanded skills, salary trends, and how demand intersects with pay in data analytics.

# The Questions
In this project, I set out to answer:

1. What are the skills most in demand for the top 3 most popular data roles?
 
2. How are in-demand skills trending for Data Analysts?

3. How well do jobs and skills pay for Data Analysts?

4. What are the optimal skills for data analysts to learn?

(Skills that are both high in demand and high paying)


# Tools I Used

For this analysis, I leveraged a robust set of tools:

Python: The backbone of the analysis.

Pandas: For data manipulation.

Matplotlib & Seaborn: For creating compelling visualizations.

Jupyter Notebooks: To seamlessly integrate code, analysis, and insights.

Visual Studio Code: My preferred environment for executing Python scripts.

Git & GitHub: For version control and sharing my work with the community

ChatGPT : For debugging my codes

# Data Preparation and Cleanup

Before diving into the analysis, I focused on ensuring data accuracy and usability through careful data cleaning.

## Import & Clean Up Data

I began by importing the necessary libraries and loading the dataset


```python
import ast
import pandas as pd
import seaborn as sns
from datasets import load_dataset
import matplotlib.pyplot as plt  

# Loading Data
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas()

# Data Cleanup
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
```

## Filter US Jobs

To concentrate on the U.S. market, I filtered the dataset to include only jobs based in the United States:

```python
df_US = df[df['job_country'] == 'United States']
```

# The Analysis
Each notebook in this project focuses on a different aspect of the data job market. Here’s an overview of the key questions and findings:

### 1. Most Demanded Skills for Top 3 Data Roles
I identified the top 3 most popular data roles and extracted their top 5 in-demand skills. This analysis not only highlights popular job titles but also shows which skills are critical based on the role.

#### View Detailed Steps: See the 2_Skill_Demand notebook.
#### Visualization Example:
python
Copy
Edit
```python
fig, ax = plt.subplots(len(job_titles), 1)
for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)[::-1]
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')
plt.show()
```
![image](https://github.com/user-attachments/assets/f2eb680b-3dde-4949-bb5d-5cd925fb9d78)



## Insights:

-SQL is a standout, being the most requested skill for both Data Analysts and Data Scientists.

-Python dominates for Data Engineers, featuring in nearly 68% of job postings.

-Each role demands a distinct mix of general and specialized skills.

### 2. Trending Skills for Data Analysts

For Data Analysts, I examined how skill demand evolved throughout 2023 by grouping skills by the month of job postings.

View Detailed Steps: Refer to the 3_Skills_Trend notebook.

Visualization Example:

```python
from matplotlib.ticker import PercentFormatter
df_plot = df_DA_US_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False, legend='full', palette='tab10')
plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))
plt.show()
```
![image](https://github.com/user-attachments/assets/c2abf1ec-c0c4-45f1-b065-5d2bdabb2343)

## Insights:

SQL remains consistently in demand, though its percentage slowly declines.

Excel sees a notable surge from September onwards, overtaking both Python and Tableau by year-end.

Python and Tableau maintain steady demand, reinforcing their role as essential tools.



