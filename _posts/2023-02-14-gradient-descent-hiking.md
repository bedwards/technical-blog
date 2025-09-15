---
---
# Gradient Descent Is Just Hiking Backwards in the Dark

When I explain gradient descent to people, I tell them to imagine they're blindfolded on a hillside, trying to find the lowest point by taking tiny steps downhill. Except you're not actually on a hill, you're in some horrible N-dimensional space where N is usually in the thousands, and also the hill keeps changing shape while you're walking on it. Oh, and sometimes there are fake valleys that seem low but aren't really.

The learning rate is basically how big your steps are, and choosing it is like Goldilocks except if you get it wrong your model explodes or takes until the heat death of the universe to train. Too high and you're bouncing around like a pinball, overshooting every minimum. Too low and you're moving so slowly that you'll still be training when your grant funding runs out. The sweet spot is this narrow band where things actually work, which you find through the scientific process of trying random numbers until something doesn't break.

What really breaks my brain is adaptive learning rates like Adam, which is basically gradient descent with memory and momentum. It's like if you were hiking and your steps got automatically smaller when you've been going uphill a lot, and you had a tendency to keep going in whatever direction you were already going. It works incredibly well, but nobody really knows why, which is very on-brand for deep learning - we've built these mathematical Rube Goldberg machines that somehow produce intelligence, and we're all just pretending we understand them.

