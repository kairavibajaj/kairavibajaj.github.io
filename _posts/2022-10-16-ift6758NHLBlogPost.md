---
layout: post
title: Milestone 1
---



#### Question 1

...content...

#### Question 2

...content...


## Step 2: Interactive Debugging Tool 


#### Question
vk
...content...



## Step 3: Tidy Data


#### Clean Dataframe Screenshot

![image](/figures/head10.png "Title")
The above image is a screenshot of the first 10 rows of an example clean dataframe. We decided to keep as many useful columns as we could image as the task or predictive target is unclear. 

#### How can we get PowerPlay/Even-Strength/Penalty Kill Data for Shots?

It would be quite simple if we were to use the game data in the JSON files. The data included when penalties were called and how long they lasted. If we were to keep track of the game situation data, it would be simple to reference that data and add a column indicating the game situation.

#### What other features could be informative for scoring chances?

The first that could be useful would be a binary variable indicating if the shot occured on an odd-man rush. An odd man rush is when there are more offensive players than defensive players on a rush. This means that if there is good passing, it creates high quality shot chances, this would be very informative for shot chances. A second feature that we could use is binary variable indicating whether the shot was a one-timer of not. One-timers usually occur is high scoring chances, like cross-ice passed and happen quickly so that the goalie doesn't have as much time to position himself to save it. One last feature that we could use could be a binary variable that says if the play is a breakaway or not. I supposed this is a sort of odd man rush, however in this case there is no deffender. These are very high scoring chances and would be nice to have a feature indicating it.


## Step 3: Simple Visualizations


![image](/figures/stats_by_shottype.png "Shot Type")


From this data, tip-ins and deflected shots have the highest percentage of goals per shot. However, they are also the least common type of shot. Wrist shots are the most common type of shot and result in the most amount of goals however only 10% go in. This figure perfectly illustrates the shots/goals per shot type.


![alt-text-1](/figures/shot_distances.png "title-1") ![alt-text-2](/figures/shotdistances2.png "title-2")
![alt-text-1](/figures/shotdistances3.png "title-3") ![alt-text-2](/figures/shotdistances4.png "title-4")
![alt-text-1](/figures/shotdistances5.png "title-5")

It's apparent that the number of shots increases from the net to a couple meters out. This is where the most amont of goals/shit is. After around 17m from the net, there is a significant drop-off in goals but shots remain about the same. There figures illustrate the shot/goal ratio for distances for each given season.

![image](/figures/last.png "Shot Type Distance")

This image shows the percentage of goals per shots given by shot type of distance. There are obvious outliers in these plots but we wanted to show the complete data. This is the only graph that we could have used to answer the question. From this image, the wrist shot has the highest percentage from the closer distance and keeps a relatively high scoring rate for all distances.


## Step 4: Advanced Visualizations

Looking at the figures from season 2016-2020, there is a main trend with the shots. The average team takes most shots from the slot, and either side of the point (blue line). The heat map featuring the expected shots is interesting as it shows how each team differs. Most teams take more or less slots shots, and more or less right and left point shots. There aren't many shots expected to be from areas near the boards or behind the net. These plots are quite useful in determining how many shots per average each team takes in comparing to the league average. It is also interesting to see teams with superstars taking more shots from the players' positions. As an example, on the Washington Capitals, there is a much higher than average shot excess per game at the left faceoff circle which is known to be Alex Ovechkin's (consistent 50+ goal scorer) position.


If we look at the 2016-2017 Colorado Avalanche, they took a tremendous amount of shots from low-scoring areas. They have higher than expected shots per game in almost every area except the slot area (where the vast majority of goals are scored). So that year's iteration took low-scoring shots and less than expected shots in the high scoring areas. That year's avalanche also finished last in their division and didn't make the playoffs. In contrast, if we look at the 2020-21 Colorado Avalanche, we see that the amount of shots taken in high scoring areas is above league average and they take less than league average or league average amount of shots from outside-slot area. This translated into the team finishing at the top of their division and in a high playoff seeding.


Like the 2020-21 Colorado Avalanche, the Tampa Bay Lightning take more shots from the slot and high scoring chances than the league average. This absolutley contributes to their success. In contrast, we see that the teams in Buffalo take less shots from the slot and high scoring areas. They do take higher than average amount of shots from outside areas and lower scoring chances. This also contributes to their near last place finishes. I think this paints a good picture but not entirely complete. The amount of shots from high scoring areas absolutley contributes to the teams' seeding. However, it's not the Sabres lack of trying. The personel each team has makes it easier or harder to get high quality chances. If the Sabres had better chances, they would be able to tale better quality shots for better areas. 





