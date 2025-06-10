# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filtered out those positions by which ones were the most popular, and got the the top 5 skills for these top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook:
[2_Skill_Demanded.ipynb](3_Project/2_Skill_Demand.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1, figsize=(8, 8))

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    sns.barplot(df_plot,x='percentage', y='job_skills', ax=ax[i], hue='percentage', palette='dark:b_r')

plt.show()
```
### Results

![Visualization of Top Skills for Data Nerds](3_Project/images/skill_demanded.png)

### Insights


1. Python and SQL are must-have skills across all data roles.

2. Excel and Tableau are still very relevant for Data Analysts but less so for Engineers and Scientists.

3. Cloud and Big Data tools (AWS, Azure, Spark) are essential for Data Engineers.

4. R and SAS are more niche or legacy tools — useful but not primary.

5. Role Focus Differentiation:
    - Analysts: Reporting, visualization, business interaction.
    - Engineers: Infrastructure, cloud, data pipelines.
    - Scientists: Advanced analytics, modeling, machine learning.

6. SQL is highly demanded for Data Engineers (68%) and equally for Analysts and Scientists (51%), while Python peaks for Data Scientists (72%), followed by Engineers (65%) and Analysts (27%).

## 2. How are in-demand skills are trending for Data Analysts?

### Visualize Data

```python
sns.lineplot(df_plot, dashes=False, palette='tab10', legend=False)
sns.set_theme(style='ticks')
sns.despine()

for i in range(5):
    plt.text(3, df_plot.iloc[4, i], df_plot.columns[i])

plt.tight_layout()

```

### Results

![Trending Top Skills for Data Analysts in the US](3_Project/images/trending_skills.png)

*Bar graph visualizing the trending top skills for Data Analysts in the US in 2023.*

### Insights

- SQL consistently led demand for Data Analysts throughout 2023, peaking at ~54% in January and maintaining dominance across all months.
- Excel held steady around 42% for most of the year but saw a noticeable drop in the final quarter, briefly rebounding in December.
- Python and Tableau trended closely together between 26–30%, while SAS remained the least requested skill, fluctuating between 18–22%.

## 3. How well do jobs and skills pay for Data Analysts?

### Visualize Data

```python
sns.boxplot(data=df_US_top6, x='salary_year_avg', y='job_title_short', order=job_order)
plt.xlim(0, 600000)
plt.title('Salary Distributions in the United States')
plt.xlabel('Median Salary $USD')
plt.ylabel('')
```
### Results

![Salary Year Distributions in the US](3_Project/images/salary_distributions.png)

*Box Plot graph visualizing the salary distributions in the US.*

### Insights

- Senior roles (e.g., Senior Data Scientist and Senior Data Engineer) show noticeably higher median salaries, with most salaries concentrated between $150K–$200K, and some outliers even approaching $600K.
- Data Scientists and Data Engineers (non-senior) have comparable distributions, both centered around $130K–$160K, but Data Scientists tend to have a slightly wider range and more high-end outliers.
- Data Analysts and Senior Data Analysts earn significantly less than their engineering and science counterparts, with most Data Analysts falling between $70K–$110K, and seniors reaching around $130K at the median.

### Highest Paid and Most In-Demand Skills for Data Analysts

### Visualize Data

```python

fig, ax = plt.subplots(2, 1, figsize=[9,6])
sns.barplot(data=df_top_pay,x='median', y='job_skills', ax=ax[0], hue='median', palette='dark:b_r')

df_in_demand_skill_sort = df_in_demand_skill.sort_values(by='median', ascending=False)
sns.barplot(data=df_in_demand_skill_sort,x='median', y='job_skills', ax=ax[1], hue='median', palette='light:b')

fig.tight_layout()
plt.show()
```

### Results

![Median Salary VS Skill For Data Analysts](3_Project/images/highest_paid_most_demand_skills.png)

*Bar graph visualizing the highest paid and most in-demand skills for Data Analysts.*

### Insights

- Highest paid skills like dplyr, bitbucket, and gitlab offer median salaries close to $190K–$200K, indicating that niche or specialized tools yield premium compensation for Data Analysts.
- Most in-demand skills, including python, tableau, and r, offer lower median salaries (around $90K–$95K), suggesting that widespread use may dilute salary premiums.
- There's a disconnect between demand and pay—tools like excel and word are frequently requested but command the lowest median salaries, highlighting that high demand doesn’t always equate to high compensation.

## 4. What are the most optimal skills to learn for Data Analysts?

### Visualize Data

```python
from adjustText import adjust_text

plt.figure(figsize=(8,5))
ax = sns.scatterplot(data=df_plot, x='skill_percent', y='median_salary', hue='technology')
sns.set_theme(style='ticks')
sns.despine()

texts = []
for i in range(len(df_job_skills)):
    x = df_job_skills['skill_percent'].iloc[i]
    y = df_job_skills['median_salary'].iloc[i] + 100  # tiny Y shift to avoid stacking
    label = df_job_skills.index[i]
    texts.append(ax.text(x, y, label, fontsize=11, weight='bold'))

```

### Results

![Most Optimal Skill To Learn](3_Project/images/most_optimal_skills.png)

*Scatter plot graph visualizing the most optimal skills to learn for data analysts.*

### Insights

- SQL is the most in-demand skill for data analysts, appearing in over 14% of job postings. As a programming skill, it also offers a solid median salary (~$91K), making it highly optimal to learn.

- Python is the highest-paying programming skill, with a median salary close to $98K. Despite being in fewer postings (~8%), it offers great value due to its high salary and growing relevance in data analysis and machine learning.

- Tableau and Power BI are top analyst tools to consider, with Tableau offering a higher median salary (~$93K) and appearing in ~8% of job postings. Power BI appears in 5% and provides a decent salary ($90K), making both valuable for data visualization.