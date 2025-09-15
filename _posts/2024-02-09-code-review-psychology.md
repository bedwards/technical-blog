---
---
# The Psychology of Code Reviews

Code reviews are where engineers practice their favorite sport: being technically correct while missing the entire point. I've seen reviews where someone spent an hour debating whether to use `i++` or `++i` in a loop that runs three times, while ignoring that the function was called `processData()` and was 3000 lines long. It's like proofreading someone's suicide note for grammar.

The worst reviews are the ones where someone clearly didn't read the code but felt obligated to comment something, so they point out a missing semicolon in JavaScript where it's optional, or suggest renaming a variable from `user` to `usr` to "save space." These are the people who would critique the Mona Lisa for not smiling enough. At Atlassian, we had a reviewer who would only ever comment "LGTM" (looks good to me) or "needs work," with no indication of what needed work. It was like getting your essay back marked "wrong" with no other feedback.

My approach to code reviews changed when I realized they're not about the code - they're about knowledge transfer. The best review comment I ever received was "This works, but here's how I've seen this pattern cause problems in the future." That's worth more than a thousand nitpicks about formatting. Now when I review, I ask myself: will the next person understand why this decision was made? If not, that's what needs commenting, not whether they used tabs or spaces.

