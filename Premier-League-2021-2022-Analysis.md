Premier League Analysis 2021/2022 with R
================
Mega
2022-10-13

Summary

The Premier League is one of the top five football leagues in the world,
it is arguably the most competitive football league with the most
talented teams and managers.

1.Aim

What is the problem I am trying to solve? • I am looking to find out the
statistically best players and teams in the league. How can these
insights drive decisions?

Deliverable • Use stats to define the best player, best young best team
and best player per country in the league.

2.Prepare

2.1 Dataset Used Data was downloaded from Kaggle, Football Players Stats
(Premier League 2021-2022)

2.2 Information and Organisation It is organised as long data with the
statistics of every player of football clubs present in the 2021/2022
premier league season. It contains 30 columns with 691 rows.

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

Gls: Goals scored or allowed

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

xG: Expected Goals

npxG: Non-Penalty Expected Goals

xA: Expected Assists

npxG+xA: Non-Penalty Expected Goals plus Expected Assists

xG: Expected Goals per 90 mins

npxG: Non-Penalty Expected Goals made per 90 mins

xA: Expected Assists made per 90 mins

npxG+xA: Non-Penalty Expected Goals plus Expected Assists made per 90
mins

2.3 Credibility

•Reliable: Data can be considered reliable considering the source and
the acknowledgements of the data. •Original: The dataset is not original
as it was collated from another source, so it’s a secondary source.
•Comprehensive: The data is comprehensible enough as there are some
duplicated column names however with different records in them.
•Current: Data was last updated 2 months ago; it is therefore considered
current. •Cited: Data is not well cited. From the above to test the
credibility of the dataset, with the data not being cited and original,
analysis of the data would purely be operational, and any insights drawn
would be definitive from the data

2.4 Verification

Using excel filter and sort functions, I was able to verify attributes
and observations of the data.

3 Process

3.1 Installing Packages Packages to be used for Analysis

``` r
library(ggpubr)
```

    ## Loading required package: ggplot2

``` r
library(tidyverse)
```

    ## ── Attaching packages
    ## ───────────────────────────────────────
    ## tidyverse 1.3.2 ──

    ## ✔ tibble  3.1.7     ✔ dplyr   1.0.9
    ## ✔ tidyr   1.2.0     ✔ stringr 1.4.0
    ## ✔ readr   2.1.2     ✔ forcats 0.5.1
    ## ✔ purrr   0.3.4     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(here)
```

    ## here() starts at C:/Users/megae/Documents/Personal Data Analysis/Premier-League-2021-2022-Analysis

``` r
library(skimr)
library(janitor)
```

    ## 
    ## Attaching package: 'janitor'
    ## 
    ## The following objects are masked from 'package:stats':
    ## 
    ##     chisq.test, fisher.test

``` r
library(lubridate)
```

    ## 
    ## Attaching package: 'lubridate'
    ## 
    ## The following objects are masked from 'package:base':
    ## 
    ##     date, intersect, setdiff, union

``` r
library(ggrepel)
library(readr)
library(readxl)
library(ggplot2)
```

3.2 Importing Datasets The Premier league 2021/2022 data was imported
using r studio files

``` r
Football_Players_Stats_Premier_League_2021_2022_ <- read_excel("C:/Users/megae/Documents/Personal Data Analysis/Premier League Analysis/Football Players Stats (Premier League 2021-2022).xlsx")
```

    ## New names:
    ## • `Gls` -> `Gls...10`
    ## • `Ast` -> `Ast...11`
    ## • `G-PK` -> `G-PK...12`
    ## • `Gls` -> `Gls...17`
    ## • `Ast` -> `Ast...18`
    ## • `G-PK` -> `G-PK...20`
    ## • `xG` -> `xG...22`
    ## • `npxG` -> `npxG...23`
    ## • `xA` -> `xA...24`
    ## • `npxG+xA` -> `npxG+xA...25`
    ## • `xG` -> `xG...26`
    ## • `xA` -> `xA...27`
    ## • `npxG` -> `npxG...29`
    ## • `npxG+xA` -> `npxG+xA...30`

3.3 Preview Dataset We would use “head” and “str” functions to preview
our data. The view function can also be used to view the entire table as
analysis goes on

``` r
head(Football_Players_Stats_Premier_League_2021_2022_ )
```

    ## # A tibble: 6 × 30
    ##   Player     Team  Nation Pos     Age    MP Starts   Min `90s` Gls...10 Ast...11
    ##   <chr>      <chr> <chr>  <chr> <dbl> <dbl>  <dbl> <dbl> <dbl>    <dbl>    <dbl>
    ## 1 Bukayo Sa… Arse… eng E… FW,MF    19    38     36  2978  33.1       11        7
    ## 2 Gabriel D… Arse… br BRA DF       23    35     35  3063  34          5        0
    ## 3 Aaron Ram… Arse… eng E… GK       23    34     34  3060  34          0        0
    ## 4 Ben White  Arse… eng E… DF       23    32     32  2880  32          0        0
    ## 5 Martin Ød… Arse… no NOR MF       22    36     32  2785  30.9        7        4
    ## 6 Granit Xh… Arse… ch SUI MF,DF    28    27     27  2327  25.9        1        2
    ## # … with 19 more variables: `G-PK...12` <dbl>, PK <dbl>, PKatt <dbl>,
    ## #   CrdY <dbl>, CrdR <dbl>, Gls...17 <dbl>, Ast...18 <dbl>, `G+A` <dbl>,
    ## #   `G-PK...20` <dbl>, `G+A-PK` <dbl>, xG...22 <dbl>, npxG...23 <dbl>,
    ## #   xA...24 <dbl>, `npxG+xA...25` <dbl>, xG...26 <dbl>, xA...27 <dbl>,
    ## #   `xG+xA` <dbl>, npxG...29 <dbl>, `npxG+xA...30` <dbl>

3.4 Cleaning Here we would look to check for errors and correct them,
this is the cleaning and formatting section

3.4.1 Change column Names To be more comprehensible, column names
representing Xg per 90 and overall Xg would need to be changed as
columns just read as “Xg” and “xG.90”. This applies to xA also.

A total of 12 columns would need to be changed to ensure data is
comprehensible by the reader or another analyst

``` r
Football_Players_Stats_Premier_League_2021_2022_  <- Football_Players_Stats_Premier_League_2021_2022_  %>%
  rename(Played_90s = `90s`,
         Gls = Gls...10,
         Ast = Ast...11,
         npg = `G-PK...12`,
         `Gls/90` = Gls...17,
         `Ast/90` = Ast...18,
         `(G+A)/90` = `G+A`,
         `npG/90` = `G-PK...20`,
         `(npG+A)/90` = `G+A-PK`,
         xG = xG...22,
         npxG = npxG...23,
         xA = xA...24,
         `npxG+xA` = `npxG+xA...25`,
         `xG/90` = xG...26,
         `xA/90` = xA...27,
         `(xG+xA)/90`=`xG+xA`,
         `npxG/90` =  npxG...29,
         `(npxG+xA)/90` = `npxG+xA...30`)

  
