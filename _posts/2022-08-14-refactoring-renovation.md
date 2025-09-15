---
---
# Why Refactoring Is Like Renovating While Living in the House

Refactoring production code is like trying to change your car's oil while driving down the highway. Everyone agrees it needs to be done, but nobody wants to be the one doing it when things inevitably go wrong. At Zenoss, we had a refactoring project that was supposed to take two weeks. Six months later, we were still finding places where the old code was hiding like roaches in a kitchen renovation.

The promise of refactoring is that you're just changing the implementation, not the behavior. This is a beautiful lie we tell ourselves, like "I'm just going to the gym for 20 minutes." Every refactoring changes behavior in subtle ways - timing changes, error messages change, that weird bug everyone worked around gets fixed and breaks the workarounds. We had a refactoring that made everything 10% faster, which sounds great until you realize that other systems were depending on that slowness for synchronization.

My favorite refactoring disaster was when we renamed a widely-used internal API from `processData` to `handleDataProcessing` for "clarity." We updated all the references we could find, tested everything, deployed to production, and immediately broke seventeen integration partners we didn't know existed. They'd been calling our internal API directly, against all documentation and common sense. The rollback was so fast I think we achieved time travel. Now when I refactor, I assume there's always some undocumented system depending on whatever terrible behavior I'm trying to fix.

