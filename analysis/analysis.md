# NBA Player Statistics – Exploratory Data Analysis

## Introduction
This project explores an NBA player statistics dataset containing player information across multiple seasons. The goal of the project is to understand the structure of the data, summarize important variables, create visualizations, and add team-level information through a join. I chose this dataset because sports data is familiar, interesting, and useful for practicing exploratory data analysis.

## Dataset Source
The main dataset used in this project is `all_seasons.csv`, which contains NBA player information and seasonal statistics. A second dataset, `team_lookup.csv`, was manually created to add conference and division information using the `team_abbreviation` field.

## What the Dataset Contains
The dataset includes player names, team abbreviations, age, height, weight, college, country, draft information, season, and statistics such as points, rebounds, and assists. Each row represents a player-season record.


```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("../data/all_seasons.csv")
joined_df = pd.read_csv("../clean_data/nba_players_with_team_info.csv")
```

## Join Explanation

The join itself was completed in a separate Python script, where the main NBA dataset (`all_seasons.csv`) was merged with a second dataset (`team_lookup.csv`) using `team_abbreviation` as the key. That process created a new file called `nba_players_with_team_info.csv`, which is loaded in this notebook as `joined_df`.

I used a left merge because the NBA player dataset is the main dataset, and I wanted to keep every player-season record while adding conference and division information where a match existed.

This type of merge can create missing values in the new columns if a team abbreviation does not match between the two datasets.


```python
team_lookup = pd.read_csv("../data/team_lookup.csv")
team_lookup.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>team_abbreviation</th>
      <th>conference</th>
      <th>division</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ATL</td>
      <td>Eastern</td>
      <td>Southeast</td>
    </tr>
    <tr>
      <th>1</th>
      <td>BOS</td>
      <td>Eastern</td>
      <td>Atlantic</td>
    </tr>
    <tr>
      <th>2</th>
      <td>BKN</td>
      <td>Eastern</td>
      <td>Atlantic</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CHA</td>
      <td>Eastern</td>
      <td>Southeast</td>
    </tr>
    <tr>
      <th>4</th>
      <td>CHI</td>
      <td>Eastern</td>
      <td>Central</td>
    </tr>
  </tbody>
</table>
</div>




```python
joined_check = pd.merge(
    df,
    team_lookup,
    how="left",
    on="team_abbreviation"
)

joined_check[["team_abbreviation", "conference", "division"]].head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>team_abbreviation</th>
      <th>conference</th>
      <th>division</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>HOU</td>
      <td>Western</td>
      <td>Southwest</td>
    </tr>
    <tr>
      <th>1</th>
      <td>WAS</td>
      <td>Eastern</td>
      <td>Southeast</td>
    </tr>
    <tr>
      <th>2</th>
      <td>VAN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>LAL</td>
      <td>Western</td>
      <td>Pacific</td>
    </tr>
    <tr>
      <th>4</th>
      <td>DEN</td>
      <td>Western</td>
      <td>Northwest</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.head()