head(Football_Players_Stats_Premier_League_2021_2022_)
```

    ## # A tibble: 6 × 30
    ##   Player      Team  Nation Pos     Age    MP Starts   Min Played_90s   Gls   Ast
    ##   <chr>       <chr> <chr>  <chr> <dbl> <dbl>  <dbl> <dbl>      <dbl> <dbl> <dbl>
    ## 1 Bukayo Saka Arse… eng E… FW,MF    19    38     36  2978       33.1    11     7
    ## 2 Gabriel Do… Arse… br BRA DF       23    35     35  3063       34       5     0
    ## 3 Aaron Rams… Arse… eng E… GK       23    34     34  3060       34       0     0
    ## 4 Ben White   Arse… eng E… DF       23    32     32  2880       32       0     0
    ## 5 Martin Øde… Arse… no NOR MF       22    36     32  2785       30.9     7     4
    ## 6 Granit Xha… Arse… ch SUI MF,DF    28    27     27  2327       25.9     1     2
    ## # … with 19 more variables: npg <dbl>, PK <dbl>, PKatt <dbl>, CrdY <dbl>,
    ## #   CrdR <dbl>, `Gls/90` <dbl>, `Ast/90` <dbl>, `(G+A)/90` <dbl>,
    ## #   `npG/90` <dbl>, `(npG+A)/90` <dbl>, xG <dbl>, npxG <dbl>, xA <dbl>,
    ## #   `npxG+xA` <dbl>, `xG/90` <dbl>, `xA/90` <dbl>, `(xG+xA)/90` <dbl>,
    ## #   `npxG/90` <dbl>, `(npxG+xA)/90` <dbl>

Played_90s: total minutes/90, this is useful as it can aggregate the
number of games a player played even though they never started a game by
dividing all their minutes played by 90.

Gls:Goals

Ast: Assist

npG: Non-penalty goals

xG; Expected goals (chance of a player scoring a goal with a maximum
value of 1)

xA: Expected Assists(chance of a pass becoming the assist to a goal with
a maximum value of 1)

npxG:Non-penalty expected goals

Total_xG: Total expected goal in the season

3.4.2 Nation column The nations column contained strings like “eng <ao>
ENG”. the “str_sub” function was then used in addition to “mutate” to
create a new column of “Nationality” and then reordered

``` r
## reordering the Nationality column we created
Football_Players_Stats_Premier_League_2021_2022_  <- Football_Players_Stats_Premier_League_2021_2022_  %>%
  mutate(Nationality=str_sub(Nation,-3)) %>%
  relocate(Nationality, .after = Team) 
