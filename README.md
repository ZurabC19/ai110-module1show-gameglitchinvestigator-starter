# 🎮 Game Glitch Investigator: The Impossible Guesser

## 🚨 The Situation
You asked an AI to build a simple "Number Guessing Game" using Streamlit.
It wrote the code, ran away, and now the game is unplayable. 
- You can't win.
- The hints lie to you.
- The secret number seems to have commitment issues.

## 🛠️ Setup
1. Install dependencies: `pip install -r requirements.txt`
2. Run the broken app: `python -m streamlit run app.py`

## 🕵️‍♂️ Your Mission
1. **Play the game.** Open the "Developer Debug Info" tab in the app to see the secret number. Try to win.
2. **Find the State Bug.** Why does the secret number change every time you click "Submit"? Ask ChatGPT: *"How do I keep a variable from resetting in Streamlit when I click a button?"*
3. **Fix the Logic.** The hints ("Higher/Lower") are wrong. Fix them.
4. **Refactor & Test.** - Move the logic into `logic_utils.py`.
   - Run `pytest` in your terminal.
   - Keep fixing until all tests pass!

## 📝 Document Your Experience

**Purpose:** This is a number guessing game where the player tries to guess a secret number within a limited number of attempts. The difficulty setting controls the range of numbers and how many attempts you get.

**Bugs Found:**
- The hints were inverted — guessing too high told you to go higher, and too low told you to go lower.
- The secret number kept changing on every button click because it wasn't stored in session state.
- The Normal and Hard difficulty ranges were swapped in `get_range_for_difficulty`.
- The "New Game" button was resetting attempts to 0 instead of 1, and hardcoded the range to 1–100 regardless of difficulty.
- On even-numbered attempts, the secret was randomly converted to a string, breaking the comparison in `check_guess`.

**Fixes Applied:**
- Stored the secret number in `st.session_state` so it persists across reruns.
- Fixed the hint messages in `check_guess` by removing the buggy string-comparison fallback.
- Corrected the difficulty ranges so Normal is 1–50 and Hard is 1–100.
- Fixed the "New Game" button to properly reset all state and use the correct difficulty range.
- Refactored all game logic out of `app.py` into `logic_utils.py` and imported it.

## 📸 Demo
<img width="2543" height="1243" alt="image" src="https://github.com/user-attachments/assets/d1b81793-c10b-44d0-b41c-47c94faf6469" />



