# League of Legends Capstone
----

## Problem Statement
----

Problem Statement:
E-sports is growing in popularity and data has become a key aspect both for the game developers ensuring quality gameplay as well as the players to determine the best strategies to win.

I will create a Logistic Regression Model to determine trends in gameplay which will help teams know which aspects of the game are key factors in which teams win.


## Executive Summary
----

The goal of this project is to get a deep understanding of the datapoints within league of legends and build a supervised learning model which can accurately predict whether a team won or lost a match based on the end stats of ranked matches for challenger tier players.

Metrics of success include having an R^2 Score and F1 Score approaching 1.

After extensive EDA and Feature Engineering the final results of the model is:

| Metric | Score |
| ------ | ----- |
| R2 | 0.964 ± 1.65% |
| F1 | 99.1% ± 0.431% |
    
| Metric | Score |
| ------ | ----- |
| Accuracy | 98.079% |
| Precision | 97.727% |
| Sensitivity | 98.265% |
| Recall | 98.265% |
    
| Metric | Score |
| ------ | ----- |
| True Posistives | 8946 |
| False Positives | 191 |
| False Negatives | 145 |
| True Negatives | 8211 |


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


# Closing

When I started this project I expected to go through and create a smattering of models to show competancy in a variety of them. However as I was doing research I came to feel that the best use of my time would be to fully document the EDA section with detailed explanation. For a full explanation fo the processes taken to get these results please read the EDA section in particular.

I feel it is easy to come to believe Data Science is about modelling but the reality is Data Science is about understanding the data. As critical as model building is, the model selection process and the model building process would not be effective if the data scientist didn't have a deep competancy in understanding how their data works with the modelling process.
