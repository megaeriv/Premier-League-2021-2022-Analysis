# Introduction 

The Premier League is one of the top five football leagues in the world, it is arguably the most competitive football league with the most talented teams and managers. 
It is the Top Tier league in the UK featuring arguably the Greatest Player of All Time in Cristiano Ronaldo.

This project contains a case study, analysis and visualization of the just concluded Premier League season (2021/2022) to identify and categorize players and teams in terms of attacking strength.

# Content

1. Aim

2. Data Sourcing

3. Data Cleaning

4. Exploratory Data Analysis

5. Data Visualization

6. Conclusion

# Aim

The aim of this project is to get valuable and meaningful insight into players and their rank in terms of attacking strength.

# Resources
Dataset used was sourced from Kaggle, Football Players Stats (Premier League 2021-2022)

It is organised as long data with the statistics of every player of football clubs present in the 2021/2022 premier league season. It contains 30 columns with 691 rows

Columns include:

Player: Player’s name

Team: Played club in 2021-2020

Nation: Player’s nation

Pos: Position

Age: Player’s age

MP: Matches played

Starts: Matches started

Min: Minutes played

90s: Minutes played divided by 90

Gls: Goals scored 

Ast: Assists

G-PK: Non-Penalty Goals

PK: Penalty Kicks made

PKatt: Penalty Kicks attended

CrdY: Yellow Cards

CrdR: Red Cards

Gls: Goals scored per 90 mins

Ast: Assists per 90 mins

G+A: Goals and Assists per 90 mins

G-PK: Goals minus Penalty Kicks made per 90 mins

G+A-PK: Goals plus Assists minus Penalty Kicks made per 90 mins

xG: Expected Goals (Probability of a goal being scored from a shot taken)

npxG: Non-Penalty Expected Goals

xA: Expected Assists (Probability of a goal being scored from the last pass given before a shot )

npxG+xA: Non-Penalty Expected Goals plus Expected Assists

xG: Expected Goals per 90 mins

npxG: Non-Penalty Expected Goals made per 90 mins

xA: Expected Assists made per 90 mins

npxG+xA: Non-Penalty Expected Goals plus Expected Assists made per 90 mins

Analysis was done with the R programming language, on R studio for analysis and visualisation, and Power BI was also used for visualization.

Packages used for Analysis:
ggpubr, tidyverse, here, skimr, janitor, lubridate, ggrepel, readxl, ggplot2

# Data Cleaning
After downloading the data from Kaggle, I needed to clean the data to perform an Exploratory data analysis. First, i checked for missing data and discovered there were some missing data and found, this was due to players registered in the league who never played a minute of football, I filltered them out. 
I renamed 12 columns to make them more comprehensible.



# Exploratory Data Analysis

To reduce bias statistically, only players with a minimum of 5 full matches (90 Minutes) played were analysed.

For various categorical values, I examined the distribution of the data and value counts. As a result of analysing the data with R, I grouped some columns in order to get an insight into the data and visualize it

Analysis on 

1. Goal-scored rank

2. Assist Rank

3. Most productive Players, this totals goals and assists

4. Grouped xG per 90 and xA per 90 to determine most threatening players in the league

5. Grouped Goals scored and Overall xG accumulated to determine the finishing strength of the Players with the most xG accumulated. Scoring more goals than calculated expected goals would mean overperforming and scoring less is underperforming.

# Data Visualization

In addition to exploring the data, I visualized it in R studio using R, as well as in Power BI. Here is the full project you can check out [Premier league 2021-2022](https://github.com/megaeriv/Premier-League-2021-2022-Analysis/blob/main/Premier-League-2021-2022-Analysis.md)
.

Power BI
![Screenshot 2022-10-10 170013](https://user-images.githubusercontent.com/111463558/195707045-0dfae290-6659-470d-9636-a15527e9de5f.png)


R studio:
![Finishing Level R ](https://user-images.githubusercontent.com/111463558/195707253-636c7ccd-a2c3-42b3-a404-243a062c8dd3.png)


# Insight

- Mohammed Salah ranked as the joint highest goal scorer with Son Heung min and accumulated the most assist, placing him as the most productive and threatening player in the league for the season.
This ranking can also be corroborated by the Threatening player’s graph of expected assists per 90 against expected goals per 90, he is positioned at the upper right corner of the graph.

He was evidently the most complete player in the league

- Son Heung min is world-class, ranked as the joint highest goal scorer but also the best finisher in the league. He scored more goals than his accumulated xG to a great extent making him even more of an elite finisher than his joint-top scorer Mohammed Salah.

-  Harry Kane, from his position in the Threatening players visual, it can be suggested he is the 2nd most threatening player in the league, yet he is classified as a poor finisher which is not commonly associated with the player. 
