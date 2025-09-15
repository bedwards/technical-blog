---
---
# Why Your Database Indexes Are Probably Backwards

During my time at 21CT working on healthcare fraud detection, I discovered that most developers think about database indexes like they think about alphabetizing books - start from the left and work your way right. But composite indexes don't work that way, and watching people create an index on (user_id, created_at, status) when they're querying by status and created_at is like watching someone try to find a book by publication date in a library organized by author.

The mental model that finally clicked for me was thinking of indexes like a phone book for aliens who read right-to-left sometimes. If you have an index on (city, last_name, first_name), you can efficiently find everyone in Austin named Smith, or everyone in Austin, but you can't efficiently find everyone named John unless you want to scan through every city. The index is only useful if you're using a prefix of the columns, in order, like you're spelling out a word and stopping partway through.

The worst part is that bad indexes are often worse than no indexes. At Zenoss, we had a query that was using an index to filter out 99% of rows, then doing a full table scan on what remained. Dropping the index entirely made the query faster because PostgreSQL stopped trying to be clever and just did what it was good at - scanning everything really fast. Sometimes the best optimization is admitting that your database is smarter than you and getting out of its way.

