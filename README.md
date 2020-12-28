# Resume-Project
Baseball Simulation made for Computational Modeling Fall 2020

# Set-up  
1. Download player stats Excel File & Download code as .py - save in same location 
2. Run code (use Spyder as part of the Anaconda environment for best results - any REPL that can accept input will work)

# Play! 
1. Pick your teams as prompted and change batting order for players if desired - stats are from 2019 
2. Pick number of games to run (1 will give you more specific results & more than one will be aggregates)
3. Run the simulation and view results

# How to Use It:  
- Sports betting for upcoming games 
- Hypothetical game matchups
- Edit the player stats Excel file to see how a slight change in player performance will affect the team
- Try to find the best line up for a team

# Assumptions: 
1. The opposing team’s pitching is not factored into scoring. This is the most significant constraint since a player's batting averages will be affected by the skill of the opposing team’s pitching. 
However, using an average accounts for games against many types of pitchers, so it was intended to not under or over predict the results to a great extent. In a future model, having a factor to scale up or down player’s batting averages depending on the opponent would be one way to account for this and retain the structure of the current code. 
2. Games end in a tie if they don’t have equal scores. 
3. Players on base advance as far as the batter does. This assumption means that if a batter hits a single, all players on base move forward by 1. This is a reasonable assumption since that is generally what happens. But, it is not a rule. There are many scenarios where players will be able to move more than the batter and this is not accounted for. 
4. Stealing bases and errors are not factored in. 

# Functions Used: 
1. Choosing Teams: This function inputs a default line up from whichever home or away team the user selected as a list. It then allows the user to update that list by spelling out player names in order of 1 - 9. No repeats are allowed and the code is resilient to any spelling errors or mistakes by using while loops to force an acceptable input. It also has helpful prompts for the user and displayers character stats initially to let them see the full roster before deciding their lineup. 

2. Simulate Inning: The inning function is the center of the code since it runs most of the actual baseball game. It inputs the number of outs and inning number. The player list, and the starting player number. It initializes data frames to track the player stats and inning states and the initializes variables to set the start of the game with clean bases, 0 outs, and 0 runs. Pandas data frames were selected since they can be sliced and updated or appended to easily and cell values can be called both directly and indirectly. There is a while loop and then a for loop that run repeatedly and move “players” around the bases by updating a dictionary until the max number of outs is reached. The while loop is to account for starting with a player in the middle of a line up (while player number < 9, perform play, then player += 1). When 9 is reached, the code enters the for loop and starts back at 0. This for loops repeats until the max outs is reached. Inside the loop, random choice is used to determine which of 6 plays a batter will do. After that play is determined, a series of for loops check how the bases dictionary needs to be updated. This continues until 3 outs are reached signaling the end of an inning. After 3 outs, an inner loop is entered and the inning stats data frame is updated for that round and any inning-specific variables like number of runs are reset. Inning_num is an important variable in this inner loop that ensures the loop only breaks 1x per 3 outs. If the loop was only triggered by # outs % 3 == 0, then it would be entered multiple times after it reaches 3 before moving to 4. To prevent this, inning_num starts at 1 and is incremented every time the inner loop is reached. The logic is that if a multiple of 3 outs is reached and it is time for the next inning (so outs / 3 == inning_num), enter the smaller loop. This ensures each inning is given a fresh start. Throughout all the loops, current player number is continuously updated since it is a necessary input later on in the code. 

3. Game Function: This portion of the code is the setup for a standard baseball game. The user inputs the number of games as the most significant variable into this equation. It first sets up two data frames to track statistics and scores throughout each iteration and then plays away for 27 outs and home for 24 before deciding on the last half inning. It then updates the data frames for the 1st game and continues running and updating until the number the user specified is reached. It outputs the statistics that are returned to the user. 
Because the inning function tracks player statistics are not reflected in the output if there are multiple games played, the game function directly prints those data frames to the user if the number of games is only 1. This is the only scenario in which this occurs because currently the player statistics are not individually tracked across all games. This could be done in future versions of the code, but it would likely be similar to the inputted batting averages from the historic data and might not offer new insight. 


# Model Evaluation: 

To evaluate that the model was running as intended, many games were run only once and each play was printed to the screen and manually tracked for scoring. The logic of the model did hold up under this test, so it was assumed to be sound for many repeated games. Additionally, the results for many iterations were compared with actual statistics like runs per game and it was often close to the season averages by team. However, some statistics were off with very high or low results such as unreasonably high home runs per season and unusually low number of triples hit. This is the nature of using statistics with no outside factors, some results will be well beyond the range of a normal game simply because they are statistically possible.
Overall, the logic was sound within the assumption limitations, and the statistical irregularities were as expected, so the model was acceptable for the scope of the project.

# Contact 
You can reach me at linkedin.com/in/veronica-carmody with questions or comments - thank you :) 