```

now to verify the number of players and attributes once again with
“head” and “str” functions

``` r
head(Football_Players_Stats_Premier_League_2021_2022_ )
```

    ## # A tibble: 6 × 31
    ##   Player      Team  Nationality Nation Pos     Age    MP Starts   Min Played_90s
    ##   <chr>       <chr> <chr>       <chr>  <chr> <dbl> <dbl>  <dbl> <dbl>      <dbl>
    ## 1 Bukayo Saka Arse… ENG         eng E… FW,MF    19    38     36  2978       33.1
    ## 2 Gabriel Do… Arse… BRA         br BRA DF       23    35     35  3063       34  
    ## 3 Aaron Rams… Arse… ENG         eng E… GK       23    34     34  3060       34  
    ## 4 Ben White   Arse… ENG         eng E… DF       23    32     32  2880       32  
    ## 5 Martin Øde… Arse… NOR         no NOR MF       22    36     32  2785       30.9
    ## 6 Granit Xha… Arse… SUI         ch SUI MF,DF    28    27     27  2327       25.9
    ## # … with 21 more variables: Gls <dbl>, Ast <dbl>, npg <dbl>, PK <dbl>,
    ## #   PKatt <dbl>, CrdY <dbl>, CrdR <dbl>, `Gls/90` <dbl>, `Ast/90` <dbl>,
    ## #   `(G+A)/90` <dbl>, `npG/90` <dbl>, `(npG+A)/90` <dbl>, xG <dbl>, npxG <dbl>,
    ## #   xA <dbl>, `npxG+xA` <dbl>, `xG/90` <dbl>, `xA/90` <dbl>,
    ## #   `(xG+xA)/90` <dbl>, `npxG/90` <dbl>, `(npxG+xA)/90` <dbl>

``` r
str(Football_Players_Stats_Premier_League_2021_2022_ )
```

    ## tibble [691 × 31] (S3: tbl_df/tbl/data.frame)
    ##  $ Player      : chr [1:691] "Bukayo Saka" "Gabriel Dos Santos" "Aaron Ramsdale" "Ben White" ...
    ##  $ Team        : chr [1:691] "Arsenal" "Arsenal" "Arsenal" "Arsenal" ...
    ##  $ Nationality : chr [1:691] "ENG" "BRA" "ENG" "ENG" ...
    ##  $ Nation      : chr [1:691] "eng ENG" "br BRA" "eng ENG" "eng ENG" ...
    ##  $ Pos         : chr [1:691] "FW,MF" "DF" "GK" "DF" ...
    ##  $ Age         : num [1:691] 19 23 23 23 22 28 28 24 21 20 ...
    ##  $ MP          : num [1:691] 38 35 34 32 36 27 24 22 33 29 ...
    ##  $ Starts      : num [1:691] 36 35 34 32 32 27 23 22 21 21 ...
    ##  $ Min         : num [1:691] 2978 3063 3060 2880 2785 ...
    ##  $ Played_90s  : num [1:691] 33.1 34 34 32 30.9 25.9 22.5 21.3 21.3 20.7 ...
    ##  $ Gls         : num [1:691] 11 5 0 0 7 1 2 1 10 6 ...
    ##  $ Ast         : num [1:691] 7 0 0 0 4 2 1 3 2 6 ...
    ##  $ npg         : num [1:691] 9 5 0 0 7 1 2 1 10 5 ...
    ##  $ PK          : num [1:691] 2 0 0 0 0 0 0 0 0 1 ...
    ##  $ PKatt       : num [1:691] 2 0 0 0 0 0 0 0 0 1 ...
    ##  $ CrdY        : num [1:691] 6 8 1 3 4 10 6 0 1 3 ...
    ##  $ CrdR        : num [1:691] 0 1 0 0 0 1 0 0 0 1 ...
    ##  $ Gls/90      : num [1:691] 0.33 0.15 0 0 0.23 0.04 0.09 0.05 0.47 0.29 ...
    ##  $ Ast/90      : num [1:691] 0.21 0 0 0 0.13 0.08 0.04 0.14 0.09 0.29 ...
    ##  $ (G+A)/90    : num [1:691] 0.54 0.15 0 0 0.36 0.12 0.13 0.19 0.56 0.58 ...
    ##  $ npG/90      : num [1:691] 0.27 0.15 0 0 0.23 0.04 0.09 0.05 0.47 0.24 ...
    ##  $ (npG+A)/90  : num [1:691] 0.48 0.15 0 0 0.36 0.12 0.13 0.19 0.56 0.53 ...
    ##  $ xG          : num [1:691] 9.7 2.7 0 1 4.8 1.2 2.5 0.7 5.8 7.2 ...
    ##  $ npxG        : num [1:691] 8.2 2.7 0 1 4.8 1.2 2.5 0.7 5.8 6.5 ...
    ##  $ xA          : num [1:691] 6.9 0.8 0 0.6 6.8 2.3 1.3 1.9 2.2 3.3 ...
    ##  $ npxG+xA     : num [1:691] 15.2 3.5 0 1.6 11.6 3.5 3.8 2.6 8 9.8 ...
    ##  $ xG/90       : num [1:691] 0.29 0.08 0 0.03 0.16 0.05 0.11 0.03 0.27 0.35 ...
    ##  $ xA/90       : num [1:691] 0.21 0.02 0 0.02 0.22 0.09 0.06 0.09 0.1 0.16 ...
    ##  $ (xG+xA)/90  : num [1:691] 0.5 0.1 0 0.05 0.38 0.14 0.17 0.12 0.37 0.51 ...
    ##  $ npxG/90     : num [1:691] 0.25 0.08 0 0.03 0.16 0.05 0.11 0.03 0.27 0.31 ...
    ##  $ (npxG+xA)/90: num [1:691] 0.46 0.1 0 0.05 0.38 0.14 0.17 0.12 0.37 0.47 ...

3.4.3 Name Change

changing the name of “Ikay Gundogan”, which reads as “?kay Gundogan”

``` r
Football_Players_Stats_Premier_League_2021_2022_$Player[398] = "Ikay Gundogan" 

