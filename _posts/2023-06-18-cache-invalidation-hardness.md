---
---
# Cache Invalidation: The Second Hardest Problem in Computer Science

Phil Karlton said there are only two hard things in computer science: cache invalidation and naming things. After spending a month debugging a caching issue at Zenoss where metrics would randomly show data from three hours ago, I'd argue cache invalidation is actually harder because at least with bad names, your code still works.

The problem with caching is that it's basically time travel. You're showing users data from the past and hoping they don't notice. It's like running a restaurant where sometimes you serve yesterday's soup because making new soup is expensive. Most of the time nobody notices, but occasionally someone orders soup, watches you make it, and then receives soup from last Tuesday, and now you have to explain the concept of eventual consistency to someone who just wanted lunch.

My favorite cache bug was one where we were caching user permissions, but the cache key didn't include the user ID. So everyone was getting the permissions of whoever logged in first that day, like a very democratic security vulnerability. Bob from accounting would log in and suddenly have admin access, while the actual admin couldn't do anything. It was like a daily lottery where the prize was accidentally becoming root. The fix was embarrassingly obvious once we found it, but it took us three weeks of users complaining about "random" permission issues before someone noticed the pattern.

