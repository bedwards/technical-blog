---
---
# Why Logging Is Like Talking to Your Future Self

Good logging is like leaving notes for yourself when you know you'll have amnesia. Bad logging is like someone constantly screaming "SOMETHING HAPPENED" without any context. At Juniper, I inherited a system where every log message was either "Error" or "Success," which is about as helpful as a smoke detector that only says "Maybe fire?"

The art of logging is knowing what your future self will desperately need to know at 3 AM when everything is broken. Log the request ID, the user ID, the timestamp, what you were trying to do, what actually happened, and why you think it failed. "Failed to process payment for user 12345: Credit card declined (insufficient funds) after 3 retry attempts" is a log message that respects your time. "Payment error" is a cry for help that nobody can answer.

My favorite logging antipattern is when people log exceptions but not the stack trace, like taking a picture of a crime scene but only photographing the sky. Or when they log so much that finding the actual error is like looking for a specific grain of sand on a beach. I once worked with a system that logged every getter and setter call, producing gigabytes of logs per hour that basically said "yep, still getting and setting" over and over. The signal-to-noise ratio was so bad that we just turned off logging entirely, which is like solving a noise problem by going deaf.

