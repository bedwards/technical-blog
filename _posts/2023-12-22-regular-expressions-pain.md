---
---
# Regular Expressions: Writing Code That Nobody, Including You, Can Read

Regex is the only programming language that looks like someone fell asleep on their keyboard and accidentally solved a problem. I once wrote a regex to parse email addresses that was so complex, I had to write documentation longer than the regex itself just to explain what it did. Six months later, I needed to modify it and ended up just rewriting it from scratch because understanding my own code would have taken longer.

The email regex is actually a perfect example of why regex is both powerful and terrible. The actual RFC-compliant regex for email addresses is over 6,000 characters long and looks like someone tried to transcribe the Matrix while having a seizure. Most people just use `.*@.*\..*` and hope for the best, which accepts basically anything with an @ symbol, including "definitely@not@an@email.address". It's like building a security system that checks if visitors are human by asking if they have a face.

My favorite regex disaster was when someone used `.*` to match "anything" but forgot that in single-line mode, it really means anything, including newlines. This regex was supposed to extract URLs from text but ended up matching the entire document as one giant URL. The resulting bug report was just "The website link downloader downloaded the entire internet." Sometimes the simplest patterns cause the biggest problems.

