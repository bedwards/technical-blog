---
---
# The Paradox of Database Indexes

Adding indexes to make queries faster is like adding lanes to a highway - it works until everyone starts using them, then you're back where you started but with more maintenance. At 21CT, we had a table with more indexes than columns because every time a query was slow, someone added an index. The inserts were so slow you could watch individual rows being added like a very boring screensaver.

The problem is that indexes make reads faster but writes slower, and nobody mentions this trade-off until your write-heavy workload grinds to a halt. It's like optimizing for going downhill by carrying rocks uphill - great if you only care about one direction. We had indexes on columns that were never queried, indexes on combinations of columns that made no sense, and one index that was literally a duplicate of another index but with a different name.

My favorite index bug was when someone created an index on a boolean column in a table where 99% of the values were true. The database would dutifully check the index, find almost every row matched, then do a full table scan anyway. It was like having a phone book where everyone's last name is Smith - technically organized but practically useless. The index was making queries slower by adding an extra step that provided no value. Sometimes the best optimization is removing your optimizations.

