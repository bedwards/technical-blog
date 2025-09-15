---
---
# The Secret Life of Database Connection Pools

Connection pooling is one of those things that seems simple until you actually try to implement it, like parallel parking or making good coffee. At Zenoss, I watched a senior engineer confidently set the pool size to 200 because "more connections = more fast" and then wonder why the database server started making concerning noises like a car engine filled with marbles.

The dirty secret is that your optimal pool size has almost nothing to do with your load and everything to do with your database's ability to context switch. PostgreSQL starts crying around 100 connections, MySQL gets nervous around 150, and Oracle just sends you another invoice. It's like trying to figure out how many browser tabs you can have open before your laptop becomes a space heater - the answer is always fewer than you think.

My favorite connection pool bug was when we had a leak that only happened on Tuesdays. Turns out, our weekly batch job was checking out connections and never returning them, like that person who borrows books from the library and uses them as furniture. The pool would slowly drain over the course of Tuesday, and by Wednesday morning, the application couldn't get a connection if its life depended on it. The fix was embarrassingly simple - try-with-resources blocks - but finding it required the kind of detective work that would make Sherlock Holmes proud.

