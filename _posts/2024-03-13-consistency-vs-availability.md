---
---
# The Eternal Struggle Between Consistency and Availability

The CAP theorem is like being told you can have a good job, a good relationship, or good health - pick two. Every distributed system eventually has to choose between being consistent (everyone sees the same data) or available (the system keeps working), and watching architects pretend they can have both is like watching someone try to be in two places at once.

At Bitbucket, we chose availability, which meant sometimes users would push code that would disappear for a few seconds then reappear, like a magic trick nobody asked for. We called it "eventual consistency" which is a fancy way of saying "it'll be right eventually, please stop asking when." Users would refresh frantically, watching their commits flicker in and out of existence like Schrödinger's code. The support tickets were amazing: "My code exists when I look at it from my laptop but not from my phone."

The alternative was choosing consistency, which meant the entire system would freeze when we couldn't reach consensus, like a group of friends trying to decide where to eat dinner. We tried this briefly and discovered that users prefer a lying system to a frozen one. It's like asking someone if they'd rather be told comforting lies or uncomfortable truths - everyone says they want truth until the system is down and they can't deploy their urgent fix. Now we just aim for "mostly consistent, usually available" which isn't academically rigorous but keeps everyone slightly unhappy rather than completely furious.

