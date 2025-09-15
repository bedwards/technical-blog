---
---
# The Lost Art of Writing Useful Error Messages

After years of debugging production issues, I've developed strong opinions about error messages. "An error occurred" is not an error message, it's an admission of defeat. It's like calling 911 and saying "something bad happened somewhere" and hanging up. At Juniper, I once spent six hours debugging an error that just said "Connection failed" when what it meant was "Connection failed because your certificate expired 37 days ago and we've been too polite to mention it."

The perfect error message tells you what went wrong, why it went wrong, and what you can do about it. "Cannot connect to database 'users' on host 'db-primary-1' port 5432: Connection timeout after 30 seconds. Check if the database is running and accepting connections on the specified host and port." That's an error message that respects your time. It's like having a helpful friend instead of a cryptic oracle.

My favorite bad error message was one that said "Success" when things failed. Turns out someone had copy-pasted error handling code and forgot to change the message. Users would try to save their work, get a cheerful "Success!" message, and lose everything. It was like having a smoke detector that played celebration music during fires. We fixed it, but not before it became legend in our support tickets as "the lying success message of doom."