view(Football_Players_Stats_Premier_League_2021_2022_)
```

3.4.4 Duplicates Now to check for duplicates in the dataset

``` r
sum(duplicated(Football_Players_Stats_Premier_League_2021_2022_ ))
```

    ## [1] 0

Results show no duplicates in data.

Export data frame to be used for later using code “write.csv(data
frame,”path”,row.names = FALSE)”

4.  Analyse Data In this section, we would be carrying out various
    analyses of the data to determine attacking threats of players and
    teams, creative strength of players and teams and aggressiveness of
    players and teams.

Analysis to be carried out: 1. Highest goal scorers 2. Highest assists
3. Most productive players (G+A) 4. Highest scoring defenders (G) 5.
Most dangerous players (players with the highest xG/90) 6. Most creative
players (players with the highest xA/90) 7. Best attacker i. Best
attacker per team ii. Best attacker per country 8. Best young attacker
9. Best attacking team (open play (npxG+xA)/90) minutes played 10. Elite
scores (Players exceeding their xG) 11. Players, xA and xG

However, any analysis of statistics would need to consider the number of
minutes players played to reduce bias, therefore only players with a
minimum of 5 90 minutes played (Played_90s)

\#Filtering data the filter function was first used to filter out
players who did not play a single match and then players who had less
than 5 90 minutes played.

``` r
football_played_stats <- Football_Players_Stats_Premier_League_2021_2022_  %>%
  filter(Starts > 0)

view(football_played_stats)


football_stats <- football_played_stats %>%
  filter(Played_90s > 5)

head(football_stats)
```

    ## # A tibble: 6 × 31
    ##   Player      Team  Nationality Nation Pos     Age    MP Starts   Min Played_90s
    ##   <chr>       <chr> <chr>       <chr>  <chr> <dbl> <dbl>  <dbl> <dbl>      <dbl>
    ## 1 Bukayo Saka Arse… ENG         eng E… FW,MF    19    38     36  2978       33.1
    ## 2 Gabriel Do… Arse… BRA         br BRA DF       23    35     35  3063       34  
    ## 3 Aaron Rams… Arse… ENG         eng E… GK       23    34     34  3060       34  
    ## 4 Ben White   Arse… ENG         eng E… DF       23    32     32  2880       32  
    ## 5 Martin Øde… Arse… NOR         no NOR MF       22    36     32  2785       30.9
    ## 6 Granit Xha… Arse… SUI         ch SUI MF,DF    28    27     27  2327       25.9
    ## # … with 21 more variables: Gls <dbl>, Ast <dbl>, npg <dbl>, PK <dbl>,
    ## #   PKatt <dbl>, CrdY <dbl>, CrdR <dbl>, `Gls/90` <dbl>, `Ast/90` <dbl>,
    ## #   `(G+A)/90` <dbl>, `npG/90` <dbl>, `(npG+A)/90` <dbl>, xG <dbl>, npxG <dbl>,
    ## #   xA <dbl>, `npxG+xA` <dbl>, `xG/90` <dbl>, `xA/90` <dbl>,
    ## #   `(xG+xA)/90` <dbl>, `npxG/90` <dbl>, `(npxG+xA)/90` <dbl>

4.1 Highest goal scorers We would analyse all players depending on the
number of goals they scored. \#Top scorers data frame was created and
filtered to only show the top 25 players

``` r
Top_scorers <- football_stats %>%
  select(Player, Team, Pos, Played_90s, Gls  ) %>%
  arrange(desc(Gls)) %>%
  slice(1:25)
  
  
head(Top_scorers)
```

    ## # A tibble: 6 × 5
    ##   Player            Team              Pos   Played_90s   Gls
    ##   <chr>             <chr>             <chr>      <dbl> <dbl>
    ## 1 Mohamed Salah     Liverpool         FW          30.7    23
    ## 2 Son Heung-min     Tottenham Hotspur FW,MF       33.4    23
    ## 3 Cristiano Ronaldo Manchester United FW          27.3    18
    ## 4 Harry Kane        Tottenham Hotspur FW          35.9    17
    ## 5 Sadio Mané        Liverpool         FW          31.3    16
    ## 6 Jamie Vardy       Leicester City    FW          20.1    15

4.2 Highest Assists We would analyse all players depending on the number
of goals they assisted.

\#Top creators data frame was created and filtered to only show the top
25 players

``` r
Top_creators <- football_stats %>%
  select(Player, Team, Pos, Played_90s, Ast  ) %>%
  arrange(desc(Ast)) %>%
  slice(1:25)
  
  
head(Top_creators)
```

    ## # A tibble: 6 × 5
    ##   Player                 Team            Pos   Played_90s   Ast
    ##   <chr>                  <chr>           <chr>      <dbl> <dbl>
    ## 1 Mohamed Salah          Liverpool       FW          30.7    13
    ## 2 Trent Alexander-Arnold Liverpool       DF          31.7    12
    ## 3 Mason Mount            Chelsea         MF,FW       26.3    10
    ## 4 Harvey Barnes          Leicester City  FW,MF       23.3    10
    ## 5 Andrew Robertson       Liverpool       DF          28.2    10
    ## 6 Jarrod Bowen           West Ham United FW          33.1    10

4.3 Most Productive players Most productive players would be determined
by the combination of goals and assists in the league

\#We would also filter out to the top 35 most productive players in the
league

``` r
Top_productive <- football_stats %>%
  select(Player, Team, Pos, Played_90s, Gls, Ast) %>%
  mutate(Gls_Ast=Gls+Ast) %>%
  arrange(desc(Gls_Ast)) %>%
  slice(1:35)

