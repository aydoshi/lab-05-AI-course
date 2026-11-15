# Lab 05 — Conclusion

<!--
Read this before you write.

This file is graded by your instructor, by hand, and it is worth 6 of the 15 points.

- Type it yourself. Do not use a chatbot, an AI assistant, an AI autocomplete or a "rewrite my
  text" tool for any part of it, not even for grammar. English that is plain and a little
  clumsy but yours is better than polished text that is not.
- Use your own numbers. Every number you quote must be one your own notebook printed. Copy
  the number exactly as it appeared. A number your notebook did not print is marked as wrong.
- Answer in your own words, about 80-200 words per question. A short answer that uses your
  numbers beats a long answer that could have been written by anyone.
- Delete these comment lines if you like. Keep the three headings and the last line.
-->

## 1. Which layer changed your results the most?

Give the numbers before -> after for that layer (correct / wrong / no answer, out of 20) and say
whether it changed what the agent *can do* or only what it *admits*. If no layer changed the
number of correct answers, say so and explain what the layers did change instead.

Answer: We can see that there is after using layer 1 correct answers increased from 16 to 18 and after layer 1 in layer 2 and 3 no difference between correct answers. after using layer 1 wrong answers increased from 4 to 6 and no answer decreased from 4 to 0. This enabled agent to recover from errors and make further attempts.
Output from Colab -> 
bare           correct 16/24  wrong  4  no answer  4  95% [0.47, 0.82]  model calls  51  tokens  39536  seconds   98.3
layer 1        correct 18/24  wrong  6  no answer  0  95% [0.55, 0.88]  model calls  62  tokens  48708  seconds  106.5
layer 2        correct 18/24  wrong  6  no answer  0  95% [0.55, 0.88]  model calls  62  tokens  48708  seconds  102.3
layer 3        correct 18/24  wrong  4  no answer  2  95% [0.55, 0.88]  model calls  74  tokens  60116  seconds  112.5

the first thing that went wrong in each run, counted:
bare           {'no_answer_line': 7, 'bad_args': 4}
layer 1        {'no_answer_line': 7, 'bad_args': 4}
layer 2        {'no_answer_line': 7, 'bad_args': 4}
layer 3        {'no_answer_line': 7, 'ungrounded': 1, 'bad_args': 4}

## 2. One failure the full harness did not fix

Pick one question that the full harness (layer 3) still gets wrong or refuses. Give its id
(q01 ... q20). Open its trace in the notebook: at which step did it go wrong, and what did
the model do instead? Name one thing you would add to the harness, and what it would cost
(extra model calls, tokens, time, or a new way to fail).

Answer: q18. The calculation went wrong. Model calculated: tool   calculate({"expression": "(16.1 - 10.6)/100"}) -> ok: {"result":0.055}
  model: ANSWER: 0.55 percentage points. after we see:   harness: Your answer is not supported by the tool results: the number 0.55 is not in any tool output. Use tool results; if the value comes from arithmetic, compute it with the calculate tool. If the data does 
so i would add a layer that checks the final answer with the result of calculator.


## 3. Workflow or agent for the monthly ranking?

Dala Insight wants to publish, every month, "which region is highest and which is lowest on one
indicator in one year". Would you ship the fixed workflow or the agent? Use the accuracy, the
number of model calls, the tokens and the time you measured in Part 1. Then say in one sentence
what kind of question would make you choose the other one.

Answer: I would choose fixed workflow, because its just better in any aspect: accuracy, token usage, model calls. But I would choose the agent for tasks when we need multiple steps or calculation and something like that

Output from Colab->
the 15 fixed-shape questions:
workflow       correct 13/15  wrong  0  no answer  2  95% [0.62, 0.96]  model calls  15  tokens   3852  seconds   17.7
agent (bare)   correct  9/15  wrong  2  no answer  4  95% [0.36, 0.80]  model calls  26  tokens  19835  seconds   53.8

---

I wrote this file myself, without any AI tool.
