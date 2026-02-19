# The Analysis
## 1. what are the most demanded skills for the top 3 most popular data roles?

to find the most demanded skills for the top 3 most popular dat roles, I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 skills. this query highlights the most popular job titles and their top skills, showing which skills i should pay attention to depending on the role i'm tareting.

view my notebook with deatiled steps here:
[2_skill_demand.ipynb](3_project\2_skill_demand.ipynb)

### Visualize Data

''' python
fig, ax = plt.subplots(len(job_titles), 1)
sns.set_theme(style='ticks')  # Set a clean style for the plots
for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title]. head(5)
    # df_plot.plot(kind='barh', x='job_skills', y='skill_percentage', ax=ax[i], title=job_title)
    sns.barplot(data=df_plot, x='skill_percentage', y='job_skills', ax=ax[i], hue='skill_count',palette='dark:b_r')
    
    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    ax[i].set_title(job_title)
    ax[i].set_xlim(0, 80)  # Set x-axis limits to 0-100% for better comparison
    ax[i].get_legend().remove()  # Remove legend for cleaner look

    for n, v in enumerate(df_plot['skill_percentage']):
        ax[i].text(v + 1, n, f'{v:.0f}%', color='black', va='center')  # Add percentage labels to bars
    if i != len(job_titles) - 1:  # Remove x-ticks for all but the last plot
        ax[i].set_xticks([])
    # ax[i].set_xticks(range(0, 81, 20))  # Set x-ticks at intervals of 20%
    # ax[i].invert_yaxis()  # To display the highest count at the top
    ax[i].legend().remove()  # Remove legend for cleaner look
fig.suptitle('Likelihood of skills requested in US job Postings', fontsize=16)
fig.tight_layout(h_pad=0.5) # Adjust the vertical spacing between subplots 
plt.show()
'''
### Results

![visualization of top skills for data roles](3_project\inages\skill_demand_of_al_roles.png)

### Insights
 python is a versatile skill, highly demanded across all three roles, but most prominently for datas cientists(72%) and data engineers(65%).

 SQL is the most requested skill for data analysts and data scientists, with it in over half the job postings for both roles.

 for data engineers, python is the most souht after skill, appearing in 68% of job postings.

 data engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and data scientists who are expected to be proficient in more general data mangement and analysis tools like excel and tableau

 # The Analysis

 ## 2. How are the in_demand skills trending for data analysts?

 ### Visualize Data

 ''' Python

 sns.lineplot(data=df_plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()
plt.title('trending top skills for data analysts in the US')
plt.ylabel('likelihood in the job posting')
plt.xlabel('2026')
plt.legend().remove()

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

for i in range(5):
    plt.text(11.2, df_plot.iloc[-1, i], df_plot.columns[i] )

plt.show()

'''

### Results

Trending  top skills for Data Analysts in the US

Bar graph visualizing the trending top skills for data analysts in the US as of 2026(date of access of dataset)

space for image

### Insights:
SQL remains themost consistently demanded skill throughout the year, although it shows a gradual decline in demand

Excel experienced a significant increase in demand starting around september, surpassing both python and tableau by the end of the year.

both python and tableau show relatively stable demand throughout the year with some fluctuations but remain essential skills for data analysts. power BI, while less demanded compared to others, shows a slight upward trend towards the year's end.

# The Analysis
## 3. How well do Jobs and skills pay for Data Analysts?

### Salary analysis for Data Analysts

''' Python

sns.boxplot(data=df_us_top6, x='salary_year_avg', y='job_title_short', orient='h', order=job_order)
sns.set_theme(style='ticks')

plt.title('Salary Distributions in the United States')
plt.ylabel('')
plt.xlabel('Yearly Salary (USD)')
plt.xlim(0, 600000)
ax= plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, p: f'${int(x/1000)}K'))
plt.tight_layout()
plt.show()

 '''
### Results
![Salary Distribution of data jobs in the US](3_project\images\salary_analysis_output.png)
* Box plot visualizing the salary distributions for the top 6 data job titles.*

### Insights:
there is a significant variation in salary ranges across different job titles. senior data scientist positions tend to have the highest salary potential, with up to $600K, indicating the high experience in the industry.

