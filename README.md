# Penalty-Kick-Taker-Analysis
Python-based data anaysis on penalty kick factors that contribute to success 

Hate them or love them, penalty kicks carry an enormous amount of deterministic weight to the outcomes of football matches. This is especially true in cup competitions, where the pressure of an entire nation can be placed upon a single player and kick. 

While many aspects of football are fuzzy from a statistical perspective, penalty kicks are unusual in that the outcome is semi-binary. Either a penalty is successful or unsuccessful. This binary nature of the event makes it a great subject for statistical analysis. What if we could analyze real-life match data to understand what factors may contribute to the success or failure of a penalty kick? These insights would not only be interesting from an academic perspective but also could carry implications for football teams and managers in their decision-making.

## The Penalty Data Available

When gathering the right data for an analysis of penalties, I found it important to have events from a variety of competitions. Any football player or fan would tell you that penalty kicks taken as part of a penalty shootout carry a different energy to them compared to a penalty kick in a league match (generally speaking). Therefore, having data across competitions would allow us to compare the statistical difference as well.

Fortunately, I found a publicly available dataset of 67,286 penalty kicks compiled by Vollmer, Schoch, and Brandes (2024), published alongside their article “Penalty shoot-outs are tough, but the alternating order is fair.” Their comprehensive dataset and research provided a valuable foundation for this project. 

I joined this valuable source with the European Soccer Database from Kaggle to connect more detailed information on the players who were involved in each penalty kick of the set. This latter dataset included a catalog of EA FC (formerly EA Sports FIFA) player ratings. Growing up, I played my fair share of FIFA video games, and I thought it would be interesting to see if their in-house ratings corresponded to any statistical correlation as well. 

Combining the sources provided me with a variable-rich dataset of almost 16,000 penalty kicks and information on the players who took them. From here, we can explore whether certain player characteristics correlate to penalty kick success.

## How important is a player’s age (and experience) when taking penalties?

We often hear about the importance of composure and experience when taking that all-important penalty. Commentators will often call upon maturer players to “step up” and take early penalties in a shootout. It is the responsibility of these leaders to settle the nerves for the younger players as the shootout progresses. Managers may even select their running order based on this adage. But is it really true from a statistical perspective?

Let’s test whether player age is positively correlated with penalty success and whether this correlation is statistically significant. Using the player’s birthday, I calculated the age of each penalty kick taker at the time of a particular match. Applying some data science best practices, I ran a logistic regression model to test the predictive power of player age.

<img width="975" height="354" alt="image" src="https://github.com/user-attachments/assets/92e3023c-3a33-4e02-bacd-e6ed7ea54e0d" />

Assuming an alpha of 0.05, the age of a player at the game was found to be statistically significant. According to this simple regression model, each additional year of a player’s age corresponds to a 0.94% increase in the odds of successfully scoring their penalty. 

But as discussed above, some penalty kicks are higher pressure situations for players. A penalty shootout for one’s national team or in the Champions League might expose the benefits of age and maturity more than when taking into account league games as well. At least, intuition might suggest as much. One only needs to recall the Euro 2020 final where England lost to Italy in a dramatic penalty shootout. Could the relative young age of England’s penalty kick takers be a factor in this result? If we filter our dataset to exclude league matches and re-run our logistic regression model, the results are interesting.

<img width="975" height="354" alt="image" src="https://github.com/user-attachments/assets/e82c35e8-26d1-430e-a310-cf9ed0661846" />

When only focusing on matches where the pressure of a penalty kick might be greater (cup, tournament, and international games), our model suggests that player age becomes more important. Now, each additional year increases the odds of a successful penalty by 2.36%. From a statistical perspective, the p-value of the variable also greatly decreases in this new data subset. 

We can visualize this difference between general penalty performance and cup/international specific performance by age bracket:

<img width="1214" height="560" alt="image" src="https://github.com/user-attachments/assets/8a1afc81-02e1-4490-b46c-e0fc2a99b030" />

Here, we can see that the rate of scoring a penalty increases more noticeably as you increase age brackets. The dip in success rate for 15-20 year olds in cup/international competitions can be  seen as well. 

This outcome suggests that age indeed matters when taking penalties, especially in cups and international competitions. Perhaps league matches are a better opportunity for younger players to gain the experience and confidence necessary when taking penalties with slightly lower stakes. Based on this initial analysis, the traditional wisdom of letting your most experienced players take those all-important penalties could be a safer bet. 

## FIFA (EA FC) Ratings: How Accurate Are They for Penalty Kicks?

Much debate goes on each year by fans and even among players themselves on the player ratings that the team at EA Sports determine. A group of internal and external collaborators contribute to the individual player ratings, largely through observation. As we have these ratings connected to our dataset, we can test how statistically relevant they are when it comes to penalty kick success.

Running another logistic regression on the penalty rating score of each player in the dataset, we can see the results below:

<img width="975" height="354" alt="image" src="https://github.com/user-attachments/assets/2d75c378-6f6a-4156-9579-92935cd803d9" />

Overall, the FIFA penalty rating is statistically significant in this simple model. However, there is a key difference between statistical significance and real-world impact. According to the model, each additional point to a player’s penalty rating increases the likelihood of scoring a penalty by 0.57%. 

Visually, this penalty rating is potentially contributing to a very small percentage change:

<img width="975" height="577" alt="image" src="https://github.com/user-attachments/assets/4e30f2bb-43f9-437a-ac5f-af2940e9dfb7" />

The absolute lowest FIFA penalty rating in the dataset corresponds to a predicted penalty success rate of roughly 73.5% while the highest rating corresponds to 81.5% success rate. In practice, the average (mean) professional player’s FIFA penalty rating is 68.5. In this model, having a perfect penalty rating compared to an average score increases the odds of scoring by only around 2%. It is encouraging that FIFA’s penalty rating does indicate statistical significance in this analysis, but it certainly isn’t a guarantee for success.

Next time on StatKicker, I will be exploring the other side of the penalty kick – what factors contribute to a goalkeeper’s success at saving penalties – a much less likely event in football.





