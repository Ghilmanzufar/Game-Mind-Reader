## Mind Reader Game
**Mind Reader is a game where you play against the computer, similar to the rock-paper-scissors concept. You can choose either 1 or 0, and the computer will try to guess your choice using machine learning. The first one to reach 10 points wins!**

# Game Idea
In this game, you and the computer take turns guessing each other's choices. The game flow is simple:
- You choose either 1 or 0.
- The computer attempts to guess your choice based on your previous choices.
- If the computer guesses correctly, it scores a point. If it guesses wrong, you score a point.
- The first player to reach 10 points is declared the winner.
# Features
- Player and Computer Guessing: You make a choice (1 or 0), and the computer tries to predict it using statistical probabilities based on your history of previous choices.
- Scoreboard: Tracks both your score and the computer's score in real time using progress bars.
- Game Over Message: Displays a win or lose message at the end of the game based on the result.
- Simple Machine Learning: The computer uses a simple probability-based model (binomial distribution) to make its guess.
# Game Interface
The game interface consists of:
- Two buttons: One for choosing 0 and one for choosing 1.
- Scoreboard: Displays the current scores of both the player and the computer.
- Final Message: Shows a "You Win!" or "You Lose!" message depending on the outcome of the game.
# Tools & Libraries Used
- ipywidgets: For creating interactive widgets such as buttons and progress bars.
- NumPy: For generating random predictions from a binomial distribution for the computer's guesses.
# How the Game Works
- Choose a Number: You select either 0 or 1 by clicking the corresponding button.
- Computer Guesses: Based on your previous choices, the computer tries to predict your next choice using a probability model.
- Score Update: If the computer guesses correctly, it scores a point. Otherwise, you score a point.
- End of Game: The game continues until either the player or the computer reaches 10 points. A final message is displayed at the end indicating the winner.
# Code Breakdown
1. Importing Libraries:
    ```
    from ipywidgets import *
    import numpy as np
    ```

2. Creating Buttons: Two buttons allow the user to make their choice (0 or 1).
    ```
    btn_zero = Button(description='0')
    btn_one = Button(description='1')
    btns = HBox([btn_zero, btn_one])
    ```
3. Scoreboard: Two progress bars track the scores of both the user and the computer.
    ```
    usr_score = IntProgress(value=0, min=0, max=10, description='You:', bar_style='success')
    bot_score = IntProgress(value=0, min=0, max=10, description='Bot:', bar_style='danger')
    scoreboard = VBox([usr_score, bot_score])
    ```

4. Game Over Message: A final message is displayed at the end of the game, indicating whether the player won or lost.
    ```
    final_msg = HTML("<h1 style='color:green'> You Win!</h1>")
    final_msg.layout.visibility = 'hidden'
    ```
5. Game Box: All widgets (buttons, scoreboard, and final message) are placed in a game box.
    ```
    game_box = VBox([HBox([scoreboard, final_msg]), btns])\
    ```
6. Updating the Game Logic: The game updates after each choice. The computer guesses based on the user's previous choices and updates the scores accordingly.
    ```
    def update_game(usr_choice):
        prob = sum(usr_history) / len(usr_history)
        comp_choice = np.random.binomial(1, prob, 1)[0]
        usr_history.append(usr_choice)
    
        if comp_choice == usr_choice:
            bot_score.value += 1
        else:
            usr_score.value += 1
    
        if usr_score.value == 10 or bot_score.value == 10:
            if bot_score.value == 10:
                final_msg.value = "<h1 style='color:red'> You Lose!</h1>"
            final_msg.layout.visibility = "visible"
            btn_zero.disabled = True
            btn_one.disabled = True
    ```
7. User Interaction: The game listens for clicks on the buttons to update the game state.
    ```
    btn_zero.on_click(lambda b: update_game(0))
    btn_one.on_click(lambda b: update_game(1))
    ```
## How to Play
1. Clone the repository:
    ```
    git clone https://github.com/yourusername/mind-reader-game.git
    ```
2. Install the required libraries:
    ```
    pip install ipywidgets numpy
    ```
3. Run the game in a Jupyter Notebook:
    ```
    jupyter notebook
    ```
4. Open the game-engine.ipynb file and run the cells to start the game.

# Enjoy the game!

