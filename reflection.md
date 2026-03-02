# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

There were a good number of bugs in the initial app. The hints seem to be inverted, so whenever you pick a number that is higher than the answer, the hint tells you to go higher; the inverse applies. There is always an extra attempt left when the game finishes.  The score can go negative (not sure if intended). The range description based on difficulty doesn't match the actual range given in-game. Submit button is not responsive.

---

## 2. How did you use AI as a teammate?

I used GitHub Copilot inside VS Code as my main AI tool on this project.

Correct suggestion: I highlighted the `check_guess` function and used Copilot inline chat to ask why the hints were wrong. Copilot correctly identified the buggy `TypeError` fallback block that compared strings instead of integers, causing the hints to be flipped. I verified this by fixing the function and running the game manually, guessing too high now correctly showed "Go LOWER".

Incorrect/misleading suggestion: When I asked Copilot to fix the import in `test_game_logic.py`, it suggested using `from ..logic_utils import check_guess` (a relative import). This caused an ImportError when I ran `pytest`. I caught the mistake by reading the error message in the terminal, and had to manually change it to use `sys.path.insert` instead to point Python to the right folder.


---

## 3. Debugging and testing your fixes

I decided a bug was fixed when both pytest and the live Streamlit game confirmed the correct behavior. I ran three pytest tests in `test_game_logic.py` targeting the hints bug, for example, checking that guessing 60 against a secret of 50 returns "Too High" with "LOWER" in the message, and all three passed after the fix. I also manually played the game after each fix to make sure the hints looked right in the actual UI. Copilot helped me understand what to assert in each test, but I chose the specific test values myself.

---

## 4. What did you learn about Streamlit and state?

In the original app, the secret number kept changing because every time the user interacted with anything on the page, Streamlit would rerun the entire script from top to bottom, generating a brand new random number each time. Streamlit reruns are like refreshing the page, every button click or input triggers the whole file to execute again, so anything not saved will reset. Session state is like a notebook Streamlit keeps on the side that survives these reruns, so you can store values like the secret number and they won't get wiped. The fix was wrapping the secret number generation in an `if "secret" not in st.session_state` check, so it only generates once and stays stable for the rest of the game.

---

## 5. Looking ahead: your developer habits

One habit I want to reuse is writing pytest tests right after fixing a bug, so I have proof the fix actually works and didn't break anything else. Next time I work with AI on a coding task, I would test every suggestion before accepting it instead of assuming it's correct, since Copilot gave me a broken import that I had to catch myself. This project made me realize that AI generated code can look completely reasonable and still have subtle bugs baked in, so reading and understanding the code yourself is just as important as getting it to run.