joined_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>player_name</th>
      <th>team_abbreviation</th>
      <th>age</th>
      <th>player_height</th>
      <th>player_weight</th>
      <th>college</th>
      <th>country</th>
      <th>draft_year</th>
      <th>draft_round</th>
      <th>...</th>
      <th>ast</th>
      <th>net_rating</th>
      <th>oreb_pct</th>
      <th>dreb_pct</th>
      <th>usg_pct</th>
      <th>ts_pct</th>
      <th>ast_pct</th>
      <th>season</th>
      <th>conference</th>
      <th>division</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Randy Livingston</td>
      <td>HOU</td>
      <td>22.0</td>
      <td>193.04</td>
      <td>94.800728</td>
      <td>Louisiana State</td>
      <td>USA</td>
      <td>1996</td>
      <td>2</td>
      <td>...</td>
      <td>2.4</td>
      <td>0.3</td>
      <td>0.042</td>
      <td>0.071</td>
      <td>0.169</td>
      <td>0.487</td>
      <td>0.248</td>
      <td>1996-97</td>
      <td>Western</td>
      <td>Southwest</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Gaylon Nickerson</td>
      <td>WAS</td>
      <td>28.0</td>
      <td>190.50</td>
      <td>86.182480</td>
      <td>Northwestern Oklahoma</td>
      <td>USA</td>
      <td>1994</td>
      <td>2</td>
      <td>...</td>
      <td>0.3</td>
      <td>8.9</td>
      <td>0.030</td>
      <td>0.111</td>
      <td>0.174</td>
      <td>0.497</td>
      <td>0.043</td>
      <td>1996-97</td>
      <td>Eastern</td>
      <td>Southeast</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>George Lynch</td>
      <td>VAN</td>
      <td>26.0</td>
      <td>203.20</td>
      <td>103.418976</td>
      <td>North Carolina</td>
      <td>USA</td>
      <td>1993</td>
      <td>1</td>
      <td>...</td>
      <td>1.9</td>
      <td>-8.2</td>
      <td>0.106</td>
      <td>0.185</td>
      <td>0.175</td>
      <td>0.512</td>
      <td>0.125</td>
      <td>1996-97</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>George McCloud</td>
      <td>LAL</td>
      <td>30.0</td>
      <td>203.20</td>
      <td>102.058200</td>
      <td>Florida State</td>
      <td>USA</td>
      <td>1989</td>
      <td>1</td>
      <td>...</td>
      <td>1.7</td>
      <td>-2.7</td>
      <td>0.027</td>
      <td>0.111</td>
      <td>0.206</td>
      <td>0.527</td>
      <td>0.125</td>
      <td>1996-97</td>
      <td>Western</td>
      <td>Pacific</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>George Zidek</td>
      <td>DEN</td>
      <td>23.0</td>
      <td>213.36</td>
      <td>119.748288</td>
      <td>UCLA</td>
      <td>USA</td>
      <td>1995</td>
      <td>1</td>
      <td>...</td>
      <td>0.3</td>
      <td>-14.1</td>
      <td>0.102</td>
      <td>0.169</td>
      <td>0.195</td>
      <td>0.500</td>
      <td>0.064</td>
      <td>1996-97</td>
      <td>Western</td>
      <td>Northwest</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>



This confirms how the join works directly in the notebook. The main dataset is merged with the team lookup table using `team_abbreviation`, which adds conference and division columns.


