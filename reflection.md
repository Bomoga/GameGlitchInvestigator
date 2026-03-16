# 💭 Reflection: Game Glitch Investigator

Answer each question in 3 to 5 sentences. Be specific and honest about what actually happened while you worked. This is about your process, not trying to sound perfect.

## 1. What was broken when you started?

- What did the game look like the first time you ran it?

A simple guess the number game that prompted the user to input a number between a certain range. The game has a hinting system that is intended to help the player move closer to the secret number by telling them if their number input was too low or too high.

- List at least two concrete bugs you noticed at the start  
  (for example: "the secret number kept changing" or "the hints were backwards").

The hints were not helpful, as they had kept saying "lower" even when I was typing numbers out of range. 
Even when inputting the correct answer, the game did not end.
The game could not be restarted.

---

## 2. How did you use AI as a teammate?

- Which AI tools did you use on this project (for example: ChatGPT, Gemini, Copilot)?

Claude Code, Gemini

- Give one example of an AI suggestion that was correct (including what the AI suggested and how you verified the result).

Backwards logic on the "GO LOWER!" and "GO HIGHER!" hints being corrected.
I verified this by playing the game and determining whether the hints were correct.

- Give one example of an AI suggestion that was incorrect or misleading (including what the AI suggested and how you verified the result).

A slightly misleading change in the hardcoded 1 through 100 was suggested to have been turned into constant variables, when they are supposed to change based on difficulty during runtime. I had verified that this suggestion was incorrect by switching difficulties and observing that the range was not changing.

---

## 3. Debugging and testing your fixes

- How did you decide whether a bug was really fixed?

By testing the actual game itself and identifying whether the game was playing correctly according to the specifications.

- Describe at least one test you ran (manual or using pytest)  
  and what it showed you about your code.

I played the higher/lower game and observed that the hints were correctly stating whether the target was actually higher or lower, and I eventually correctly guessed that the number was 76. Upon doing this, I restarted the game successfully and played again until I lost to observe the behavior of the game when I lost.

- Did AI help you design or understand any tests? How?

Yes, it guided me to check for certain things and edge cases that were not obvious.

---

## 4. What did you learn about Streamlit and state?

- In your own words, explain why the secret number kept changing in the original app.

Every time the user interacts with the page, the entire Python script re-runs from top to bottom. If the target was generated with a single random.randint() at the top of the script, unprotected by the session state, it would produce a new random number every time.

- How would you explain Streamlit "reruns" and session state to a friend who has never used Streamlit?

Streamlit is basically a whiteboard that gets erased and redrawn every time you interact with it. Variables get erased and reassigned along with it. The session state is essentially a sticky note you put on the side of the board, containing things that should not be erased.

- What change did you make that finally gave the game a stable secret number?

if "secret" not in st.session_state:
    st.session_state.secret = random.randint(low, high)

We ensured that the secret would only be assigned a random number if it didn't already exist in the session state.


---

## 5. Looking ahead: your developer habits

- What is one habit or strategy from this project that you want to reuse in future labs or projects?
  - This could be a testing habit, a prompting strategy, or a way you used Git.

The bugfixing feedback loop that I used with Claude would work very well with a personal project I am working on.

- What is one thing you would do differently next time you work with AI on a coding task?

Be less vague and provide more specifications to keep it grounded.

- In one or two sentences, describe how this project changed the way you think about AI generated code.

It's certainly a way to accelerate my development by reducing the amount of repetitive code I have to write, but its not perfect. It still requires revision.
