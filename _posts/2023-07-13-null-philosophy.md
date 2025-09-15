---
---
# The Philosophical Implications of NULL

NULL is the programming equivalent of dividing by zero - mathematically necessary but philosophically troubling. It's not zero, it's not empty, it's not false - it's the absence of existence itself. At Zenoss, we had a bug where NULL != NULL was true, because you can't compare nothing to nothing and expect a meaningful answer. It's like asking if the color of invisible is the same as the color of transparent.

SQL's three-valued logic with NULL is where sanity goes to die. TRUE, FALSE, and NULL walk into a bar. The bartender asks, "Do all of you want drinks?" The answer is NULL because we don't know what NULL wants. This actually happened in our reporting system - any query with a NULL in the wrong place would make the entire result NULL, like a black hole that consumed meaning itself. We'd run reports and get blank pages, not because there was no data, but because somewhere, deep in the logic, a NULL had poisoned everything it touched.

My favorite NULL bug was when we were checking if a value was not equal to something, and NULLs were sneaking through because NULL isn't equal or not equal to anything - it exists outside the concept of equality. It's like asking if a unicorn is taller than a dragon. The question assumes both exist. We ended up wrapping everything in COALESCE calls until our SQL looked like we were afraid NULL was contagious, which, in a way, it is.

