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


