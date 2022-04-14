# League of Legends Capstone
----

## Executive Summary
----

The goal of this project is to get a deep understanding of the datapoints within league of legends and build a supervised learning model which can accurately predict whether a team won or lost a match based on the end stats of ranked matches for challenger tier players.

Metrics of success include having an R^2 Score and F1 Score approaching 1.

After extensive EDA and Feature Engineering the final results of the model is:
<center>
    | Metric | Score |
    | ------ | ----- |
    | R^2 | 0.967 |
    | F1 | 0.934 |
    | ------ | ----- |
    | Accuracy | 93.786% |
    | Precision | 94.178% |
    | Sensitivity | 92.724% |
    | Recall | 92.724% |
    | ------ | ----- |
    | True Posistives | 7748 |
    | False Positives | 479 |
    | False Negatives | 608 |
    | True Negatives | 8658 |
</center>

The Model Chosen was Logistic Regression. In life often times the simplest tools can be the most effective. While the problem could be solved with other more complicated modelling techniques there are drawbacks to those complications. If a simple model has a high level of success then using a more complicated solution serves only to obfuscate the solution and cost more computational power to generate and act on predictions.

## Conclusions and Insights
----
League of Legends is a complicated game with a large amount of variables. Despite this complexity there are some clear rules to predicting success in the game.

<center><b>Get and Maintain a Lead</b></center>

----
The snowball effect has always been a topic of discussion amongst top tips to improving league of legends gameplay. Get a lead and keep it at all costs. This exploration into the dataset has given hard numbers supporting these claims.

Before 40 minutes the top metrics of a team's success are about being ahead. Gold Earned, Champion Level, and Tower Kills. These features are not skill based. These are lead based. One top player that runs a youtube channel dedicated to advising players to improve their performance in the game has stated that League of Legends is a game of basic math; people with higher numbers win. This applies to one on one fights (the person with the higher level wins), pressure within the game (people with more dragon and baron kills have more pushing power) and the overarching game itself (players that kill more objectives win). This process has proven these claims with objective numbers to support the experience of top tier players and analysts.

As much as League of Legends is a game of skill the main goal for players is the get and maintain a lead early.

<center><b>Late Game Skill</b></center>

----
After the 40 minute mark the predictors drastically change as players have reached the caps of Champion Levels and Item Levels.

Bounty Level becomes the main predictor of winning teams as it implies a team has managed to win team fights and pushed to win.

<center><b>Next Steps</b></center>

----

Items was examined at a very basic level. This feature could benefit from an unsupervised classification model that could classify items based on poularity and impacts on gameplay mechanics.

I don't think this could improve the Logitistic Regression Model I do believe it would give further insights into the items within the game potentially identifying powerful items teams should focus on as well as items which are underpowered which should be avoided. 

----

## Synopsis
----

After compiling the dataset the DataFrame had 1150 features. The main priority of EDA was to get a full understanding of the feature set and simplify terms to solve the problem.

After some basic exploration it was simple to determine the dataset was very clean with minimal null values. The null values that did exist were from Riot ID values and could simply be dropped as irrelevant to the problem statement.

<center><b>Navigation</b></center>

----

The first major problem which needed to be solved was a way to navigate all of the feature names. With 1150 features in the base data it is not practical to have large lists of code to scroll through or manually create those lists every time a mask is needed. As such I designed a system to easily use list comprehensions to generate feature lists on the fly using a handful of feature name components stored in an external file.


Example:
```python
[f"{player}_{feature}" for feature in PLAYER_FEATURES[0:5]
                       for player in PLAYER_PREFIXES[0:2]]
```
returns the first 5 features with the first 2 player prefixes:
```python
['t1p1_assists', 't1p2_assists', 't1p1_baronKills', 't1p2_baronKills', 't1p1_bountyLevel', 't1p2_bountyLevel', 't1p1_champExperience', 't1p2_champExperience', 't1p1_champLevel', 't1p2_champLevel']
```

<center><b>Aggregation</b></center>

----

The second big hurdle to tackle was reducing complexity without losing data. As League of Legends is a team game and the problem was to predict whether Team 1 or Team 2 won all individual stats had to be aggregated using various techniques into Team Scores.

<center><b>Differencing</b></center>

----

Reducing the individual scores to team scores was simply the enty point to the feature engineering aspect of this problem. Due to the Law of Averages half the time Team 1 won and half the time Team 2 won. This meant that virtually all of the metrics could be strong for one team or the other but ultimately these features needed to be tied together in order to be truly effective.

# Instert Images here

<center><b>Combining Features</b></center>

----

In some cases there were more complicated algorithms that could be utilized to represent multiple feature sets not only allowing complexity to be reduced but to also increase preciactive power in the data. One example of this is the Dominance Ratio which takes Kills, Deaths and Assists and combines them using an algorithm. This resulted in a correlation coefficient increase of 0.3 and a net reduction of 2 features.

Dominance Ratio: $\frac{2 * Kills + Assists}{3 * Deaths}$

<center><b>Outliers</b></center>
There were quite a few outliers. One simple outlier which had to be removed was the Early Surrender outlier which in the Riot API only refer to games which had an AFK player in the match rather than games which resulted in an actual surrender before 20 minutes.

However the bigger exmaple of outliers needing to be addressed is the fact the key predictors for most games fell off after matches reached 30 minutes. In order to counteract this and improve predictions for the entire dataset I altered the interpretation of the late game statistics by combining the degrading features with a feature that works well in the end game.

# Insert Images Here

## Modelling
----

The model chosen was Logistic Reegresion. This is because, as stated earlier, it performed extremely well, all of the data was linear in nature and there was no need for a more complicated solution.

I modeled in a series of steps to prove multiple hyptheses starting with rejecting the null hypothesis.

<center><b>Model 1</b></center>

----

The baseline score was 47%. The basic model which used loosely filtered feature set had an R2 Score of 96.907% ± 0.00634 which is a very impressive score on it's own. However there were multicollinear features and biases in the model whcih could be improved.

<center><b>Model 2</b></center>

----

The second model performed worse than first. This was because removing the bias in the previous model caused the noise in the late game features to reduce the models effectiveness.

<center><b>Model 1</b></center>

----

The third model switched the basic features for the modified features with the expectation that this would reduce the noise in the late game datasets. This model performed amazingly well with an R2 Score of 96.655% ± 0.00923. False Positives and False Negatives were also signifigantly reduced.

The full scores as well as the conclusions were listed in this executive summary.

# Closing

When I started this project I expected to go through and create a smattering of models to show competancy in a variety of them. However as I was doing research I came to feel that the best use of my time would be to fully document the EDA section with detailed explanation. This technical report is a cliff note in comparison.

I feel it is easy to come to believe Data Science is about modelling but the reality is Data Science is about understanding the data. As critical as model building is, the model selection process and the model building process would not be effective if the data scientist didn't have a deep competancy in understanding how their data works with the modelling process.

