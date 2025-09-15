---
---
# The False Promise of Horizontal Scaling

"Just add more servers" is the distributed systems equivalent of "just print more money" - it sounds great until you understand the implications. At Atlassian, we tried to scale horizontally and discovered that our bottleneck wasn't CPU or memory - it was the single MySQL database that every server was talking to. Adding more servers just meant more connections fighting over the same database lock. It was like solving traffic by adding more cars.

The coordination overhead of horizontal scaling is what they don't tell you in the architecture diagrams. Every server needs to know about every other server, they need to agree on who's doing what, and they need to share state somehow. You've basically created a distributed system where before you had a simple one. It's like solving your relationship problems by getting into a polyamorous relationship - technically you've addressed the issue, but you've created seventeen new ones.

My favorite horizontal scaling failure was when we added auto-scaling that would spin up new instances based on CPU usage. But the instances took five minutes to warm up, during which they'd consume maximum CPU. This would trigger more instances to spin up, which would also consume maximum CPU while warming up. We accidentally created a positive feedback loop that would spawn instances until we hit our AWS spending limit. It was like a bacteria culture that grew until it ran out of petri dish.

