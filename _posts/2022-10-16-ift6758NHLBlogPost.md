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

![image](figures/head10.png "Title")
The above image is a screenshot of the first 10 rows of an example clean dataframe. We decided to keep as many useful columns as we could image as the task or predictive target is unclear. 

#### How can we get PowerPlay/Even-Strength/Penalty Kill Data for Shots?

It would be quite simple if we were to use the game data in the JSON files. The data included when penalties were called and how long they lasted. If we were to keep track of the game situation data, it would be simple to reference that data and add a column indicating the game situation.

#### What other features could be informative for scoring chances?

The first that could be useful would be a binary variable indicating if the shot occured on an odd-man rush. An odd man rush is when there are more offensive players than defensive players on a rush. This means that if there is good passing, it creates high quality shot chances, this would be very informative for shot chances. A second feature that we could use is binary variable indicating whether the shot was a one-timer of not. One-timers usually occur is high scoring chances, like cross-ice passed and happen quickly so that the goalie doesn't have as much time to position himself to save it. One last feature that we could use could be a binary variable that says if the play is a breakaway or not. I supposed this is a sort of odd man rush, however in this case there is no deffender. These are very high scoring chances and would be nice to have a feature indicating it.


## Step 3: Simple Visualizations


![image](figures/stats_by_shottypstats_by_shottype.png "Shot Type")


From this data, tip-ins and deflected shots have the highest percentage of goals per shot. However, they are also the least common type of shot. Wrist shots are the most common type of shot and result in the most amount of goals however only 10% go in. This figure perfectly illustrates the shots/goals per shot type.


![alt-text-1](figures/shot_distances.png "title-1") ![alt-text-2](figures/shot_distances2.png "title-2")
![alt-text-1](figures/shot_distances3.png "title-1") ![alt-text-2](figures/shot_distances4.png "title-2")
![alt-text-1](figures/shot_distances5.png "title-1")

It's apparent that the number of shots increases from the net to a couple meters out. This is where the most amont of goals/shit is. After around 17m from the net, there is a significant drop-off in goals but shots remain about the same. There figures illustrate the shot/goal ratio for distances for each given season.

![image](figures/last.png "Shot Type")

This image shows the percentage of goals per shots given by shot type of distance. There are obvious outliers in these plots but we wanted to show the complete data. This is the only graph that we could have used to answer the question. From this image, the wrist shot has the highest percentage from the closer distance and keeps a relatively high scoring rate for all distances.


