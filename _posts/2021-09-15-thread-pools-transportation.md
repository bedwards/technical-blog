---
---
# Why Thread Pools Are Like Public Transportation

Thread pools are supposed to be efficient resource management, but they're really just a way to make your threading problems someone else's problem. It's like taking the bus instead of driving - you're not dealing with traffic directly, but you're still stuck in it. At Juniper, we had a thread pool that would occasionally just stop accepting new tasks, like a bus driver who decided they'd had enough and just parked the bus.

The sizing problem is identical to connection pools but with more existential dread. Too few threads and tasks queue up like people waiting for the bathroom at a concert. Too many and your CPU context-switches itself to death, spending more time changing between tasks than doing them. The "optimal" number is always based on benchmarks that have nothing to do with your actual workload. It's like sizing a parking lot based on average usage then being surprised when it's empty on weekends and overflowing during events.

My favorite thread pool bug was when tasks would submit new tasks to the same pool, creating a deadlock where all threads were waiting for threads to become available. It was like a circular firing squad where everyone's waiting for someone else to shoot first. The pool was full of tasks waiting for the pool to have space. We fixed it by having separate pools for different task types, which is really just admitting that one pool isn't enough and maybe we should have thought about this more.

---

I am working on copying all my blog posts to LinkedIn. In the meantime, you can find them all at

[https://bedwards.github.io/technical-blog/](https://bedwards.github.io/technical-blog/)

After re-reading this post, I am motivated to explain the concepts from first principles, differentiating them from similar concepts (or their opposites).

---

Thread pools sound like a clever way to tame concurrency, but they’re closer to outsourcing the mess than solving it. To see why, it helps to strip the idea down to basics. A thread is just a worker. If you need more work done than one worker can handle, you hire more. A pool is like setting up a hiring agency: instead of spawning workers yourself, you drop off tasks and trust the agency to dispatch them. This sounds neat, but the hard problems—how many workers, how they’re scheduled, what happens if they block—are still there. They’ve only been hidden one layer deeper.

The opposite of a thread pool is ad-hoc threading, where each task spawns its own worker and lets the operating system figure it out. That removes the bottleneck of a shared queue but creates its own chaos: hundreds or thousands of workers all competing for CPU time, memory, and locks. The pool avoids this explosion but introduces queues and capacity limits, which means you’re still constrained, just differently.

The sizing dilemma is the heart of the matter. Too few threads and everything piles up, a backlog that grows like a line at airport security. Too many threads and you choke the system with context switches, as if every passenger had their own dedicated lane and the TSA kept shuffling them around instead of screening anyone. The sweet spot exists, but it shifts constantly depending on I/O versus CPU work, bursts of load, and hidden dependencies. Static “best practice” numbers rarely survive first contact with reality.

One way to see this tension clearly is through percentile wait times. Looking only at averages hides the spikes, but a metric like the 95th percentile (p95) reveals the real pain: the slowest tail of tasks stuck in line while others flow through. If your average looks fine but the p95 is high, you know the system is failing under pressure—critical jobs are waiting too long, even if most are handled quickly. Thread pools can make the mean look smooth, but the p95 shows whether the design is actually protecting workloads or just shifting the delays around.

The value of p95 comes from living between two less useful extremes. The 50th percentile—the median—tells you what a “typical” task experiences, but typical is not the problem people notice. The 100th percentile—the absolute slowest—tends to be dominated by weird one-off events: a single task stuck on a disk hiccup, a network timeout, a machine swapping. Those numbers are real but not representative. By focusing on the 95th percentile, you trim off the rarest freak cases while still measuring the slow-but-normal tail that actually shapes user experience. That’s the slice of the curve where real bottlenecks show themselves.

Then there’s the recursive trap. If a task inside the pool tries to submit more tasks back into the same pool, you can deadlock. All the workers are waiting, none are free, and the queue just stares back at itself. It’s the concurrency equivalent of two mirrors facing each other: infinite regress, no progress. Separate pools for separate responsibilities break the cycle, but that’s an admission that “one pool to rule them all” was a fantasy from the start.

The related concept here is connection pooling, which faces the same question of “how many is enough?” but with sockets instead of threads. Both try to reuse expensive resources and avoid runaway creation. The opposite of pooling—creating a new resource each time—seems simpler until you hit scaling limits. Pooling flips the problem: instead of resource exhaustion, you risk contention, starvation, or deadlock. It’s always a trade.

And finally, there is the human side of the metaphor. A pool of workers, like a pool of buses, can only mask the traffic for so long. You can size it, split it, tune it, monitor it—but in the end, you are still in traffic. Thread pools are not a silver bullet. They are a truce with complexity, a way of saying: “I won’t solve this, I’ll manage it.” And managing it well is sometimes harder than solving it outright.