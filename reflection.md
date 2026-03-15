# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?
- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").

**Ans:** The game initially ran with mismatched difficulty ranges, confusing hints, incorrect scoring, and restart logic that reused the wrong range, status, and guess history.

Two concrete starting bugs were:

- The Hard difficulty used the same range as Normal (1–50 instead of 1–200), so it was not actually harder.

- The hint messages were reversed, telling you to go higher when your guess was already too high, and lower when it was too low.
 
---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?
- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).
- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

**Ans:** I used Sonnet 4.6 as an AI teammate on this project. It mainly helped me reason about bugs and propose code fixes.

Correct AI suggestion
- The AI correctly identified that wrong guesses were sometimes adding points instead of deducting them on even-numbered attempts.

- It suggested changing the scoring so that every incorrect guess always deducts 5 points from the score, regardless of attempt number.

I verified this by playing multiple rounds, intentionally guessing wrong on several attempts (including even attempts) and confirming that the score consistently dropped by 5 points each time.

Incorrect AI suggestion
- At one point, the AI took control of the solution design midway, proposing changes beyond what I asked for.

- It started assuming extra behaviors, like generating fixes that could be a lot simpler and fixing unrelated parts of the code that were already working.

I verified these suggestions were misleading by running the modified game, noticing new unexpected behavior, and then rolling back those changes to restore the intended logic.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?
- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.
- Did AI help you design or understand any tests? How?

**Ans:** I treated a bug as fixed only after I could rerun the game and see the behavior consistently match what I expected in multiple tries.

How I tested my fixes  
- I tested manually by running the game, trying different guesses on each difficulty, and checking that the score, attempts, hints, and ranges all updated with the correct values after each input.
- I also tried using pytest. I asked AI to generate some basic test functions for my game logic, ran those tests in pytest, and confirmed they all passed, which gave me extra confidence that the core functions were working.

How AI helped with tests  
- AI helped me design tests by suggesting changes that i didnt know of and by writing example pytest functions that I could paste and run.
- It also explained in detail what each test was checking and how it related to my code changes, which made it easier for me to understand pytest even though I was unfamiliar with it.
---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.
- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?
- What change did you make that finally gave the game a stable secret number?

**Ans:** The secret number kept changing because the app was running the whole script again on every click and calling random.randint each time, without saving that value anywhere that persisted. When Streamlit reruns, normal variables like secret = random.randint(...) are recalculated on every run, so the target number kept getting replaced. To fix this, I stored the secret in st.session_state and only set it once, when "secret" didn’t exist yet. Now the secret number stays the same across reruns and only changes when I start a new game.

---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.
- What is one thing you would do differently next time you work with AI on a coding task?
- In one or two sentences, describe how this project changed the way you think about AI generated code.

**Ans:** One habit I want to reuse is setting up a virtual environment and basic pytest tests, and I also practiced using clearer commit messages in Git, which made it easier to track changes and keep the project organized. I also improved my prompting by giving the AI more context and asking it to explain changes, which I want to keep doing in future labs.

Next time, I’d be more strict about reviewing AI suggestions, treating them as drafts instead of final answers, and double-checking them with tests or manual runs before accepting them. I’d also try to limit how much the AI refactors everything at once and instead ask for smaller, focused changes so the code stays understandable.

This project made AI-generated code feel overpowerful but also risky as it can speed things up a lot, but it still needs human judgment, testing, and review to be trustworthy. I expect to read, test, and adjust its output instead of just pasting it in.