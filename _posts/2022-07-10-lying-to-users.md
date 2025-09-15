---
---
# The Art of Lying to Users About Distributed Systems

One thing I learned at Atlassian is that users don't want to know about eventual consistency - they want to click save and see their changes immediately. So we became masters of illusion, creating what I call "optimistic UI" but what's really just consensual lying between the frontend and backend. You click save, we immediately show you the saved state, and then frantically try to actually save it before you notice.

The trick is managing the edge cases when the lie falls apart. What happens when the save fails but we already told the user it worked? You need this whole reconciliation dance where you gracefully degrade from "saved" to "saving" to "maybe saved?" to "okay it's definitely not saved and here's why." It's like being a magician whose rabbit died mid-trick and now you have to explain to the audience why the hat is making sad noises.

My favorite pattern was what we called "the time traveler's save" - we'd optimistically update the UI, send the request, and if it failed, we'd rewind the UI state like nothing happened. Users would occasionally see their text flicker as reality reasserted itself, but it was better than showing a spinner every time someone typed a character. The key insight was that users prefer a beautiful lie that's usually true over an ugly truth that's always accurate.

