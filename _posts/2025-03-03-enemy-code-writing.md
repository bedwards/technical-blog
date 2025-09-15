---
---
# The Art of Writing Code for Your Enemy

I write code like the person maintaining it wants to hurt me, because that person is usually future me, and future me definitely wants to hurt past me. At Juniper, I inherited code that was clearly written by someone who hated humanity. Variable names like `x`, `xx`, and `xxx`. Comments like "don't touch this." Functions that were 3000 lines of nested if statements. It was like archaeological excavation of someone's breakdown.

Good code is like a well-written recipe - even if you don't understand why you're adding baking soda, at least you know when and how much. Bad code is like those recipes that say "cook until done" - technically correct but practically useless. I now write comments explaining not what the code does (that should be obvious) but why it does it that way. "We sort here because the database returns results in random order due to a bug in version 2.3.4 that we can't upgrade because of licensing issues."

My rule is: if you have to think about it for more than five seconds, comment it. If you did something weird to work around a bug, document the bug. If you optimized something, explain what was slow and why this is faster. Your future self isn't psychic, and neither is the poor soul who inherits your code when you leave for a better job. Every unclear line of code is a future 3 AM debugging session waiting to happen.

