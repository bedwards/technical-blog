---
---
# Binary Search: The Algorithm That Keeps Giving You Trust Issues

Binary search is theoretically simple - keep cutting the search space in half until you find what you want. It's like looking for a word in the dictionary if dictionaries were vindictive and enjoyed watching you suffer. The number of ways to get binary search wrong is truly remarkable for something that's basically just "pick the middle and recurse."

The classic off-by-one error in binary search has probably caused more debugging hours than any other algorithm mistake. Should it be `mid = (low + high) / 2` or `mid = low + (high - low) / 2`? The first one can overflow if your array is big enough, which you'll discover at 3 AM when your production system starts returning garbage. The second one is correct but looks like you're showing off. And don't even get me started on whether high should be `length` or `length - 1`.

I once spent an entire day debugging a binary search that worked perfectly except for the last element of the array. Turns out I was using `<` instead of `<=` in the loop condition, so it would get tantalizingly close to the last element and then give up, like a marathon runner collapsing inches from the finish line. The fix was one character, but finding it required adding so many print statements that the code looked like a journal of my descent into madness.

