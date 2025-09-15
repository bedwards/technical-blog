---
---
# Why Caching Is Like Gambling With Performance

Every cache is a bet that the future will look like the past. You're gambling compute time now against potential savings later, like buying lottery tickets with CPU cycles. At Bitbucket, we cached everything - user data, repository metadata, permission checks, the results of caching checks. We had caches of caches, like Russian nesting dolls made of memory leaks.

The cache invalidation problem is actually three problems wearing a trench coat. First, knowing when to invalidate. Second, actually invalidating everything that needs it. Third, not invalidating everything else by accident. It's like trying to update your address with every company you've ever given it to - you'll forget someone, update someone twice, and somehow end up on new mailing lists you never signed up for. We had cascading cache invalidations that would ripple through the system like dominoes falling in slow motion.

My favorite cache bug was when we cached error responses. A service would timeout once, we'd cache the error, and then serve that cached error for the next hour even though the service was fine. It was like taking a photo of someone sleeping and then showing that photo whenever anyone asked how they were doing. "Sorry, Bob is unconscious" we'd say, while Bob was standing right there, waving frantically. The fix was simple - don't cache errors - but we only figured this out after users complained that the system was both "always broken" and "working fine" simultaneously.

