# The Overview
This project analyzes the **2023 job market for data science roles in the US,**.
This project was created in a way so that one's understand the job market more effectively. 

The data sourced from [Luke Barousse's Python Course](https://huggingface.co/datasets/lukebarousse/data_jobs) which provides a foundation for my analysis. The insights provide guidance for aspiring and experienced Data Scientists on which skills to prioritize, learn, or specialize in for career growth.

# The Background
This project examines job postings and salary trends to answer:

- Which skills are most in demand?

- How are in-demand skills trending for Data Scientists?

- How well do jobs and skills pay for Data Scientists?

- Which skills are optimal for career growth?

By leveraging job market data, I aim to help professionals make data-driven career decisions.

# The Tools Used
### Python: 
The backbone of my analysis, allowing me to analyze the data and find critical insights. I also used the following python libraries to make my work easier:

    1. Pandas Library: This was used to analyze data
    2. Matplotlib Library: This was used for data visualization
    3. Seaborn Library: This was used to help me create more advanced visuals.

### Jupyter Notebooks: 
The tool I used to run my python scripts which let me easily include my notes and analysis.
### Visual Studio Code:
My go-to for executing my Python Scripts.
### Git & GitHub: 
Essential for Version Control and sharing my code and analysis.

# The Analysis
## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles, I filtered out those positions by which ones were the most popular and got the top 5 skills for them. This query shows which skills I should focus on more depending on the role I'm targetting.

View my notebook with detailed steps here:
[2_skills_count.ipynb](project\2_skills_count.ipynb)

### Visualization
```python
fig, ax = plt.subplots(len(job_titles), 1)
sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_percent[df_skills_percent['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skills_count', palette='dark:b_r')
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].get_legend().remove()
    ax[i].set_xlim(0, 78)

    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1, n, f'{v:.0f}%', va='center')
    
    if i != len(job_titles) - 1:
        ax[i].set_xticks([])

fig.suptitle("Likelihood of Skills Requested in US Job Postings", fontsize=15)
fig.tight_layout(h_pad=1)
plt.show()
```
### Results
![Visualization of most demanded skills](project\images\skills_demand.png)

### Insights
- SQL and Python are critical across all roles, with SQL being especially vital for data analysts and engineers, while Python dominates in data science.

- Cloud and big data tools are highly valued for Data Engineers, indicating the industry's shift toward scalable data solutions.

- Data visualization and statistical tools vary by role, with Tableau being more relevant for analysts and R for data scientists.

- For aspiring professionals, focusing on SQL, Python, and cloud technologies will provide a competitive edge in the job market.

## 2. How are in-demand skills trending for Data Scientists?
### visualization
```python

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

for i in range(5):
    plt.text(11.2, df_plot.iloc[-1, i], df_plot.columns[i])

plt.show()
```
### Results
![Visualization of top trending skills](project\images\trending_skills.png)
*Bar graph visualizing the trending top skills for data scientist in the US in 20230*

### Insights:
- Python remains the most essential skill for data scientists, reinforcing its importance in analytics, machine learning, and AI.

- SQL is a necessary complementary skill, with steady but slightly fluctuating demand.

- R is slowly declining, while Tableau is gaining traction for visualization.

- SAS is losing relevance, suggesting a shift toward open-source tools and modern analytics platforms.

## 3. How well do jobs and skills pay for Data Scientists?
### Salary Analysis
#### Visualization
```python
sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)

ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```
#### Results
![Analyzing Salary of Data jobs in the US](project\images\Salary_Analysis.png)
*Box plot visualizing the salary distributions for the top 6 data job titles*

#### Insights
- Moving into senior roles significantly increases earning potential, with Senior Data Scientists and Engineers earning the most.

- Data Engineers and Data Scientists earn competitive salaries, making them attractive career paths.

- Data Analysts have lower salaries but can transition into higher-paying roles like data science or engineering with upskilling.

### Highest paid & Most Demanded skills for Data Scientists
#### Visualization
```python
fig, ax = plt.subplots(2, 1)

sns.barplot(data=df_DS_top_pay, x='median', y=df_DS_top_pay.index, ax=ax[0], hue='median', palette='dark:b_r')


sns.barplot(data=df_DS_skills, x='median', y=df_DS_skills.index, ax=ax[1], hue='median', palette='light:b')

plt.show()
fig.tight_layout()
```
#### Results
![Highest paid and most demanded skills in the US](project\images\Highest_paid_and_most_demanded_skills.png)

#### Insights
- Top-paying skills include Asana, Airtable, Watson, Unreal, and Ruby on Rails, with median salaries exceeding $200K.

- TensorFlow & Spark – indicating strong demand for machine learning and big data processing.

- There’s a gap between the highest-paid and most in-demand skills:
AI, automation, and niche expertise pay higher, but traditional data science skills (Python, SQL, AWS, Spark, etc.) are more widely required.

## 4. What is the most optimal skill to learn for Data Analyst?
#### Visualization
```python
from adjustText import adjust_text
sns.scatterplot(
    data=df_plot,
    x='skill_percent',
    y='median_salary',
    hue='technology'
)

sns.despine()
sns.set_theme(style='ticks')

texts = []
for i, txt in enumerate(df_DS_skills_high_demand.index):
    texts.append(plt.text(df_DS_skills_high_demand['skill_percent'].iloc[i], df_DS_skills_high_demand['median_salary'].iloc[i], txt))

adjust_text(texts, arrowprops=dict(arrowstyle='->', color='gray', lw=1))

plt.show()
```

#### Results
![Most Optimal skills for Data Scientist in the US](project\images\optimal_skills.png)

#### Insights
- Python and SQL are the best entry-level skills, with the highest job demand.
Machine Learning (TensorFlow) and Big Data (Spark, AWS) pay more but have fewer job postings—ideal for specialization.

- Cloud skills (AWS, Azure) are growing in demand and provide strong salary potential.

- Analytics skills (Tableau, Excel, Hadoop) are important but pay slightly less compared to programming and ML skills.

# What I Learned
### Python & Its Libraries

    - Improved my Python programming skills, particularly in data handling and visualization.

    - Worked extensively with Pandas and NumPy for data manipulation.
Used Seaborn and Matplotlib to create meaningful visualizations.

### Data Handling & Cleaning

    - Understood the importance of data cleaning and preprocessing before analysis.
    - Dealt with missing values, inconsistencies, and outliers in salary data.
    - Applied grouping, filtering, and aggregation techniques to extract insights.

### Advanced Concepts in Data Analysis

    - Learned how to interpret job market trends using statistical measures.
    - Gained experience in exploratory data analysis (EDA) to uncover hidden patterns.
    - Used median salary instead of mean to reduce the impact of outliers in salary distribution.

### Strategic Skill Analysis for Career Growth

    - Identified which skills are in demand vs. which skills pay well.
    - Understood the trade-off between demand and salary when choosing career paths.
    - Realized the importance of specializing in high-value skills for career advancement.

# Conclusion

This analysis provided valuable insights into the Data Science job market, helping identify the most strategic skills for career growth.

**For beginners:** Python, SQL, and R are the best starting points.

**For higher salaries:** Specializing in Machine Learning (TensorFlow, Spark) or Cloud (AWS, Azure) is beneficial.

**For long-term career growth:** A combination of programming, cloud, and ML expertise leads to the best opportunities.

By applying data-driven decision-making, professionals can make informed career choices and maximize their growth potential.







