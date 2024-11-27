# Data Analysis Project: Understanding Player Valuations on Game Outcomes

## **Overview**
This project analyses football games by combining data from player market valuations (from transfermarkt.co.uk) and betting odds. The aim is to uncover insights into the relationship between team valuations and outcomes. This analysis focuses on games from major leagues, including the Premier League (GB1), Bundesliga (L1), and La Liga (ES1).

---
## **Sources**
  - Transfermarkt.co.uk data comes from https://www.kaggle.com/datasets/davidcariboo/player-scores
  - Betting data comes from https://www.football-data.co.uk/
---

## **Goals**
1. **Extract Relevant Game Information**:
   - Filter game data to include only relevant leagues and competitions.
   - Retain key details like game IDs, dates, and participating clubs.

2. **Transform and Clean Player Valuation Data**:
   - Match player valuations to their respective games using player IDs and dates.
   - Calculate aggregated club valuations based on starting lineups.

3. **Integrate Betting Data with Game Valuations**:
   - Merge betting odds with game valuation data.
   - Assign home and away valuations to each game based on club IDs.

4. **Generate Actionable Insights**:
   - Explore the relationship between betting odds and team valuations.
   - Identify trends and anomalies that could inform betting strategies or valuation assessments.

---

## **Datasets**
### **1. Games Dataset**
- Source: `games.csv`
- Contains:
  - `game_id`: Unique identifier for each game.
  - `home_club_id` and `away_club_id`: Identifiers for the participating clubs.
  - `date`: Date of the game.
  - `competition_id`: Unique identifier for the competition of the game.

### **2. Player Valuations**
- Source: `player_valuations.csv`
- Contains:
  - `player_id`: Unique identifier for each player.
  - `market_value_in_eur`: Player's market valuation.
  - `date`: Date of the valuation.

### **3. Game Lineups**
- Source: `game_lineups.csv`
- Contains:
  - `game_id`: Unique identifier for each game
  - `club_id`: Unique identifier for each club
  - `player_id`: Unique identifier for each player.
  - `market_value_in_eur`: Player's market valuation.
  - `date`: Date of the valuation.
    
### **3. Betting Data**
- Source: Various betting odds datasets.
- Contains:
  - `HomeTeam` and `AwayTeam`: Names of the competing teams.
  - `odds`: Betting odds for the match outcome.
  - `date`: Date of the game.
  - `FTR`: Full Time Result
  - `B365H`, `B365D` and `B365A`: Bet365 odds for home win, draw and away win that is used in this analysis.
---

## **Key Findings from the Data**
1. **Game Information Extraction**:
   - Filtered and cleaned games data to include only league matches for major competitions.
   - Created a connection file linking games with club IDs and dates.

## **2. Team Valuations vs. Outcomes**

### **Scatter Plot: Team Valuations**
![image](https://github.com/user-attachments/assets/1ead49e0-ed8f-4d06-9395-11886d5279c8)

In this scatter plot, the valuations of the starting XI for the home and away teams are plotted against each other. Each point represents a match, and the green points indicate games where the team with the more "valuable" starting XI won.

However, the high density of overlapping data points makes it challenging to draw meaningful conclusions. This plot lacks clarity due to data congestion, but allows us to see the extent are data is reliable.

---

### **Heatmap: Team Valuations**
![image](https://github.com/user-attachments/assets/d807e7e1-a35c-4661-81fa-c9f50d44bf68)

The heatmap provides a clearer visualization of the same data. The x-axis represents the valuation of the home team, while the y-axis represents the valuation of the away team. The intensity of the color indicates the density of matches correctly predicted by team value.

Each square (bin) considers all observations that were plot on the above scatter graph. The closer the bin is to green (1.0), the more accurate our team value prediction is. The closer the bin is to red (0), the less accurate our team value prediction is.

#### **Key Observations**:
1. **Uncertainty Along the Diagonal (`y = x`)**:
   - Matches where the valuations of both teams are nearly equal exhibit the most uncertainty in outcomes, in the data range with the most observations. This is makes sense, as closely matched teams often produce unpredictable results.

2. **Outcome Bias Towards Home Teams**:
   - As the valuation gap increases (moving away from `y = x`), the results become more predictable.
   - Interestingly, there is a noticeable bias towards home teams, with fewer unexpected outcomes favoring the away team. This supports the concept of the "12th man" advantage, where home fans contribute to their team's performance.

4. ## Valuation and Betting Odds Analysis

This analysis explores the relationship between the team valuations and betting odds, using historical data to analyze patterns and trends. The primary idea is to compare probabilities, rather than a win/draw/loss categorisation.

---

## **Goals**
1. **Analyze the Relationship Between Valuations and Betting Odds**:
   - Investigate how differences in team valuations correspond to pre-match betting odds.
   - Identify patterns and trends in game outcomes based on these metrics.

2. **Develop Predictive Insights**:
   - Use regression analysis to determine how valuation differences influence implied odds.
   - Highlight deviations from expected relationships as potential areas of interest.

3. **Simulate Betting Strategies**:
   - Test betting strategies based on valuation differences and implied odds.
   - Simulate potential returns to evaluate the accuracy of these strategies.

---


markdown
Copy code
### **Regression Analysis: Valuation Differences vs Implied Odds**

#### **1. Understanding the Relationship**
![image](https://github.com/user-attachments/assets/cfd36ce6-85e8-4647-812f-711e0c615f45)

This plot shows games that were either won or lost, with the x-axis representing the implied probability of winning and the y-axis representing the difference in valuation between the winning and losing teams. As expected, there is a positive correlation between the bookmakers' favorites (lower implied odds) and teams with higher valuations.

#### **Key Insight: Betting Above the Regression Line**
In theory, bets positioned above the regression line represent opportunities where the bookmakers may have undervalued a team. These bets could potentially offer an edge over the bookmakers. The question is: could this strategy yield profitable results over time?

---

#### **2. Betting Simulation Results**
##### **Betting on All Games Above the Regression Line**
![image](https://github.com/user-attachments/assets/6c2a241b-b419-453f-a5a6-76c5fe1a9cbb)

When betting on every game positioned above the regression line, the results show a clear disadvantage. The bookmakers' edge remains too strong, leading to significant losses over time. This approach alone does not appear to be a viable strategy.

---

##### **Betting on Games One Standard Deviation Above the Regression Line**
![image](https://github.com/user-attachments/assets/a2950830-a20f-4c95-b65f-df906c1160d7)

By narrowing the focus to bets at least one standard deviation above the regression line, the results improve. While losses are still incurred, they are significantly reduced compared to the first strategy. This suggests that higher deviations may offer more value.

---

##### **Betting on Games Two Standard Deviations Above the Regression Line**
![image](https://github.com/user-attachments/assets/9677c359-3ddb-4ecf-874b-aa5b7bf2e97b)

When further restricting bets to those two standard deviations above the regression line, the outcomes improve further. Although this strategy does not completely eliminate losses, it minimizes them substantially compared to the previous approaches.

---

---

## **Next Steps**
- **Regression Analysis**:
  - Investigate the numbers behind the simple regression model (win%, home/away bets, draws, long and short odds)
- **Model Development**:
  - Develop more complex predictive analysis 


