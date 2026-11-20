# IPL-SQL-Analytics
## Project Overview 
This project analyzes Indian Premier League (IPL) data using SQL to uncover insights about teams, players, venues, and match outcomes. 
## Dataset 
Source: Kaggle IPL Dataset 
## Tools Used 
- SQL
- MySQL
- GitHub 
## Analysis Performed 
Problem Statement 1. Total number of matches played?
SQL Query:

SELECT COUNT(id) as No_of_matches_played
from matches;

Result:
<img width="652" height="145" alt="Screenshot 2026-11-20 140003" src="https://github.com/user-attachments/assets/1de76002-2de2-4961-9f20-304ab0c44065" />


Problem Statement 2: How many teams participated?
SQL Query:

SELECT COUNT(DISTINCT team) AS No_of_Teams_Played
FROM (
    SELECT team1 AS team
    FROM matches
    
    UNION
    
    SELECT team2 AS team
    FROM matches
) AS teams;

Result:
<img width="652" height="145" alt="image" src="https://github.com/user-attachments/assets/34e73cf4-0860-4ee0-81cf-6b8ec55a593f" />

Problem Statement 3: 3. Which team played the most matches?

SQL Query:
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

Result:
<img width="752" height="107" alt="image" src="https://github.com/user-attachments/assets/1c3584e8-b286-4927-ab0a-2c381d0d460c" />


Problem Statement 4: Which venue hosted the most matches?

SQL Query:
SELECT city, COUNT(city) as city_hosted_most_matches
from matches
group by city 
Order by COUNT(city) Desc
Limit 1;

Result:
<img width="787" height="108" alt="image" src="https://github.com/user-attachments/assets/a9de5087-2ea9-4fdb-bc99-f7da9b724132" />

Problem Statement 5: How many matches were played each season?

SQL Query:

Result:

   
8. Which team won the most matches?
9. Which team has the highest win percentage?
10. What is the average first innings score?
11. Which venue produces the highest scores?
12. Which toss decision is more successful?
13. Team-wise home ground performance.
14. Most successful captain.
15. Rank teams by total wins.
16. Top 5 run scorers by season.
17. Top wicket takers by season.
18. Highest successful run chase.
19. Calculate win percentage for every team.
## Project Structure 
- Dataset files
- SQL queries
- Screenshots of results
- Documentation 
## Author : Leena Bitoni

## Markdown
sh

