# 🪨 📄 ✂️ Rock, Paper, Scissors Championship

An interactive, terminal-based Rock, Paper, Scissors tournament engine built with Python. The game pits a human player against a randomized computer opponent in a best-of-series match, tracking match metrics dynamically through a centralized state dictionary until someone scores 3 points.

---

## 🎮 Game Rules & Logic

The game follows standard competitive Rock, Paper, Scissors rules:
* **Rock (1)** smashes **Scissors (3)**
* **Scissors (3)** cuts **Paper (2)**
* **Paper (2)** covers **Rock (1)**
* Matching choices result in a **Tie** (no points awarded).

The first participant to reach **3 points** is crowned the champion.

---

## ⚙️ Architecture & Key Features

* **Centralized State Management:** Game metrics are tracked using a single `game_state` dictionary (`{"rounds": 0, "player_score": 0, "computer_score": 0}`). This avoids relying on global variables and eliminates complex tuple unpacking between turns.
* **Modular Function Design:** Separates discrete gameplay responsibilities across dedicated helper functions:
  * Input collection & validation
  * Randomized move generation
  * Turn execution & score mutation
  * Tournament outcome determination
* **Robust Input Sanitization:**
  * Move inputs validate strictly against available numeric options (`1`, `2`, or `3`), reprompting on invalid or non-numeric entries without crashing.
  * The endgame replay prompt enforces a strict `yes`/`no` validation loop.
* **Automated Rematch Cycle:** When a player opts to play again, a clean `game_state` instance is initialized, resetting round counters and scores to zero automatically.

---

## 🧩 Program Workflow

```text
START GAME (start_game())
   │
   ├──> Initialize game_state = {"rounds": 0, "player_score": 0, "computer_score": 0}
   ├──> Display welcome banner (welcome_message())
   │
   ├──> Call process_turn(game_state)
   │     │
   │     └──> WHILE game_state["player_score"] < 3 AND game_state["computer_score"] < 3:
   │             │
   │             ├──> Prompt player move -> get_player_input() (validates 1, 2, or 3)
   │             ├──> Generate computer move -> get_computer_input() (random.choice)
   │             ├──> Increment round: game_state["rounds"] += 1
   │             │
   │             ├──> Evaluate Round Outcome:
   │             │       ├── Move match -> Tie (no points awarded)
   │             │       ├── Player wins -> game_state["player_score"] += 1
   │             │       └── Computer wins -> game_state["computer_score"] += 1
   │             │
   │             └──> Print live round summary and current scoreboard
   │
END OF TOURNAMENT LOOP
   │
   ├──> Return updated game_state dictionary
   │
   └──> Call winner(game_state)
         │
         ├──> Announce final outcome:
         │       ├── game_state["player_score"] == 3 -> Victory banner
         │       └── game_state["computer_score"] == 3 -> Defeat banner
         │
         └──> Prompt for Replay:
                 │
                 ├──> Validate input (reprompt until "yes" or "no")
                 ├──> If "yes" -> start_game() (launches new match with fresh state)
                 └──> If "no"  -> Exit cleanly ("Thanks for playing!")
