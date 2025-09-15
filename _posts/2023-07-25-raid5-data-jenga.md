---
---
# Why RAID 5 Is Like Playing Jenga With Your Data

RAID 5 is what happens when you want redundancy but you're too cheap for RAID 10. It's like insurance that only covers you if exactly one thing goes wrong - any more than that and you're having a very bad day. At ExxonMobil, I watched a RAID 5 array lose two drives within an hour of each other, and the sound the storage admin made was somewhere between a sob and a laugh.

The beautiful lie of RAID 5 is that drives fail independently. In reality, drives from the same batch, running the same workload, in the same temperature conditions, tend to fail together like synchronized swimmers. When one drive fails and you start rebuilding, you're basically stress-testing all the other drives that were already thinking about retirement. It's like asking your elderly car to help push another broken car - sometimes that's exactly when it decides to join its friend in failure.

The rebuild process itself is terrifying. You're reading every single bit from every surviving drive, and if any of them have even one unreadable sector, your rebuild fails and your data is gone. Watching a RAID 5 rebuild is like watching someone defuse a bomb while jogging - technically possible, but you really don't want any surprises. These days I tell people RAID 5 is fine for data you'd be okay losing, which defeats the entire purpose, but at least sets expectations appropriately.