senior data engineer and senior data scientist roles show a considerable number of outliers on the hihger end of the salary spectrum, suggesting that exceptional skills or circumstances can lead to high pay in these roles. in contrast, data analyst roles demonstrate more consistency in salary, with fewer outliers.

the median salaries increase with the seniority and specialization of the roles. senior roles(senior data scientist, senior data engineer) not only have higher median salaries but also larger differences in the typical salaries, reflecting greater variance in the compensation as responsibilities increase.

# the analysis:
Investigating median salary vs skill for data analysts

## 3. how well do jobs and skills pay for data 

### highest paid & most demanded skills for data
#### visualize data

'''python

fig, ax = plt.subplots(2, 1)

sns.set_theme(style="ticks")
sns.barplot(data=df_da_top_pay, y=df_da_top_pay.index, x='median', ax=ax[0], hue='median', palette='dark:b_r')
ax[0].legend().remove()
#df_da_top_pay.plot(kind='barh', y='median', ax=ax[0], legend=False)
#ax[0].invert_yaxis()
ax[0].set_title('Top 10 Skills for Data Analysts by Median Salary')
ax[0].set_xlabel('')
ax[0].set_ylabel('')
ax[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, p: f'${int(x/1000)}K'))

sns.barplot(data=df_da_skills, y=df_da_skills.index, x='median', ax=ax[1], hue='median', palette='dark:b_r')
ax[1].legend().remove()
#df_da_skills.plot(kind='barh', ax=ax[1], legend=False)
#ax[1].invert_yaxis()
ax[1].set_title('Top 10 most in-demand Skills for Data Analysts')
ax[1].set_xlabel('Medain Salary(USD)')
ax[1].set_ylabel('')
ax[1].set_xlim(ax[0].get_xlim())
ax[1].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, p: f'${int(x/1000)}K'))
#plt.tight_layout()
fig.tight_layout()
plt.show()

'''
![The highest paid & most in-demand skills for data analysts in the US](3_project\images\most in_demand skills and paid skills output.png)
*Two separate bar graphs visualizing the highest paid skills and most in-demand skills for data analysts in the US*

#### Insights:
the top graph shows specialized technical skils like 'dplyr', 'bitbucket' and 'Gitlab' are associated with higher salaries, some reaching up to $200k, suggesting that advanced technical proficiency can increase earning potential.

the bottom graph highlights that foundational skills like 'Excel', 'Python', and 'SQL' are the most in-demand, even though they may not offer the highest salaries. this demonstrates the importance of these core skills for employability in data analysis roles.

there's a clear distinction between the skills that are highest paid and those that are the most in-demand. Data analysts aiming to maximise their career potential should consider developing a diverse skill set that includes both high-paying specialized skills and widely demanded foundational skills.

# The Analysis
## what is the most optimal skill to learn fro data analysts?
 methodology
 1. group skills to determine median salary and the likelihood of being in posting
 2. visualize median salary vs percent skill demand
 3. determine if certain technologies are more prevalent

## visualize data

'''python

sns.scatterplot(
    data=df_plot,
    x='skill_percent',
    y='median_salary',
    hue='technology' 
)

sns.despine()
sns.set_theme(style='ticks')

plt.tight_layout()
plt.show()

'''
#### Results

![most optimal skills for data analysts in the US](3_project\images\most optimal skill output.png)* Ascatterplot visualizing the most optimal skills (high paying & high demand) for data analysts in the US*

#### Insights:
the scatter plot shows the most of the 'programming' skills(colored blue) tend to cluster at higher salary levels compared to other categories, indicatinf that programming expertise might offer greater salary benefits within the data analytics field.

analyst tools(colored green), including tableau and power BI, are prevalent in Job Postings and offer competitive salaries, showing that visualization and data analysis software are crucial for current data roles. this category not only has good salaries but is also versatile across different types of data tasks.

the database skills(colored green), such as Oracle and SQL server, are associated ith some od the highest salaries among data analyst tools. this indicates a significant demand and valuation for data management and manipulation expertise in this industry.