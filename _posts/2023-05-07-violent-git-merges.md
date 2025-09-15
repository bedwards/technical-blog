---
---
# The Surprisingly Violent History of Git Merge Conflicts

Git merge conflicts are what happens when parallel universes collide and you have to manually decide which reality wins. At Atlassian, I spent so much time resolving conflicts in Bitbucket's codebase that I started seeing angle brackets in my dreams. The worst part isn't the conflict itself - it's when Git helpful shows you both versions and they look identical to the human eye but differ by one invisible whitespace character.

The thing that really gets me is how Git's conflict markers are basically the software equivalent of a shrug emoji. "Here's what you had, here's what they had, you figure it out." It's like if your GPS said "you want to go left, your passenger wants to go right, good luck!" and then shut off. The manual resolution process is basically performing surgery on your codebase with a text editor as your only tool.

My favorite was when we had a conflict in a conflict resolution script. Someone had written a tool to automatically resolve certain types of conflicts, then two people had improved it in incompatible ways, creating a meta-conflict that broke the very tool designed to fix conflicts. It was like the universe was testing whether we understood irony. We ended up resolving it by flipping a coin, which honestly might be how Git should handle all conflicts.