head(Top_productive)
```

    ## # A tibble: 6 × 7
    ##   Player          Team              Pos   Played_90s   Gls   Ast Gls_Ast
    ##   <chr>           <chr>             <chr>      <dbl> <dbl> <dbl>   <dbl>
    ## 1 Mohamed Salah   Liverpool         FW          30.7    23    13      36
    ## 2 Son Heung-min   Tottenham Hotspur FW,MF       33.4    23     7      30
    ## 3 Harry Kane      Tottenham Hotspur FW          35.9    17     9      26
    ## 4 Kevin De Bruyne Manchester City   MF          24.5    15     8      23
    ## 5 Jarrod Bowen    West Ham United   FW          33.1    12    10      22
    ## 6 Mason Mount     Chelsea           MF,FW       26.3    11    10      21

4.4 Most Productive defenders

Top goal contributing defenders would be determined using both goals and
assists.

``` r
Top_productive_defenders <- football_stats %>%
  select(Player, Team, Pos, Played_90s, Gls, Ast) %>%
  filter(Pos=='DF') %>%
  mutate(Gls_Ast=Gls+Ast) %>%
  arrange(desc(Gls_Ast)) %>%
  slice(1:20)

head(Top_productive_defenders)
```

    ## # A tibble: 6 × 7
    ##   Player                 Team            Pos   Played_90s   Gls   Ast Gls_Ast
    ##   <chr>                  <chr>           <chr>      <dbl> <dbl> <dbl>   <dbl>
    ## 1 Reece James            Chelsea         DF          20.7     5     9      14
    ## 2 Trent Alexander-Arnold Liverpool       DF          31.7     2    12      14
    ## 3 Andrew Robertson       Liverpool       DF          28.2     3    10      13
    ## 4 Marcos Alonso          Chelsea         DF          24.1     4     4       8
    ## 5 João Cancelo           Manchester City DF          35.9     1     7       8
    ## 6 Matty Cash             Aston Villa     DF          37.5     4     3       7

4.5 Most productive players per 90 Normalizing for time played is the
only way to accurately compare statistics between different players. we
would then use the Gls/90, Ast/90 to determine the productivity of
players per 90 mins played and not just overall. (All goals would be
used including penalty goals)

With this, we can compare both data set insights of the most productive
players and most productive players per 90. this brings consistency into
the equation and further context into understanding the better players.

``` r
Top_productive_per90 <- football_stats %>%
  select(Player, Team, Pos, Played_90s, `Gls/90`, `Ast/90`, `(G+A)/90`) %>%
  arrange(desc(`(G+A)/90`)) %>%
  slice(1:35)

head(Top_productive_per90)
```

    ## # A tibble: 6 × 7
    ##   Player           Team            Pos   Played_90s `Gls/90` `Ast/90` `(G+A)/90`
    ##   <chr>            <chr>           <chr>      <dbl>    <dbl>    <dbl>      <dbl>
    ## 1 Mohamed Salah    Liverpool       FW          30.7     0.75     0.42       1.17
    ## 2 Riyad Mahrez     Manchester City FW          16.6     0.66     0.3        0.96
    ## 3 Kevin De Bruyne  Manchester City MF          24.5     0.61     0.33       0.94
    ## 4 Dejan Kulusevski Tottenham Hots… MF,FW       14       0.36     0.57       0.93
    ## 5 Son Heung-min    Tottenham Hots… FW,MF       33.4     0.69     0.21       0.9 
    ## 6 Jamie Vardy      Leicester City  FW          20.1     0.75     0.1        0.85

When analysing with stats/90, it tends to favour players with lesser
minutes. Therefore, to complement for this bias we would further filter
out players with less than 15 90 minutes played (played_90s). 15 is less
than half of the games in a season (38)

``` r
Top_productive_per90_final <- football_stats %>%
  select(Player, Team, Pos, Played_90s, `Gls/90`, `Ast/90`, `(G+A)/90`) %>%
  filter(Played_90s>15) %>%
  arrange(desc(`(G+A)/90`)) %>%
  slice(1:35)

head(Top_productive_per90_final)
```

    ## # A tibble: 6 × 7
    ##   Player          Team             Pos   Played_90s `Gls/90` `Ast/90` `(G+A)/90`
    ##   <chr>           <chr>            <chr>      <dbl>    <dbl>    <dbl>      <dbl>
    ## 1 Mohamed Salah   Liverpool        FW          30.7     0.75     0.42       1.17
    ## 2 Riyad Mahrez    Manchester City  FW          16.6     0.66     0.3        0.96
    ## 3 Kevin De Bruyne Manchester City  MF          24.5     0.61     0.33       0.94
    ## 4 Son Heung-min   Tottenham Hotsp… FW,MF       33.4     0.69     0.21       0.9 
    ## 5 Jamie Vardy     Leicester City   FW          20.1     0.75     0.1        0.85
    ## 6 Mason Mount     Chelsea          MF,FW       26.3     0.42     0.38       0.8

4.6 Most Dangerous players Mos dangerous players can be characterized by
players scoring the most goals, but over the years a new statistic has
been used, “xG”

This quantifies the quality of a shot based on different variables, a
player has a shot off and could score from an xG shot of
0.3(over-perform his xG) and not score from a n xG shot of
0.7(under-perform)

Same way xG characterizes the quality of a goal from a shot, the quality
of a goal resorting from a pass can also be qualified. this statistic is
called “xA”

with this, we could understand players that under-performed or
over-performed based on their accumulated xG and with xA to determine
players who create great chances for their teammates.

For this category, we would determine the best creators and scorers by
their overall xG and xA. later, we would include their xG and xA per 90
to determine the most productive alongside their consistency over the
season.

``` r
Top_xG_performers <- football_stats %>%
  select(Player,Team, Pos, Played_90s, xG, Gls)%>%
  mutate(`Gls-xG` = Gls - xG) %>%
  mutate(xG_Performance = case_when(
    (Gls-xG) > 0 ~ "Over-performed",
    (Gls-xG) < 0 ~ "Under-Performed",
    (Gls-xG) == 0 ~ "Just right"
  ) ) %>%
  arrange(desc(xG))%>%
  slice(1:35)


