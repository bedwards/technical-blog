---
---
# Why Eventual Consistency Is Like Agreeing to Disagree

Eventual consistency is the distributed systems equivalent of "we'll figure it out later." It's what happens when you can't afford to be consistent right now, so you promise to be consistent eventually, like a New Year's resolution for databases. At Bitbucket, we had eventual consistency with a several-second delay, which meant you could push code, refresh, not see it, panic, refresh again, see it, and wonder if you were going crazy.

The "eventual" in eventual consistency is doing a lot of heavy lifting. It's like saying you'll "eventually" clean your room - technically true but practically useless without a timeframe. We had customers who would make a change, immediately read it back, get the old value, and file a bug report about our "broken" system. Explaining eventual consistency to users is like explaining why their pizza will "eventually" arrive - they don't care about your distributed consensus problems, they just want their data.

My favorite eventual consistency bug was when two users would edit the same document simultaneously, and depending on which replica they hit, they'd see different versions. It was like a choose-your-own-adventure book where different people were reading different adventures. The support tickets were amazing: "The document says X!" "No, it says Y!" They were both right, just reading from different realities. We fixed it by adding read-after-write consistency, which is like eventual consistency with training wheels.

