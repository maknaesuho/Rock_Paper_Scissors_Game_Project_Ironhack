# Rock, Paper, Scissors

A modular, terminal-based implementation of the classic **Rock, Paper, Scissors** game built in Python. The player competes against an automated computer opponent in a best-of-five race where the first to reach **3 wins** claims the championship.

---

## Features

* **Modular Architecture**: Built with separated helper functions coordinating input handling, computer decision logic, and score state management.
* **Input Validation**: Uses input sanitization loops to ensure only valid moves (`1`, `2`, or `3`) and replay choices (`yes` or `no`) are accepted from the player.
* **Pure State Management**: Game state (`rounds`, `player_score`, `computer_score`) is passed explicitly as parameters and returned via tuples rather than relying on global variables[cite: 1, 4].
* **Tuple Unpacking**: Passes round counts and updated score states dynamically between turns using sequence unpacking[cite: 1].
* **Instant Replay Loop**: Prompts the user to restart the game upon conclusion, cleanly resetting rounds and scores to 0[cite: 4].

---

## Game Rules

Standard Rock-Paper-Scissors mechanics determine round outcomes:
* **Rock (1)** smashes **Scissors (3)**
* **Scissors (3)** cuts **Paper (2)**
* **Paper (2)** covers **Rock (1)**
* Identical choices result in a tied round with no point awarded to either side.

---

## Project Structure

* `welcome_message()`: Introduces the player and prompts them to begin.
* `get_player_input()`: Collects and validates the player's numerical choice (`1`, `2`, or `3`).
* `get_computer_input()`: Uses Python's `random.choice()` to select a move for the computer opponent.
* `process_turn(rounds, player_score, computer_score)`: The primary round loop that tracks scores, prints play-by-play feedback, and terminates once either player hits 3 wins.
* `winner(player_score, computer_score)`: Prints the game-over screen and prompts for a replay with validation.
* `start_game()`: The coordinator function that sequences the match and manages replay flow.

---

## Getting Started

### Prerequisites
* Python 3.6 or higher (uses f-strings and standard library modules).

### How to Run

1. Clone or download this repository:
    git clone [https://github.com/your-username/rock-paper-scissors.git](https://github.com/your-username/rock-paper-scissors.git)
    cd rock-paper-scissors