```python
df.shape
df.columns
df.info()
df.describe
df.isna().sum()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 12844 entries, 0 to 12843
    Data columns (total 22 columns):
     #   Column             Non-Null Count  Dtype  
    ---  ------             --------------  -----  
     0   Unnamed: 0         12844 non-null  int64  
     1   player_name        12844 non-null  object 
     2   team_abbreviation  12844 non-null  object 
     3   age                12844 non-null  float64
     4   player_height      12844 non-null  float64
     5   player_weight      12844 non-null  float64
     6   college            10990 non-null  object 
     7   country            12844 non-null  object 
     8   draft_year         12844 non-null  object 
     9   draft_round        12844 non-null  object 
     10  draft_number       12844 non-null  object 
     11  gp                 12844 non-null  int64  
     12  pts                12844 non-null  float64
     13  reb                12844 non-null  float64
     14  ast                12844 non-null  float64
     15  net_rating         12844 non-null  float64
     16  oreb_pct           12844 non-null  float64
     17  dreb_pct           12844 non-null  float64
     18  usg_pct            12844 non-null  float64
     19  ts_pct             12844 non-null  float64
     20  ast_pct            12844 non-null  float64
     21  season             12844 non-null  object 
    dtypes: float64(12), int64(2), object(8)
    memory usage: 1.8+ MB





    Unnamed: 0              0
    player_name             0
    team_abbreviation       0
    age                     0
    player_height           0
    player_weight           0
    college              1854
    country                 0
    draft_year              0
    draft_round             0
    draft_number            0
    gp                      0
    pts                     0
    reb                     0
    ast                     0
    net_rating              0
    oreb_pct                0
    dreb_pct                0
    usg_pct                 0
    ts_pct                  0
    ast_pct                 0
    season                  0
    dtype: int64



## Initial Inspection and Descriptive Analysis

To begin the analysis, I inspected the shape of the dataset, reviewed the columns, checked for missing values, and created summary statistics. This helps establish what kind of data is available and what patterns can be explored further through visualization.


```python
df.isna().sum().sort_values(ascending=False).head(15)
```




    college         1854
    Unnamed: 0         0
    pts                0
    ast_pct            0
    ts_pct             0
    usg_pct            0
    dreb_pct           0
    oreb_pct           0
    net_rating         0
    ast                0
    reb                0
    gp                 0
    player_name        0
    draft_number       0
    draft_round        0
    dtype: int64




```python
df["season"].nunique(), df["season"].min(), df["season"].max()
```




    (27, '1996-97', '2022-23')




```python
df.sort_values("pts", ascending=False)[["player_name","season","team_abbreviation","pts","reb","ast"]].head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>player_name</th>
      <th>season</th>
      <th>team_abbreviation</th>
      <th>pts</th>
      <th>reb</th>
      <th>ast</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10227</th>
      <td>James Harden</td>
      <td>2018-19</td>
      <td>HOU</td>
      <td>36.1</td>
      <td>6.6</td>
      <td>7.5</td>
    </tr>
    <tr>
      <th>4163</th>
      <td>Kobe Bryant</td>
      <td>2005-06</td>
      <td>LAL</td>
      <td>35.4</td>
      <td>5.3</td>
      <td>4.5</td>
    </tr>
    <tr>
      <th>10634</th>
      <td>James Harden</td>
      <td>2019-20</td>
      <td>HOU</td>
      <td>34.3</td>
      <td>6.6</td>
      <td>7.5</td>
    </tr>
    <tr>
      <th>12839</th>
      <td>Joel Embiid</td>
      <td>2022-23</td>
      <td>PHI</td>
      <td>33.1</td>
      <td>10.2</td>
      <td>4.2</td>
    </tr>
    <tr>
      <th>4302</th>
      <td>Allen Iverson</td>
      <td>2005-06</td>
      <td>PHI</td>
      <td>33.0</td>
      <td>3.2</td>
      <td>7.4</td>
    </tr>
    <tr>
      <th>12740</th>
      <td>Luka Doncic</td>
      <td>2022-23</td>
      <td>DAL</td>
      <td>32.4</td>
      <td>8.6</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>12564</th>
      <td>Damian Lillard</td>
      <td>2022-23</td>
      <td>POR</td>
      <td>32.2</td>
      <td>4.8</td>
      <td>7.3</td>
    </tr>
    <tr>
      <th>2847</th>
      <td>Tracy McGrady</td>
      <td>2002-03</td>
      <td>ORL</td>
      <td>32.1</td>
      <td>6.5</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>11537</th>
      <td>Stephen Curry</td>
      <td>2020-21</td>
      <td>GSW</td>
      <td>32.0</td>
      <td>5.5</td>
      <td>5.8</td>
    </tr>
    <tr>
      <th>8013</th>
      <td>Kevin Durant</td>
      <td>2013-14</td>
      <td>OKC</td>
      <td>32.0</td>
      <td>7.4</td>
      <td>5.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.sort_values("pts", ascending=True)[["player_name","season","team_abbreviation","pts","reb","ast"]].head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>player_name</th>
      <th>season</th>
      <th>team_abbreviation</th>
      <th>pts</th>
      <th>reb</th>
      <th>ast</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6802</th>
      <td>Hamady Ndiaye</td>
      <td>2011-12</td>
      <td>WAS</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4235</th>
      <td>Nene</td>
      <td>2005-06</td>
      <td>DEN</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>12048</th>
      <td>Nate Hinton</td>
      <td>2021-22</td>
      <td>IND</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2659</th>
      <td>Pepe Sanchez</td>
      <td>2002-03</td>
      <td>DET</td>
      <td>0.0</td>
      <td>0.7</td>
      <td>0.9</td>
    </tr>
    <tr>
      <th>12095</th>
      <td>M.J. Walker</td>
      <td>2021-22</td>
      <td>PHX</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>0.5</td>
    </tr>
    <tr>
      <th>2675</th>
      <td>Paul Shirley</td>
      <td>2002-03</td>
      <td>ATL</td>
      <td>0.0</td>
      <td>0.5</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>9855</th>
      <td>Chris Boucher</td>
      <td>2017-18</td>
      <td>GSW</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>5624</th>
      <td>Martell Webster</td>
      <td>2008-09</td>
      <td>POR</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4195</th>
      <td>Randy Livingston</td>
      <td>2005-06</td>
      <td>CHI</td>
      <td>0.0</td>
      <td>0.8</td>
      <td>0.2</td>
    </tr>
    <tr>
      <th>12145</th>
      <td>Matt Mooney</td>
      <td>2021-22</td>
      <td>NYK</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby("season")["pts"].mean()
