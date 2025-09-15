---
---
# Why API Rate Limiting Is Like a Nightclub Bouncer

Rate limiting is supposed to protect your API from abuse, but mostly it just annoys legitimate users while attackers figure out ways around it. It's like having a bouncer who counts how many times you've entered the club but doesn't notice you climbing in through the bathroom window. At Bitbucket, we had rate limiting that would kick in right when users needed the API most - during deployments when CI/CD systems would hammer our endpoints.

The fun part is choosing what to limit. Requests per second? Requests per minute? Per endpoint? Per user? Per IP? Congratulations, you've invented a multidimensional optimization problem where every solution makes someone angry. We had one customer with thousands of employees behind a single NAT IP who would hit our per-IP rate limit constantly. But if we raised it, we'd be opening ourselves up to actual abuse. It was like trying to set a speed limit that works for both racing cars and school buses.

My favorite rate limiting bug was when we implemented exponential backoff incorrectly and told clients to wait negative seconds before retrying. The client library dutifully interpreted this as "retry immediately," creating a thundering herd that would DDoS us every time we rate limited someone. We were essentially punishing ourselves for trying to protect ourselves. It was like a security system that calls the burglars when it detects a break-in.
