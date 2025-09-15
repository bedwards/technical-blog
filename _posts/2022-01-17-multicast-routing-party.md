---
---
# Why Multicast Routing Is Like Hosting a Party Nobody Wants to Attend

Writing a book on interdomain multicast routing was like documenting a beautiful solution to a problem nobody wanted to admit they had. The protocol itself is elegant - instead of sending the same video stream to a thousand clients individually, you send it once and let the network figure out the replication. But getting ISPs to actually deploy it was like trying to convince people to use the metric system in America.

The fundamental issue with multicast is that it requires every router in the path to maintain state about who wants what stream. In a world where routers are already tracking hundreds of thousands of unicast routes, asking them to also remember that Bob in accounting wants to watch the company all-hands meeting is apparently a bridge too far. It's like asking a postal worker to not only deliver mail but also remember everyone's Netflix preferences.

What really frustrated me was watching CDNs basically reinvent multicast at the application layer, badly. They'd build these elaborate overlay networks to distribute content, burning through bandwidth like a teenager with unlimited data, all because network operators couldn't get their act together to deploy a protocol we'd had working since the 1990s. Sometimes I think about all the wasted bandwidth from sending the same cat video millions of times and a little part of my soul dies.

