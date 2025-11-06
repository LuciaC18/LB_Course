# Analysis

## What are the most demanded skills for the top 3 most popular data roles?

This analysis explores U.S. job postings to identify the most in-demand roles and the key skills employers are seeking. Using aggregated job posting data, I first determined the most frequently advertised positions, then examined the top five skills associated with each role.

By comparing skill frequencies across popular roles such as Data Analyst and Data Scientist, the analysis highlights which technical competencies are most valued in today’s job market—most notably Python, SQL, and Excel. These insights provide a data-driven perspective on hiring trends, helping to pinpoint the core skills that consistently appear in high-demand positions.

For detailed steps, you can view the notebook [here](3_Project/2_Skills_Demand.ipynb).

### Visualise Data
```python
fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_pct[df_skills_pct['job_title_short']== job_title].head(5)
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], palette='flare_r')
    ax[i].set_title(job_title)
    ax[i].set_ylabel('')
    ax[i].set_xlabel('')
    ax[i].get_legend()
    ax[i].set_xlim(0,78)

    for n, v in enumerate(df_plot['skill_percent']):
        ax[i].text(v + 1, n, f'{v:.0f}%', va='center')
    
    if i != len(job_titles) - 1:
        ax[i].set_xticks([])

fig.suptitle('Likelihood of Skills Requested in US Job Postings', fontsize=15)
fig.tight_layout(h_pad=0.5)
plt.show()
```
### Results

![Visualization of Top Skills for Data Roles](3_Project/images/skill_demand_all_data_roles.png)

### Insights

1. **SQL and Python dominate across all roles**
    - SQL appears in the top two skills for every role, confirming it as a universal requirement for data professionals.

    - Python is equally strong — it’s the top skill for Data Scientists (72%) and a core skill for Data Engineers (65%).

2. **Role-specific skill differences**

    - Data Analysts emphasize Excel and Tableau, reflecting a focus on reporting, visualization, and business-facing analytics.

    - Data Engineers show strong demand for AWS, Azure, and Spark — pointing to a focus on cloud infrastructure and large-scale data pipelines.

    - Data Scientists rely more heavily on R, SAS, and Tableau, which align with statistical modeling and analytical visualization.

3. **Shared foundation, diverging specializations**

    - The overlap in Python and SQL shows a shared technical foundation, but beyond that, each role specializes:

        - Analysts lean toward visualization tools.
        - Engineers toward cloud and big data platforms.
        - Scientists toward modeling and experimentation frameworks.

## How are in-demand skills trending for Data Analysts?

### Visualise Data

``` python
df_plot = df_DA_US_percent.iloc[:, :5]
sns.lineplot(data=df_plot, dashes=False)
sns.set_theme(style='ticks')
sns.despine()

plt.title('Trending Top Skills for Data Analysts in the US')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('2023')
plt.legend().remove()

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))


offsets = {
    'tableau': 1.5,
    'python': -1.5
} # need to manually otherwise these labels overlap

for i in range(5):
    label = df_plot.columns[i]
    y_pos = df_plot.iloc[-1, i] + offsets.get(label, 0)
    plt.text(11.2, y_pos, label)

```

### Results

![Trending Top Skills for Data Analysts in the US](3_Project/images/skills_trend_DA.png)

### Insights

SQL and Excel remain foundational skills for Data Analysts throughout 2023, with SQL consistently dominating job requirements. Tableau and Python show stable demand, while SAS continues a gradual decline. Overall, the data reflects a shift toward widely used analytical tools (SQL, Python, Tableau) and away from legacy platforms.