Top_xA_creators <- football_stats %>%
  select(Player,Team, Pos, Played_90s, xA, Ast)%>%
    mutate(xA_Performance = case_when(
    (Ast-xA) > 0 ~ "Over-performed",
    (Ast-xA) < 0 ~ "Under-Performed",
    (Ast-xA) == 0 ~ "Just right"
  ) ) %>%
  arrange(desc(xA))%>%
  slice(1:35)



head(Top_xG_performers)
```

    ## # A tibble: 6 × 8
    ##   Player            Team    Pos   Played_90s    xG   Gls `Gls-xG` xG_Performance
    ##   <chr>             <chr>   <chr>      <dbl> <dbl> <dbl>    <dbl> <chr>         
    ## 1 Mohamed Salah     Liverp… FW          30.7  21.8    23    1.2   Over-performed
    ## 2 Harry Kane        Totten… FW          35.9  20.1    17   -3.1   Under-Perform…
    ## 3 Sadio Mané        Liverp… FW          31.3  16.7    16   -0.700 Under-Perform…
    ## 4 Cristiano Ronaldo Manche… FW          27.3  16.5    18    1.5   Over-performed
    ## 5 Son Heung-min     Totten… FW,MF       33.4  16.4    23    6.6   Over-performed
    ## 6 Diogo Jota        Liverp… FW          26.3  16.1    15   -1.10  Under-Perform…

``` r
head(Top_xA_creators)
```

    ## # A tibble: 6 × 7
    ##   Player                 Team        Pos   Played_90s    xA   Ast xA_Performance
    ##   <chr>                  <chr>       <chr>      <dbl> <dbl> <dbl> <chr>         
    ## 1 Trent Alexander-Arnold Liverpool   DF          31.7  11.2    12 Over-performed
    ## 2 Mohamed Salah          Liverpool   FW          30.7  10.4    13 Over-performed
    ## 3 Kevin De Bruyne        Manchester… MF          24.5   9.5     8 Under-Perform…
    ## 4 Harry Kane             Tottenham … FW          35.9   9       9 Just right    
    ## 5 Bruno Fernandes        Manchester… MF          34.6   8.4     6 Under-Perform…
    ## 6 Son Heung-min          Tottenham … FW,MF       33.4   8.1     7 Under-Perform…

For checking of consistency of players in being productive per 90
minutes played, we would use xG and xA per 90

``` r
Top_xGxA_players_per90 <- football_stats %>%
 select(Player, Team, Pos, Played_90s, `xG/90`, `xA/90`,`(xG+xA)/90`)%>%
  filter(Played_90s > 15) %>%
  arrange(desc(`(xG+xA)/90`)) %>%
            slice(1:35)


head(Top_xGxA_players_per90)
```

    ## # A tibble: 6 × 7
    ##   Player          Team             Pos   Played_90s `xG/90` `xA/90` `(xG+xA)/90`
    ##   <chr>           <chr>            <chr>      <dbl>   <dbl>   <dbl>        <dbl>
    ## 1 Mohamed Salah   Liverpool        FW          30.7    0.71    0.34         1.05
    ## 2 Riyad Mahrez    Manchester City  FW          16.6    0.61    0.22         0.83
    ## 3 Diogo Jota      Liverpool        FW          26.3    0.61    0.21         0.82
    ## 4 Raheem Sterling Manchester City  FW          23.6    0.61    0.2          0.81
    ## 5 Harry Kane      Tottenham Hotsp… FW          35.9    0.56    0.25         0.81
    ## 6 Gabriel Jesus   Manchester City  FW          20.9    0.49    0.26         0.74

4.7 Dangerous players per Team and country

Here we would analyse the most dangerous player and young player per
team using aggregated Goals and assists.

``` r
Best_player_Team <- football_stats %>%
  select(Team, Player, Pos, Played_90s, Gls, Ast, )%>%
  mutate(Gls_Ast=Gls+Ast) %>%
  group_by(Team) %>%
  slice(1:3) %>%
  arrange(Team,desc (Gls_Ast))
  


Best_player_Country <- football_stats %>%
  select(Nationality, Player, Pos, Played_90s, Gls, Ast,) %>%
  mutate(Gls_Ast = Gls+Ast) %>%
  group_by(Nationality) %>%
  arrange(desc(Gls_Ast)) %>%
  slice(1) %>%
  arrange(desc(Gls_Ast)) 
  

  
