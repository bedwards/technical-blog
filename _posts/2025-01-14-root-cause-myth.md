---
---
# The Myth of the Root Cause

"Root cause analysis" is what we do when we want to pretend that failures have a single cause, like a murder mystery where there's always one butler with one candlestick. In reality, system failures are more like airplane crashes - a bunch of things had to go wrong in just the right way. At Atlassian, we had an outage that required seventeen different things to fail simultaneously. The root cause analysis looked like a conspiracy theory board with red string connecting everything.

The Five Whys technique is supposed to help, but usually, it just leads to existential questions. Why did the server crash? Because it ran out of memory. Why did it run out of memory? Because the cache was too big. Why was the cache too big? Because we cached everything. Why did we cache everything? Because database queries were slow. Why were queries slow? Because we exist in a universe where the speed of light is finite and entropy always increases. At some point, you have to stop or you end up blaming the Big Bang.

My approach is to accept that failures are usually conspiracies of circumstances. Instead of finding "the" root cause, I look for the easiest link to break in the failure chain. Can't prevent cosmic rays from flipping bits? Add error correction. Can't prevent developers from writing bugs? Add tests. Can't prevent tests from missing things? Add monitoring. It's not satisfying to say "several things went wrong," but it's more honest than pretending there's always one villain to blame.

