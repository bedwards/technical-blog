---
---
# Why Distributed Locks Are Basically Philosophical Debates

Implementing distributed locking at Atlassian taught me that distributed systems are just philosophy with more math. You think you understand what "holding a lock" means until you have to define it across multiple machines that can't agree on what time it is. It's like trying to organize a group project where everyone's watch shows a different time and some people might spontaneously combust.

The classic problem is what happens when a node acquires a lock and then has a very long garbage collection pause. From its perspective, it still holds the lock. From everyone else's perspective, it's dead and the lock has been given to someone else. When it wakes up from its GC coma, it still thinks it owns the lock and starts modifying data, like someone who fell asleep at a party and woke up still talking. This is how you get data corruption that makes you question the nature of reality.

My solution was to use fencing tokens - basically giving each lock a version number that increments every time it changes hands. If you show up with an old token, you get rejected like trying to use last year's parking pass. It's not perfect (nothing in distributed systems ever is), but it turns catastrophic corruption into merely annoying failures, which is about as good as it gets in this business.