head(Best_player_Team)
```

    ## # A tibble: 6 × 7
    ## # Groups:   Team [2]
    ##   Team        Player             Pos   Played_90s   Gls   Ast Gls_Ast
    ##   <chr>       <chr>              <chr>      <dbl> <dbl> <dbl>   <dbl>
    ## 1 Arsenal     Bukayo Saka        FW,MF       33.1    11     7      18
    ## 2 Arsenal     Gabriel Dos Santos DF          34       5     0       5
    ## 3 Arsenal     Aaron Ramsdale     GK          34       0     0       0
    ## 4 Aston Villa Matty Cash         DF          37.5     4     3       7
    ## 5 Aston Villa Tyrone Mings       DF          35.4     1     3       4
    ## 6 Aston Villa Emiliano Martínez  GK          36       0     0       0

``` r
head(Best_player_Country)
```

    ## # A tibble: 6 × 7
    ## # Groups:   Nationality [6]
    ##   Nationality Player            Pos   Played_90s   Gls   Ast Gls_Ast
    ##   <chr>       <chr>             <chr>      <dbl> <dbl> <dbl>   <dbl>
    ## 1 EGY         Mohamed Salah     FW          30.7    23    13      36
    ## 2 KOR         Son Heung-min     FW,MF       33.4    23     7      30
    ## 3 ENG         Harry Kane        FW          35.9    17     9      26
    ## 4 BEL         Kevin De Bruyne   MF          24.5    15     8      23
    ## 5 POR         Cristiano Ronaldo FW          27.3    18     3      21
    ## 6 JAM         Michail Antonio   FW          33      10     8      18

4.8 Best Young player We would look to identify the best young player
using xG and xA per 90 over the course of the season with more than 15
90 minutes played. Age would be set at under 21 (21 and below)

``` r
Best_young_player <- football_stats %>%
  select(Player, Age, Team, Pos, Played_90s, Gls,Ast, `(G+A)/90` ) %>%
  filter(Age < 22 ) %>%
  filter(Played_90s > 15) %>%
  arrange(desc(`(G+A)/90`)) %>%
  slice(1:10)

head(Best_young_player)
```

    ## # A tibble: 6 × 8
    ##   Player             Age Team            Pos   Played_90s   Gls   Ast `(G+A)/90`
    ##   <chr>            <dbl> <chr>           <chr>      <dbl> <dbl> <dbl>      <dbl>
    ## 1 Reece James         21 Chelsea         DF          20.7     5     9       0.68
    ## 2 Phil Foden          21 Manchester City FW          23.6     9     5       0.59
    ## 3 Martinelli          20 Arsenal         FW,MF       20.7     6     6       0.58
    ## 4 Emile Smith Rowe    21 Arsenal         MF,FW       21.3    10     2       0.56
    ## 5 Bukayo Saka         19 Arsenal         FW,MF       33.1    11     7       0.54
    ## 6 Conor Gallagher     21 Crystal Palace  MF          31.6     8     3       0.35

4.9 Best Attacking Team To calculate the best-attacking team, we would
aggregate the xg and as created per 90 minutes to establish the
best-attacking teams

``` r
Top_Attacking_Team <- football_stats %>%
  group_by(Team) %>%
  mutate(Total_xG = sum(xG))%>%
  mutate(xG_per_game = sum(xG/90)) %>%
  select(Team,Total_xG,xG_per_game) %>%
  slice(1) %>%
  arrange(desc(xG_per_game))


head(Top_Attacking_Team)
```

    ## # A tibble: 6 × 3
    ## # Groups:   Team [6]
    ##   Team              Total_xG xG_per_game
    ##   <chr>                <dbl>       <dbl>
    ## 1 Manchester City       88.1       0.979
    ## 2 Liverpool             86.4       0.96 
    ## 3 Chelsea               67.7       0.752
    ## 4 Tottenham Hotspur     65.3       0.726
    ## 5 Arsenal               60.7       0.674
    ## 6 Manchester United     52.7       0.586

5.0 Visualizations

through visualizations, we would like to determine the level of
finishers present in the league, the reliance of teams on a single
player, the best-attacking teams, the best player and t best young
player.

5.1 Level of Finishers

we would classify and visualize the level of finishing of players by
using the difference between goals scored and xG accumulated.

Elite - Players with \>1.5 (Goals - XG) Clinical - Players with
-0.5:+1.5 (Goals - XG) Average -Players with -1.5:-0.5 (Goals - XG)
Poor - Players with \<-1.5 (Goals - XG)

``` r
Finishing_Level <- Top_xG_performers %>%
  select(Player,Team, Pos, Played_90s, xG, Gls)%>%
  mutate(Gls_xG= Gls-xG) %>%
  mutate(Finishing = case_when(
    Gls_xG > 1.5 ~ "Elite",
    Gls_xG >= -0.5 & Gls_xG <= 1.5 ~ "Clinical",
    Gls_xG >= -1.5 & Gls_xG < -0.5 ~ "Average",
    Gls_xG < -1.5 ~ "Poor"
  )) %>%
  arrange(desc(Gls_xG))

head(Finishing_Level)
```

    ## # A tibble: 6 × 8
    ##   Player          Team             Pos   Played_90s    xG   Gls Gls_xG Finishing
    ##   <chr>           <chr>            <chr>      <dbl> <dbl> <dbl>  <dbl> <chr>    
    ## 1 Son Heung-min   Tottenham Hotsp… FW,MF       33.4  16.4    23    6.6 Elite    
    ## 2 Jamie Vardy     Leicester City   FW          20.1   9.5    15    5.5 Elite    
    ## 3 Wilfried Zaha   Crystal Palace   FW          30.7   9.4    14    4.6 Elite    
    ## 4 James Maddison  Leicester City   MF,FW       27.3   8.2    12    3.8 Elite    
    ## 5 Emmanuel Dennis Watford          FW,MF       28.7   7.5    10    2.5 Elite    
    ## 6 Mason Mount     Chelsea          MF,FW       26.3   8.9    11    2.1 Elite

To determine the level of finishing present in the premier league, we
would plot a pie chart to depict the level of finishing among the top 35
goal scorers in the league.

Firstly, a data frame with the percentage distribution of finishers
would be created.

``` r
Finishing_Level_percent <- Finishing_Level %>%
  group_by(Finishing) %>%
  summarise(total = n()) %>%
  mutate(Finishing_percent_total = total/sum(total))%>%
  group_by(Finishing) %>%
  mutate(labels = scales::percent(Finishing_percent_total)) %>%
  arrange(desc(Finishing_percent_total))

