---
---
# Why Database Migrations Are Like Performing Surgery on a Moving Train

Database migrations in production are what separate the brave from the sensible. At 21CT, we had to migrate a table with 2 billion rows while the system was actively writing to it. It's like trying to change the tires on a car during a NASCAR race - theoretically possible, but everyone watching is just waiting for the explosion.

The classic approach is to add the new column, backfill it, start writing to both columns, switch reads to the new column, stop writing to the old column, then drop it. Each step is a potential disaster. I've seen migrations where someone forgot to add an index to the new column, so the cutover turned every query into a full table scan. The database went from humming along to making sounds like a garbage disposal eating a spoon. The rollback procedure was "quickly" and the post-mortem was "we should have tested this better."

My favorite migration horror story was when we discovered, mid-migration, that our new column's data type couldn't actually hold all the values from the old column. Dates from before 1970 were being converted to December 31, 1969, turning our historical data into a time traveler's paradox. We ended up running the migration for three weeks, fixing data as we went, like renovating a house while living in it. The lesson: migrations are easy if you don't care about your data, and impossible if you do.

