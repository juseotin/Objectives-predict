# Objectives-predict


By Justin Seo
## Introduction

Our dataset comprises all professional League of Legends games that took place in 2023. This dataset includes various match statistics, focusing on specific events and overall performance metrics. The dataset is extensive, containing detailed information on each game's events, team performances, and outcomes.

Our primary question is: “How do specific early game events impact the likelihood of a team winning?” By addressing this question, we aim to provide insights into the critical events that can shift the balance of a game. Understanding these key events can help teams strategize better and improve their chances of winning.

Although the data does not explicitly indicate the impact of each event, we can infer this information from columns such as “event1”, “event2”, “event3”, “blueJungleKDA”, “redJungleKDA”, and the final “result” of the game.

League of Legends is a complex game where early game advantages can snowball into a decisive victory. Players and coaches often debate which early game actions (like securing the first tower or achieving a high KDA) are most beneficial for winning the game. Through this analysis, we aim to identify which early game events significantly impact the overall win rate.

The columns we are interested in to answer our question include: “event1”, “event2”, “event3”, “blueJungleGP”, “blueJungleKDA”, “redJungleGP”, “redJungleKDA”, and “result”. These columns provide information about the early game events, jungle performance, and the final result of each match. By analyzing these columns, we can determine the influence of specific events on the game's outcome.

Columns: 
* game: Game ID of the player
* event1: The first significant event in the game, such as the first tower taken or first blood.
* event2: The second significant event in the game.
* event3: The third significant event in the game.

* blueJungleKDA: Kill-Death-Assist ratio of the Blue team's jungler.

* redJungleKDA: Kill-Death-Assist ratio of the Red team's jungler.
* result: The final outcome of the game (1 for a win, 0 for a loss).

I created additional columns,

* First_Event_Red: Indicates whether the first event was advantageous for the Red team (1) or the Blue team (0).
* Second_Event_Red: Indicates whether the second event was advantageous for the Red team (1) or the Blue team (0).
* Third_Event_Red: Indicates whether the third event was advantageous for the Red team (1) or the Blue team (0).
* Red_More_Objectives: A boolean indicating whether the Red team secured more objectives in the first three events.


## Data Cleaning and Exploratory Data Analysis

The raw data was loaded from a CSV file containing various match statistics for professional League of Legends games. Checked for any missing values in the dataset and decided to either fill them with appropriate values or drop them based on their significance. Removed the columns that are not being used, and added several new columns.
* First_Event_Red, Second_Event_Red, Third_Event_Red: These columns were created to indicate whether the corresponding event was advantageous for the Red team (1) or the Blue team (0). This helps in understanding the impact of each event on the game's outcome.
* Red_More_Objectives: This boolean column was created to indicate whether the Red team secured more objectives in the first three events. This feature helps in analyzing if securing more objectives early in the game has a significant impact on winning.





| game                  | event1            | event2       | event3       |   blueJungleKDA |   redJungleKDA |   result |   First_Event_Red |   Second_Event_Red |   Third_Event_Red | Red_More_Objectives   |
|:----------------------|:------------------|:-------------|:-------------|----------------:|---------------:|---------:|------------------:|-------------------:|------------------:|:----------------------|
| ESPORTSTMNT03_3087499 | BLUE: first_blood | BLUE: dragon | BLUE: herald |            0    |              0 |        1 |                 0 |                  0 |                 0 | False                 |
| ESPORTSTMNT01_3309691 | BLUE: first_blood | BLUE: dragon | RED: herald  |            0    |              0 |        1 |                 0 |                  0 |                 1 | False                 |
| ESPORTSTMNT01_3311651 | BLUE: first_blood | BLUE: dragon | BLUE: herald |            0    |              0 |        1 |                 0 |                  0 |                 0 | False                 |
| ESPORTSTMNT01_3309743 | RED: first_blood  | RED: dragon  | RED: herald  |            1.56 |              0 |        1 |                 1 |                  1 |                 1 | True                  |
| ESPORTSTMNT01_3311712 | BLUE: first_blood | RED: herald  | RED: dragon  |            9    |              0 |        1 |                 0 |                  1 |                 1 | True                  |




* Univariate Charts

  In order to increase our awareness of the data, I produced an interactive pie chart using “plotly” that reprensents the percentage of the each teams taking the first, second and third objectives. 


<iframe
  src="assets/eda1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

  This pie chart shows the distribution of the First_Event_Red column, indicating whether the first event was advantageous for the Red team (1) or the Blue team (0). This visualization helps in understanding 
  the frequency of the first event being advantageous for each team and its relation to the game result. The probability of red team taking the first objectives is 39%.
  I made two more pie charts for the second and third objective as well, red team had a probability of 41% to take the second objective, and 36.8% for the third objective. This pie chart showed that Red team 
  has lower percentage of taking objectives than the Blue team.

* Bivariate Charts

  The bar chart displays the win(all objects secured) rate for the Red team when they secure the first objective. It shows the proportion of games won(perfectly securing object) when the Red team secures the   first objective, compared to the total number of games. 

<iframe
  src="assets/eda2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

I made another bar chart which displays the rate for Red team to win while not perfectly securing the first three objectives, when Red team did take the first objectives, or did not take the first objectives. Comnparing these two charts helps in understanding the significance of securing the first objective in the overall game outcome. This indicates that taking the first objectives helps team winning with all objectives secure, and they are going to have a different way other than winning by taking all objectives if the opponent team took the first objectives. 

* Interesting Aggregates

  While In the process of an interesting aggregate, I created a pivot table to show the mean of Red team taking each event are the columns, and the result of the game as the rows. It highlights the relationship between early game events and the overall game outcome, providing insights into how critical securing early objectives can be for winning the game.

  With this, the Red team tends to lose more games when the early game events (first, second, and third events) are advantageous to them. This is indicated by the lower average values for First_Event_Red, Second_Event_Red, and Third_Event_Red in games that were won (result = 1) compared to those that were lost (result = 0).


|   First_Event_Red |   Second_Event_Red |   Third_Event_Red |
|------------------:|-------------------:|------------------:|
|          0.638691 |           0.610242 |          0.56899  |
|          0.390387 |           0.410317 |          0.368113 |


## Assessment of Missingness

* NMAR Analysis
  In the context of our dataset, I believe that the event1 column could be considered Not Missing At Random (NMAR). The reasoning is that the presence or absence of certain events might depend on the outcome or nature of the game itself, rather than being random or dependent on other observed variables. For instance, if event1 refers to a significant game event like the first tower taken, it might be missing because such an event did not occur in certain games. To explain the missingness of event1 and potentially make it Missing At Random (MAR), additional data like game duration would be useful.

* Missingness Dependency
  To investigate whether the missingness of event1 depends on the result column, I performed a permutation test.
