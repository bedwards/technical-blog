---
---
# That Time I Accidentally DDoSed Myself with Webhooks

At Atlassian, I was redesigning Bitbucket's webhook system when I learned that distributed systems have a sense of humor, and it's dark. I'd built this beautiful event-driven architecture where every git push would trigger webhooks to update build systems, notify chat rooms, and sync with issue trackers. What I hadn't considered was what happens when one of those webhooks triggers another git push.

The first sign of trouble was when our monitoring dashboard looked like a Christmas tree having a seizure. Turns out, a customer had set up a webhook that would automatically format code and push it back to the repository. This triggered the webhook again, which formatted the already-formatted code (making tiny whitespace changes), which triggered the webhook again. Within minutes, we had created an infinite loop that was generating thousands of commits per second, all of them changing absolutely nothing important.

The fix was embarrassingly simple - add loop detection. But the lesson stuck with me: every distributed system is about three edge cases away from becoming self-aware and trying to kill you. Now whenever I design event systems, I always ask myself "what happens if this event triggers itself?" It's like the distributed systems version of "what if your time machine kills your grandfather?" except instead of a paradox, you get a very angry SRE team.