```




    season
    1996-97    8.026077
    1997-98    7.947608
    1998-99    7.358542
    1999-00    7.985845
    2000-01    7.811338
    2001-02    7.982727
    2002-03    7.849299
    2003-04    7.745475
    2004-05    8.088147
    2005-06    7.982533
    2006-07    8.208734
    2007-08    8.267184
    2008-09    8.503820
    2009-10    8.571719
    2010-11    8.206195
    2011-12    7.928870
    2012-13    7.957996
    2013-14    8.090249
    2014-15    8.122561
    2015-16    8.349370
    2016-17    8.426749
    2017-18    8.160370
    2018-19    8.613585
    2019-20    8.726465
    2020-21    8.942407
    2021-22    8.240000
    2022-23    9.121336
    Name: pts, dtype: float64




```python
import matplotlib.pyplot as plt

df["pts"].hist(bins=30)
plt.title("Distribution of Points Per Game (PTS)")
plt.xlabel("PTS")
plt.ylabel("Count")
plt.show()
```


    
![png](Analysis_files/Analysis_14_0.png)
    


### Interpretation of Points Distribution

This histogram shows the distribution of points per game across all player-season records in the dataset. Most observations are concentrated at the lower end of the scoring range, with fewer players averaging very high point totals. This creates a right-skewed distribution, which makes sense because only a small number of players score at an elite level, while many players have lower scoring averages.


```python
avg_pts_by_season = df.groupby("season")["pts"].mean().sort_index()

avg_pts_by_season.plot()
plt.title("Average Points Per Game by Season")
plt.xlabel("Season")
plt.ylabel("Average PTS")
plt.xticks(rotation=90)
plt.show()
```


    
![png](Analysis_files/Analysis_16_0.png)
    


### Interpretation of Average Points by Season

This graph shows how the average points per game in the dataset changes across NBA seasons. While the values do not rise perfectly every year, the overall pattern suggests that average scoring tends to increase over time. This is useful because it shows that player scoring trends are not static and that season-level analysis can reveal broader changes in the game.


```python
df.plot(kind="scatter", x="usg_pct", y="pts")
plt.title("Usage % vs Points Per Game")
plt.xlabel("Usage %")
plt.ylabel("PTS")
plt.show()
```


    
![png](Analysis_files/Analysis_18_0.png)
    


### Interpretation of Usage % vs Points Per Game

This scatterplot compares player usage percentage with points per game. There is a clear positive relationship, meaning that players with higher usage percentages generally tend to score more points. However, the relationship is not perfect, since some players have moderate or even high usage without scoring at the same level. This graph is important because it shows that offensive role and scoring are related, but other factors also affect production.


```python

```
