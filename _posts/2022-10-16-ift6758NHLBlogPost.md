---
layout: post
title: Milestone 1
---


## Step 1: Data Acquisition

* Importing the required libraries
  We will be requiring the following libraries to download our data from the NHL API:
  * os
  * urllib
  * json
  * tqdm

{% highlight js %}
// Importing libraries
import os
import urllib.request, json
from tqdm import tqdm

{% endhighlight %}

* NHL data is very rich; it contains information from many years into the past ranging from 
metadata about the season itself (eg. how many games were played), to season standings, to player 
stats per season, to fine-grained event data for every game played, known play-by-play data.
First, we'll start with getting the duration of years for which we want the data.

{% highlight js %}
def __init__(self, start_year: int, end_year: int, local_data_repo: str) -> None:
    '''
    Class Constructor to initialize instance.

    Input(s):
    start_year (int): Year from which data is to be loaded for. (ex. 2017)
    end_year (int): Year upto which data is to be loaded for. (ex. 2020)
    local_data_repo (str): path to local data repository from where the data will 
    be stored/fetched. By default it is set from environment variable DATA_LOC.
    '''
    assert start_year > 2015 ,  f"start year should be greater than 2016 expected, got: {start_year}"
    assert end_year < 2023 ,  f"start year should be less than 2023 expected, got: {end_year}"
    self.start_year = start_year
    self.end_year = end_year
    self.local_data_repo = local_data_repo

def get_years_list(self) -> list: 
    '''
    Generates a list of years from start_year to end_year with the increment of 1.

    Input(s):
    None

    Output:
    list of years. (ex. [2017, 2018, 2019, 2020]) 
    '''
    return list(range(self.start_year, self.end_year+1, 1))

{% endhighlight %}

* Now that we have the years for which we need the data; the next step is to separate the data on basis of the type of the game. This can be done by generating game_ids for different types of matches. It is demonstrated in the following code snippet.

{% highlight js %}
def generate_game_id(self, game_type: int) -> list:
        '''
        For a given year and game type it generates a list of possible game ids.
        Input(s):
        game_type (int): Encoded form of game type (i.e 1 for regular match and 2 for playoff)
        Output: 
        List of generated 10 digit game_ids.
        '''
        years = self.get_years_list()
        game_ids = []
        for year in years:
            if year <2017:
                total_matches = 1230
            else:
                total_matches = 1271
            match_id_list = list(range(1, total_matches+1, 1))
            for match_id in match_id_list:
                game_ids.append(str(year)+f'{game_type:02}'+f'{match_id:04}')
        return game_ids

{% endhighlight %}

* These generated game_ids will be used to fetch data from the NHL public API. The following function fetches data associated with a particular game_id from the API.

{% highlight js %}

def download_from_endpoint(self, game_id, file_path) -> None:
        '''
        Connects to the NHL public API to download game data and saves it to a hierarchical file storage.
        Input(s):
        game_id (str) : a particular game id for which data is to be downloaded for.
        file_path(str): path to local data repository from where the data will be stored/fetched. By default it is set from environment variable DATA_LOC.
        
        Output(s):
        None
        '''
        link = "https://statsapi.web.nhl.com/api/v1/game/{0}/feed/live/".format(game_id)
        try:
            with urllib.request.urlopen(link) as url:
                data = json.load(url)
                os.makedirs(os.path.dirname(file_path), exist_ok=True)
                with open(file_path, 'w') as f:
                    json.dump(data, f)
        except BaseException as e:
            with open('log.txt', 'a') as logger:
                logger.write(link+','+str(e)+'\n')

def load_data(self) -> None:
        '''
        Generates and iterates over game ids from start year to end year to load the data if not cached then downloads data.
        Input(s):
        None
    
        Output(s):
        None
        '''
        game_types_list = [2,3]
        for game_type in game_types_list:
            id_list = self.generate_game_id(game_type)
            for game_index in tqdm(range(len(id_list))):
                file_path = os.path.join(self.local_data_repo, id_list[game_index][:4], id_list[game_index][4:6], str(id_list[game_index][6:])+'.json')
                if os.path.exists(file_path):
                    pass
                else:
                    self.download_from_endpoint(id_list[game_index], file_path)
                    pass
{% endhighlight %}

## Step 2: Interactive Debugging Tool

The tool below allows one to go through the .json format game data downloaded using the Data Acquisition Tool. The top half of the tool selects the desired game, while the botom half looks through the interested events of said game.

The following code snippet gives a summary of how we generated the interactive widget:

![Interactive debugging tool Code](/figures/Screen Shot 2022-10-23 at 2.14.55 PM.png)

Now lets look at the final output. It can be seen in two parts. First part depicts the tool that selects the year and desired game type and second depicts the tool that gives the option to select the type of plays and all the information related to that particular shot.

![Interactive tool 1](/figures/Screen Shot 2022-10-23 at 2.22.19 PM.png)

![Interactive tool 2](/figures/Screen Shot 2022-10-23 at 2.24.29 PM.png)

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

{% include 2016.html %}
{% include 2017.html %}
{% include 2018.html %}
{% include 2019.html %}
{% include 2020.html %}

Looking at the figures from season 2016-2020, there is a main trend with the shots. The average team takes most shots from the slot, and either side of the point (blue line). The heat map featuring the expected shots is interesting as it shows how each team differs. Most teams take more or less slots shots, and more or less right and left point shots. There aren't many shots expected to be from areas near the boards or behind the net. These plots are quite useful in determining how many shots per average each team takes in comparing to the league average. It is also interesting to see teams with superstars taking more shots from the players' positions. As an example, on the Washington Capitals, there is a much higher than average shot excess per game at the left faceoff circle which is known to be Alex Ovechkin's (consistent 50+ goal scorer) position.


If we look at the 2016-2017 Colorado Avalanche, they took a tremendous amount of shots from low-scoring areas. They have higher than expected shots per game in almost every area except the slot area (where the vast majority of goals are scored). So that year's iteration took low-scoring shots and less than expected shots in the high scoring areas. That year's avalanche also finished last in their division and didn't make the playoffs. In contrast, if we look at the 2020-21 Colorado Avalanche, we see that the amount of shots taken in high scoring areas is above league average and they take less than league average or league average amount of shots from outside-slot area. This translated into the team finishing at the top of their division and in a high playoff seeding.


Like the 2020-21 Colorado Avalanche, the Tampa Bay Lightning take more shots from the slot and high scoring chances than the league average. This absolutley contributes to their success. In contrast, we see that the teams in Buffalo take less shots from the slot and high scoring areas. They do take higher than average amount of shots from outside areas and lower scoring chances. This also contributes to their near last place finishes. I think this paints a good picture but not entirely complete. The amount of shots from high scoring areas absolutley contributes to the teams' seeding. However, it's not the Sabres lack of trying. The personel each team has makes it easier or harder to get high quality chances. If the Sabres had better chances, they would be able to tale better quality shots for better areas. 





