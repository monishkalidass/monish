
Overview

The FifaWorldCup2022 database is designed to store and analyze match statistics from the 2022 FIFA World Cup. It includes detailed information about matches, team performance, player contributions, and match-specific metrics.



-- Create a new database
CREATE DATABASE FifaWorldCup2022;
CREATE TABLE MatchStatistics (
    Sl_No INT PRIMARY KEY,
    Match_No INT,
    Team VARCHAR(50),
    Against VARCHAR(50),
    Group_Char CHAR(1),
    Goal INT,
    Possession_Percent INT,
    Inside_Penalty_Area INT,
    Outside_Penalty_Area INT,
    Assists INT,
    Total_Attempts INT,
    On_Target INT,
    Off_Target INT,
    Target_in_Penalty INT,
    Target_from_Outside INT,
    Left_Channel INT,
    Left_Inside_Channel INT,
    Central_Channel INT,
    Right_Inside_Channel INT,
    Right_Channel INT,
    Receptions_MD INT,
    Receptions_D INT,
    Attempted_Line_Breaks INT,
    Completed_Line_Breaks INT,
    Attempted_Defensive_Line_Breaks INT,
    Completed_Defensive_Line_Breaks INT,
    Yellow_Cards INT,
    Red_Cards INT,
    Fouls_Against INT,
    Offsides INT,
    Passes INT,
    Passes_Completed INT,
    Crosses INT,
    Crosses_Completed INT,
    Corners INT,
    Free_Kicks INT,
    Penalties_Scored INT,
    Pts INT
);
-- Example for inserting data (bulk import is recommended for large datasets)
BULK INSERT MatchStatistics
FROM "C:\Users\acer\Downloads\Fifa Worldcup 2022.csv"
WITH (
    FIRSTROW = 2, -- Skips the header row
    FIELDTERMINATOR = ',', -- Delimiter in the CSV file
    ROWTERMINATOR = '\n', -- End of row
    TABLOCK
);
SELECT TOP 10 * FROM MatchStatistics;
SELECT Team, SUM(Goal) AS TotalGoals
FROM MatchStatistics
GROUP BY Team
ORDER BY TotalGoals DESC;

SELECT Team, AVG(Possession_Percent) AS AvgPossession
FROM MatchStatistics
GROUP BY Team
ORDER BY AvgPossession DESC;

SELECT Group_Char, AVG(Goal) AS AvgGoals
FROM MatchStatistics
GROUP BY Group_Char;

SELECT Team, SUM(Pts) AS TotalPoints
FROM MatchStatistics
GROUP BY Team
ORDER BY TotalPoints DESC;

SELECT Match_No, Team, Against, SUM(Goal) AS TotalGoals
FROM MatchStatistics
GROUP BY Match_No, Team, Against
ORDER BY TotalGoals DESC;

SELECT Team, SUM(Assists) AS TotalAssists
FROM MatchStatistics
GROUP BY Team
ORDER BY TotalAssists DESC;

SELECT Team, COUNT(*) AS Wins
FROM MatchStatistics
WHERE Pts = 3
GROUP BY Team
ORDER BY Wins DESC;








