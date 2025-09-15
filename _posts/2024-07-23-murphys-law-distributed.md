---
---
# The Distributed Systems Version of Murphy's Law

In distributed systems, anything that can fail will fail, and several things that can't fail will also fail just to keep things interesting. At Atlassian, we had a system that would work perfectly in testing, staging, and production... until Thursday afternoon, when it would mysteriously fail for exactly 17 minutes. It was like the system had a weekly appointment with chaos.

The investigation revealed a beautiful cascade of failures: our health check timeout was 30 seconds, our connection pool timeout was 29 seconds, and our load balancer timeout was 31 seconds. Every Thursday, a batch job would cause just enough latency that these timeouts would create a perfect storm where healthy servers were marked as unhealthy while unhealthy servers were kept in rotation. It was like a three-way Mexican standoff where everyone shoots themselves.

The fix was to make all the timeouts different enough that they couldn't resonate, like detuning a guitar so it can't create feedback. But the real lesson was that distributed systems don't just fail - they fail in ways that would make Rube Goldberg proud. Every timeout is a potential failure mode, every retry is a potential amplifier, and every cache is a potential time bomb. The only question is whether you'll find the bomb before it goes off.

