# Football-League-Team-Analysis
"The Top 5 European Football Leagues Analysis project uses data from Kaggle to examine the domestic football (soccer) leagues of the top 5 European countries. The data set does not include European competitions such as the UEFA Champions League and Europa League. The goal of this project is to analyze and understand various aspects of the domestic football leagues, including team performance, player statistics, and league trends."
Domestic football leagues in Europe are structured in a pyramid-like system, where teams are grouped into different tiers based on their level of skill and competitiveness. At the top of the pyramid is the first tier, also known as the top flight or the top division, which is where the best teams in the country compete against each other.
Below the top tier, there are usually one or two lower divisions, where teams that were relegated from the top tier, as well as teams that have not yet been promoted, compete against each other. The number of teams in each division varies from country to country, but it typically ranges from 20 to 24 teams.
In addition to these domestic leagues, there are also international competitions, such as the UEFA Champions League and the UEFA Europa League, which allow teams from different countries to compete against each other.



## Summary:
1- The data set includes information about the top 5 European football leagues from 2010-2011 to 2020-2021.

2- Some basic statistics and visualizations were generated to understand the distribution of various metrics among the teams.

3- The top teams in terms of offensive, defensive, and overall performance over the last 11 years were identified and compared.



## Data Preparation and Cleaning 
![Screenshot 2024-07-20 191017](https://github.com/user-attachments/assets/9c27c3c4-dd53-4a3d-9840-ffb3e629d171)

plotting a graph to show Number of Times Each Team Won the League
![Screenshot 2024-07-20 191058](https://github.com/user-attachments/assets/c55b9ef6-ba97-4b43-a382-482dceb25bee)

plotting a graph to check how many different league winners a single league has had during the years this will tell us how competative a competition is
![Screenshot 2024-07-20 191109](https://github.com/user-attachments/assets/a7349b65-cba7-49b8-a619-e8f8c4bec908)


Q1) Which are the top 10 teams with the best offensive performance among the league-winning teams over the last 11 years, when sorted on the basis of their offensive performance?
![Screenshot 2024-07-20 191123](https://github.com/user-attachments/assets/94b12782-b7e3-4fbe-8468-cc4c976b8db1)

Q2) Which are the top teams with the best defensive performance among the league-winning teams over the last 11 years, when sorted on the basis of their defensive performance?
![Screenshot 2024-07-20 191143](https://github.com/user-attachments/assets/a520c730-6d29-4a2f-8199-8684ae1417ac)

### Competitiveness Index Calculation
```python
# Competitiveness Index = Number of unique winners / Total seasons in the dataset for each league
competitiveness = winner_counts.copy()
competitiveness['competitiveness_index'] = competitiveness['squad'] / len(teams_df['season'].unique())
competitiveness.sort_values(by='competitiveness_index', ascending=False, inplace=True)
competitiveness.plot(kind='bar', x='competition', y='competitiveness_index',
                     title='Competitiveness Index of Each League', color='skyblue')
plt.ylabel('Competitiveness Index')
plt.show()
competitiveness
```
![7e880d72-076e-40ea-b7d6-daefa9dddb65](https://github.com/user-attachments/assets/66756e82-55e3-425e-bdb3-d265bfc2a33e)

### Trend Analysis for Goals Scored 
```python
# Displaying the grouped data for verification
goals_trend = teams_df.groupby(['season', 'competition']).agg({'goals_for': 'mean', 'goals_against': 'mean'}).reset_index()
print(goals_trend.head())  # Check first few rows of the grouped data

# Plotting Average Goals Scored per Season
sns.lineplot(data=goals_trend, x='season', y='goals_for', hue='competition', marker='o')
plt.title('Average Goals Scored per Season by League')
plt.ylabel('Average Goals Scored')
plt.xlabel('Season')
plt.xticks(rotation=45)
plt.legend(title='League', bbox_to_anchor=(1.05, 1), loc='upper left')
plt.show()
```
![ce7f0246-5ab6-49a3-af98-bfc1b1545ead](https://github.com/user-attachments/assets/dafbd44b-02a2-4aa6-b432-06f9e1514344)




