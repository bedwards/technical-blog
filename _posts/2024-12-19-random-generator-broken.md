---
---
# Why Your Random Number Generator Isn't

Computer random numbers are like professional wrestling - entertaining and mostly convincing until you look too closely. At 21CT, we were using `rand()` for generating session tokens until someone noticed that users logging in at the same second got the same "random" token. It was like a lottery where everyone who bought tickets at the same time won the same prize.

The problem is that computers are deterministic machines trying to pretend they're chaotic. It's like asking an accountant to be spontaneous - they'll try, but it's going to follow a very predictable pattern. Even "cryptographically secure" random number generators are just really good at hiding their patterns, like a magician who's very good at sleight of hand but is still following a script.

My favorite random number bug was in a card game where the shuffle was using the timestamp as a seed. Players figured out they could predict the deck by checking their computer's clock, turning poker into a memory game. We fixed it by using a proper entropy source, but for a brief period, we had accidentally created a game where the best poker players were the ones with the most accurate clocks. Sometimes bugs create more interesting gameplay than features.

