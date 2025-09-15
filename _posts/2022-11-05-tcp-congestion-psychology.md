---
---
# Why TCP Congestion Control Is Actually a Psychology Experiment

TCP congestion control is what happens when you try to solve a game theory problem with network packets. The whole system is based on this gentleman's agreement where everyone promises to slow down when things get congested, like drivers merging onto a highway. Of course, just like with driving, there's always that one implementation that decides the rules don't apply to them.

The beauty of algorithms like Cubic and BBR is that they're essentially trying to psychoanalyze the network. Cubic assumes the network is moody but predictable, backing off sharply when it senses trouble then cautiously ramping back up. BBR, on the other hand, is like that friend who's always pushing boundaries, constantly probing to find exactly how fast it can go without causing problems. It's basically playing chicken with packet loss.

What kills me is that we've built the entire internet on top of this voluntary politeness protocol. Every Netflix stream, every video call, every cat photo is being delivered by algorithms that are essentially guessing about how much they can get away with. It's like building global commerce on top of a honor system where everyone pinky swears not to be greedy. The miracle isn't that it works - it's that it works as well as it does.

