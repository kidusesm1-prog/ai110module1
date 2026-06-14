## 1. What was broken when you started?

* The game loaded normally at first, but the behavior became inconsistent after a few guesses.
* The hint system was backwards.
* Correct guesses sometimes failed because the secret number was converted into a string.
* The New Game button did not fully reset the game state.

**Bug Reproduction Log**

| Input                                     | Expected Behavior                       | Actual Behavior                                                          | Console Output / Error |
| ----------------------------------------- | --------------------------------------- | ------------------------------------------------------------------------ | ---------------------- |
| Guess higher than the secret number       | Hint should say "Go LOWER"              | Hint said "Go HIGHER"                                                    | None                   |
| Correct guess on an even-numbered attempt | Game should register a win              | Correct guess failed because the secret number was converted to a string | None                   |
| Click "New Game" after winning or losing  | Game should fully reset and start fresh | Status, score, and history were not fully reset                          | None                   |

---

## 2. How did you use AI as a teammate?

* I used ChatGPT and the AI assistant in VS Code.
* A correct AI suggestion was that the hint logic in `check_guess()` was reversed.
* I verified that by testing guesses above and below the secret number.
* One misleading suggestion was treating the issue mostly as a Streamlit state problem. The actual code also had a type bug where the secret number was changed into a string.

---

## 3. Debugging and testing your fixes

* I tested each bug by reproducing it first, then checking if it disappeared after the fix.
* I manually tested guesses below, above, and equal to the secret number.
* I also tested the New Game button after winning to make sure attempts, score, history, status, and the secret number reset.
* Finally, I ran `python -m pytest tests/test_game_logic.py`, and all 3 tests passed.

---

## 4. What did you learn about Streamlit and state?

* Streamlit reruns the script from top to bottom whenever the user interacts with the app.
* `st.session_state` lets the app remember values between reruns.
* Without session state, the game would forget the secret number, score, attempts, and history after each button click.
* I would explain session state as the app’s memory while the user is playing.

---

## 5. Looking ahead: your developer habits

* I want to reuse the habit of writing down bugs before fixing them.
* Listing the input, expected behavior, and actual behavior made debugging easier.
* Next time, I would ask AI more focused questions instead of asking it to fix too much at once.
* This project showed me that AI-generated code can look correct while still having serious logic bugs, so every fix needs to be tested.
