---
---
# Why Your Load Balancer Is Probably Making Things Worse

Load balancers are supposed to distribute traffic evenly, but most of them are about as good at it as a drunk dealer at a casino. Round-robin sounds fair until you realize that requests aren't created equal - one might be a simple health check while another is generating a PDF of the entire Harry Potter series. It's like distributing groceries by giving everyone one item, whether it's a grape or a watermelon.

At Zenoss, we had a load balancer that was using "least connections" which sounds smart until you realize it was sending all traffic to the fastest server, which would then slow down, causing traffic to shift to the next server in a beautiful cascade of failure. It was like a game of hot potato where the potato was our entire user base. The load balancer was technically working perfectly - it just wasn't solving the problem we thought it was.

The solution was to implement weighted routing based on actual CPU usage, but that required the load balancer to understand application-level metrics, which is like asking a traffic light to understand the emotional state of drivers. We ended up with this Rube Goldberg machine of health checks, metrics exporters, and dynamic weight adjustments that probably used more resources than just handling the traffic poorly would have. Sometimes the cure is worse than the disease, but at least our graphs looked better.

