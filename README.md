# IPL-SQL-Analytics
## Project Overview 
This project analyzes Indian Premier League (IPL) data using SQL to uncover insights about teams, players, venues, and match outcomes. 
## Dataset 
Source: Kaggle IPL Dataset 
## Tools Used 
- SQL
- MySQL
- GitHub
## Skills Demonstrated

- SQL Queries
- Aggregate Functions
- Joins
- Common Table Expressions (CTEs)
- Subqueries
- Data Analysis
- Sports Analytics
- MySQL
- Git & GitHub

## Analysis Performed 
# Problem Statement 1. Total number of matches played?

## SQL Query:

SELECT COUNT(id) as No_of_matches_played
from matches;

## Result:
<img width="652" height="145" alt="Screenshot 2026-11-20 140003" src="https://github.com/user-attachments/assets/1de76002-2de2-4961-9f20-304ab0c44065" />


# Problem Statement 2: How many teams participated?

## SQL Query:

SELECT COUNT(DISTINCT team) AS No_of_Teams_Played
FROM (
    SELECT team1 AS team
    FROM matches
    
    UNION
    
    SELECT team2 AS team
    FROM matches
) AS teams;

## Result:
<img width="652" height="145" alt="image" src="https://github.com/user-attachments/assets/34e73cf4-0860-4ee0-81cf-6b8ec55a593f" />

# Problem Statement 3: Which team played the most matches?

## SQL Query:

SELECT team,
       COUNT(*) AS matches_played
FROM (
    SELECT team1 AS team
    FROM matches
    UNION ALL
    SELECT team2 AS team
    FROM matches
) AS teams
GROUP BY team
ORDER BY matches_played DESC
LIMIT 1;

## Result:
<img width="752" height="107" alt="image" src="https://github.com/user-attachments/assets/1c3584e8-b286-4927-ab0a-2c381d0d460c" />


# Problem Statement 4: Which venue hosted the most matches?

## SQL Query:

SELECT city, COUNT(city) as city_hosted_most_matches
from matches
group by city 
Order by COUNT(city) Desc
Limit 1;

## Result:
<img width="787" height="108" alt="image" src="https://github.com/user-attachments/assets/a9de5087-2ea9-4fdb-bc99-f7da9b724132" />

# Problem Statement 5: How many matches were played each season?

## SQL Query:

select season, count(id) as matches_played_each_season
from matches
group by season;

## Result:
<img width="637" height="280" alt="image" src="https://github.com/user-attachments/assets/91cae2e9-cc88-4fa3-83cf-dea1d04608e4" />

   
# Problem Statement 6: Which team won the most matches?

## SQL Query: 

SELECT winner,
       COUNT(*) AS matches_won
FROM matches
WHERE winner IS NOT NULL
GROUP BY winner
ORDER BY matches_won DESC
LIMIT 1;

## Result:
<img width="781" height="106" alt="image" src="https://github.com/user-attachments/assets/2efb888f-ef9c-49ee-8ad8-8661a55ecbff" />


# Problem Statement 7: Which team has the highest win percentage?

## SQL Query:

With team_total_matches as (
	Select team1 as team 
    from matches
    Union All
    Select team2 as team 
    from matches
    ),
    matches_played as (
		Select team, Count(*) as played
        from team_total_matches
        Group by team
        ),
	matches_won as (
		Select winner as team, Count(*) as won
        from matches
        where winner is not null
        Group by winner
        )
SELECT
    mp.team,
    mp.played,
    COALESCE(mw.won, 0) AS won,
    ROUND(
        COALESCE(mw.won, 0) * 100.0 / mp.played,
        2
    ) AS win_percentage
FROM matches_played mp
LEFT JOIN matches_won mw
    ON mp.team = mw.team
ORDER BY win_percentage DESC
limit 1;

## Result:
<img width="577" height="103" alt="image" src="https://github.com/user-attachments/assets/b101308f-fe29-489e-bcfb-25da92226c6b" />


# Problem Statement 8: Which toss decision is more successful?

## SQL Query:

SELECT
    toss_decision,
    COUNT(*) AS total_matches,
    SUM(CASE WHEN toss_winner = winner THEN 1 ELSE 0 END) AS wins_after_winning_toss,
    ROUND(
        SUM(CASE WHEN toss_winner = winner THEN 1 ELSE 0 END) * 100.0
        / COUNT(*),
        2
    ) AS success_rate
FROM matches
GROUP BY toss_decision
ORDER BY success_rate DESC;

## Result:
<img width="632" height="122" alt="image" src="https://github.com/user-attachments/assets/90cf3083-896a-4c61-b2bf-7bd842312988" />

## Project Structure 

- Dataset: IPL matches datasets from Kaggle.
- SQL Queries: Contains analytical SQL queries used to extract insights.
- README.md: Project overview, business questions, SQL solutions, and key findings.
- Screenshots: Query outputs and visual results for reference

## Key Insights

• Mumbai Indians have won the most matches.
• Fielding first is the more successful toss strategy.
• High-scoring venues favor chasing teams.
• Win percentage varies significantly across franchises.

## Author : Leena Bitoni
- GitHub: https://github.com/Linabitoni
- LinkedIn: https://www.linkedin.com/in/lina-bitoni-392471104/



