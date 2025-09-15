---
---
# Why Naming Things Is the Hardest Problem in Computer Science

They say there are two hard problems in computer science: cache invalidation, naming things, and off-by-one errors. After spending three hours in a meeting arguing about whether to call something a `Manager`, `Handler`, `Controller`, or `Service`, I can confirm that naming things is definitely one of them. We eventually settled on `Processor`, which nobody liked but everyone could live with, like a compromise in a bad relationship.

The problem with naming is that every name carries baggage. Call something a `Factory` and suddenly everyone expects it to implement the factory pattern. Call it a `Helper` and you've basically admitted you have no idea what it does. Call it `Utils` and you've created a junk drawer where random functions go to die. At Zenoss, we had a class called `DataManagerFactoryServiceHelperUtil` which was technically accurate but spiritually defeated.

My favorite naming disaster was when we had two different things called `User` in the same codebase - one was the database model, the other was the API representation. This led to functions like `convertUserToUser()` which made perfect sense if you knew the context and looked like a no-op if you didn't. Code reviews were like Abbott and Costello's "Who's on First" routine. We eventually prefixed everything with its layer (`DbUser`, `ApiUser`), which was ugly but at least unambiguous. Sometimes clarity beats elegance, even if it hurts to type.

