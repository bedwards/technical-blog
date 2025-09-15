---
---
# Why Comments Are Like Footnotes Nobody Reads

Comments are what we write to explain our code, and then never update when the code changes. They're like museum placards next to modern art - they might have been accurate once, but now they're just confusing everyone. At Zenoss, I found a comment that said "temporary hack, remove after version 2.0." We were on version 8.3. The hack had become load-bearing infrastructure.

The worst comments are the ones that just repeat what the code does. `i++; // increment i`. Thanks, I never would have figured that out. It's like subtitles that just say "[speaking foreign language]" - technically accurate but missing the point entirely. Good comments explain why, not what. "Increment i to skip the header row" tells me something useful. "Increment i" tells me you were forced to write comments by a style guide.

My favorite comment was just "drunk, fix later" above a block of code that actually worked perfectly. We spent hours trying to figure out what was wrong with it before realizing the comment was the bug. The code was fine; the programmer had just been honest about their state of mind. We left the comment as a warning to future generations. Sometimes the best documentation is admitting you don't know what you were thinking.