head(Finishing_Level_percent)
```

    ## # A tibble: 4 × 4
    ## # Groups:   Finishing [4]
    ##   Finishing total Finishing_percent_total labels
    ##   <chr>     <int>                   <dbl> <chr> 
    ## 1 Clinical     14                   0.4   40%   
    ## 2 Average       8                   0.229 23%   
    ## 3 Poor          7                   0.2   20%   
    ## 4 Elite         6                   0.171 17%

``` r
Finishing_Level_percent %>%
  ggplot(aes(x="",y=Finishing_percent_total, fill=Finishing)) +
  geom_bar(stat = "identity", width = 1)+
  coord_polar("y", start=0)+
  theme_minimal()+
  theme(axis.title.x= element_blank(),
        axis.title.y = element_blank(),
        panel.border = element_blank(), 
        panel.grid = element_blank(), 
        axis.ticks = element_blank(),
        axis.text.x = element_blank(),
        plot.title = element_text(hjust = 1, size=10, face = "bold")) +
  scale_fill_manual(values = c("#F0E442","#56B4E9", "#009E73", "#ff8080")) +
  geom_text(aes(label = labels),
            position = position_stack(vjust = 0.5))+
  labs(title="League Finishing Level Distribution")
```

![](Premier-League-2021-2022-Analysis_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

I as a fan of the premier league was shocked by the resulting visual as
I cannot count the number of times, I have had discussions with fans of
my clubs or other clubs about how some strikers are not clinical enough.

Therefore, Analytic bias should always be put into consideration when
analysing cause stats tell different stories when processed effectively

From the above visual, it shows the premier league is majorly filled
with clinical strikers when it comes to scoring from a shot according to
statistics. with elite-level finishers not so less than poor-level
finishers.

5.1.1 Finishing level per player

to visualize the level of finishing per player, the Goals - Expected
goals metric would be used here also but per player.

``` r
Finishing_Level %>%
  arrange(Gls_xG)%>%
  mutate(Player=factor(Player, levels = Player))%>%
 ggplot(aes(x=Player, y=Gls-xG, label= Finishing))+
  geom_bar(stat = "identity", aes(fill=factor(Finishing)), width = .4)+
  scale_fill_manual(name = "Finishing",
                    labels =c("Elite","Clinical","Average","Poor"),
                    values = c("Elite"="#009E73", "Clinical"="#56B4E9", "Average"="#F0E442","Poor"="#ff8080"))+
  labs(subtitle = "Top 20 Goal Scorers",
       title = "Finishing Level")+
  coord_flip()
```

![](Premier-League-2021-2022-Analysis_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

Classification of Finishing level Elite - Players with \>1.5 (Goals -
XG) Clinical - Players with -0.5:+1.5 (Goals - XG) Average -Players with
-1.5:-0.5 (Goals - XG) Poor - Players with \<-1.5 (Goals - XG)

From the visuals, we can see the classification of the finishing levels
of the top 20 goal scorers with Son from spurs being the most elite
finisher, and Mbuemo from Brentford being the poorest finisher among the
top 20.

5.2 Best Player

Using xG and xA per 90, we would determine the best player in the league
using a scatter plot

``` r
Top_xGxA_players_per90 %>%
  ggplot(aes(x=`xG/90`,y=`xA/90`,label = Player))+
  geom_point()+
  geom_text(nudge_x=-0.001,nudge_y=-0.0039,check_overlap = TRUE,size = 2)+
   labs(subtitle = "Expected assists vs Expected Goals",
       title = "Threatening Players")
```

![](Premier-League-2021-2022-Analysis_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->

As we move from left to right in the Threatening Players visual, we see
players that had greater likelihood of their shots leading to goals
while as we move from -bottom to top we see players whose passes had a
greater likelihood of leading to a goal being scored.

From visual

Assist and playmaking oriented -Kevin De Bryune -Jack Grealish These
players rank as the most assist-oriented players in the 2021/2022
season. They are players whose contribution mostly involved passing the
ball to create a goal.

Goal Oriented -Raheem Sterling -Riyad Mahrez -Cristiano Ronaldo These
players rank as the most goal-oriented players in the 2021/2022 season.
They are players whose contribution mostly involved scoring goals.

Best Player - Mohammed Salah from the stats and plot, he is simply an
incredible player with greater scoring chances than the goal-oriented
players and almost as many passes with the likelihood of leading to a
goal as the assist-oriented players.

Evidently the most complete player as seen in the visual.

Statistically, players placed diagonally lower from Salah are also
complete players in terms of chance Creation and goal threat but to a
lesser degree as of last season.

Personal Insight. An interesting insight with the visualizations is
Harry Kane, from his position in the Threatening players visual, it can
be suggested he is the 2nd most threatening player in the league, yet he
is classified as a poor finisher which is not commonly associated with
the player.
