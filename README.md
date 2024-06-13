# Objectives-predict


By Justin Seo
## Introduction

Our dataset comprises all professional League of Legends games that took place in 2023. This dataset includes various match statistics, focusing on specific events and overall performance metrics. The dataset is extensive, containing detailed information on each game's events, team performances, and outcomes.

Our primary question is: “How do specific early game events impact the likelihood of a team winning?” By addressing this question, we aim to provide insights into the critical events that can shift the balance of a game. Understanding these key events can help teams strategize better and improve their chances of winning.

Although the data does not explicitly indicate the impact of each event, we can infer this information from columns such as “event1”, “event2”, “event3”, “blueJungleKDA”, “redJungleKDA”, and the final “result” of the game.

League of Legends is a complex game where early game advantages can snowball into a decisive victory. Players and coaches often debate which early game actions (like securing the first tower or achieving a high KDA) are most beneficial for winning the game. Through this analysis, we aim to identify which early game events significantly impact the overall win rate.

The columns we are interested in to answer our question include: “event1”, “event2”, “event3”, “blueJungleGP”, “blueJungleKDA”, “redJungleGP”, “redJungleKDA”, and “result”. These columns provide information about the early game events, jungle performance, and the final result of each match. By analyzing these columns, we can determine the influence of specific events on the game's outcome.

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
