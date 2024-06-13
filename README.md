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
  
* Null Hypothesis (H0): The missingness of event1 is independent of the game result.
* Alternative Hypothesis (H1): The missingness of event1 is dependent on the game result.

I used the difference in proportions of missing event1 between games that were won and games that were lost as an test statistics.
  
  <iframe
  src="assets/NMAR.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


Observed Difference: 0, 
P-value: 1

Observed difference indicates that there were no difference in the result of the game when there is a missingness of event1. With a P-value of 1, we fail to reject the null hypothesis, suggesting that the missingness of event1 is not significantly dependent on the game result.
This also means that the game competition takes a good care of preventing the unknown accidents during the game, so it does not control the result of the game. By performing this analysis, I was able to gain insights into whether the missingness of event1 is potentially NMAR and consider additional data that might help transform it to MAR.


## Hypothesis Testing

There were no missing values in the data I used. 
* Null Hypothesis: Teams that took advantages in the first three events are equally likely to win compared to teams that did not.
* Alternative Hypothesis: Teams that took advantages in the first three events are more likely to win compared to teams that did not.

The Null and Alternative Hypothesis came from the idea to figure out if the first three events are significant for the team winning to get to know about the relationship between objectives and game results. The test statistic was the difference between the game winning when took advantages in the first three events, and the game winning without taking advantages in the first, in a significance level of 5%.

Result: observed differnce: 0.3 p-value = 1, fail to reject the null hypothesis. The observation we saw in our data did not happen due to random chance, so taking advantages in first three events is not related to winning the game.

## Framing a Prediction Problem

Type: Classification (Binary Classification)

Prediction Problem: Predict whether a team wins the game based on their performance in the jungle laner's KDA and the first three events.

Response Variable: The response variable is result, which indicates whether the team won (1) or lost (0) the game. This binary outcome is crucial for understanding the effectiveness of early game advantages in determining the final outcome of the game.

Evaluation Metric: F1-score

Reason for Choosing F1-score:

* Imbalance Handling: In competitive games, the distribution of wins and losses may not be perfectly balanced. The F1-score, which is the harmonic mean of precision and recall, is more informative for imbalanced datasets than accuracy, as it considers both false positives and false negatives.
* Model Performance: It provides a better measure of the incorrectly classified cases than the accuracy metric, especially when the class distribution is skewed.

At the "time of prediction," we use information from the first three events, which are part of the early game. This ensures that our model is practical and can be applied in real-time scenarios, where decisions and predictions need to be made based on the ongoing game's current state.

In this classification problem, we're predicting whether a team will win based on the jungle laner's performance early game events. We use features available at the time of prediction to ensure the model's practicality. The F1-score is chosen as the evaluation metric due to its suitability for potentially imbalanced datasets, providing a balanced measure of precision and recall.

## Baseline Model 

Model Type: Random Forest Classifier

# Features
Categorical Features: event1(Encoded using OneHotEncoder)

Quantitative Features: Red_More_Objectives(Binary indicator if the Red team had more objectives in the first three events), redJungleKDA(KDA score for the Red team's jungler.)

F1-score: 0.645

I believe my current model is good since it would catch if it is the jungle laner who contributes the most to loss of both objectives and a game, however, with a importance of 0.8 in redJungleKDA, I would like to add the difference between the KDA of the jungle laners in each team for a better prediction. 

## Final Model

Model Type: Random Forest Classifier

# Hyperparameters that worked the best

Number of Trees (n_estimators): Controls the number of trees in the forest.

Maximum Depth (max_depth): Controls the maximum depth of the trees.

Minimum Samples Split (min_samples_split): The minimum number of samples required to split an internal node.

# Features

Categorical Features: event1(Encoded using OneHotEncoder)

Quantitative Features: Red_More_Objectives(Binary indicator if the Red team had more objectives in the first three events), redJungleKDA(KDA score for the Red team's jungler),Total_Objectives(Sum of blueJungleGP and redJungleGP),KDA_Difference(Difference between blueJungleKDA and redJungleKDA)

F1-score: 0.695(increased from 0.65)

Conclusion
I decided to add the Total_Objectives since I am trying to find the relation between the objectives and the game result in a bigger pie. Before I built the baseline model, the first three objectives were not significant to the result of the game, so I started thinking about the position related to taking objectives which is jungle laner. I added the columns comparing the KDA of the jungle laners in each team so it could include the part that was never brought up before, and was found highly important. By adding new features (Total_Objectives and KDA_Difference) and the best working the hyperparameters, the final model is expected to improve upon the baseline model. The pipeline ensures that all preprocessing steps and model training are performed in a single step, making the process efficient and reproducible.


## Fairness Analysis

Group X: Teams with a high redJungleKDA (above the median value).

Group Y: Teams with a low redJungleKDA (below or equal to the median value).

Evaluation Metric: F-1 Score


Hypotheses
* Null Hypothesis (H0): The model's F1-score for high redJungleKDA teams and low redJungleKDA teams are roughly the same, and any differences are due to random chance.
* Alternative Hypothesis (H1): The model's F1-score for high redJungleKDA teams is higher than its F1-score for low redJungleKDA teams.

* Test Statistic: The difference in F1-scores between high redJungleKDA and low redJungleKDA teams.
* Significance Level: 0.05

p-value: 0.99

Observed Difference: 0.13817487933550343

We fail to reject the null hypothesis, with a p-value of 0.99, which indicates the Jungle laner's performance do not effect the result of the game. This concludes to that our model was fair, and the jungle laner's performance do not effect the game result.
