---
---
# The Myth of the Stateless Service

Everyone talks about stateless services like they're the solution to all distributed systems problems. "Just make it stateless," they say, as if state isn't like energy - it can neither be created nor destroyed, only moved around until it becomes someone else's problem. At Atlassian, we had services that were technically stateless but required 47 environment variables to start up, which is just state with extra steps.

The dirty secret is that truly stateless services are about as common as unicorns and just as magical. Your "stateless" API server still needs to know which database to talk to, what port to listen on, and how to authenticate requests. That's all state, you've just convinced yourself it doesn't count because it's in a config file. It's like saying you're vegetarian except for bacon - technically true but missing the point.

My favorite example was a service that prided itself on being stateless but would crash if you restarted it too quickly because it was actually storing state in Redis with a 30-second TTL. It was stateless in the same way that I'm organized because I know which pile of papers contains what I'm looking for. The state was there, just carefully hidden where the architects couldn't see it, like sweeping dust under a rug and calling the room clean.

