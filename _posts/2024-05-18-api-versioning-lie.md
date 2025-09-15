---
---
# The Noble Lie of API Versioning

API versioning is what we tell ourselves we'll do properly this time, like flossing or going to the gym. Everyone starts with good intentions - v1, v2, v3 - then reality hits and you end up with v2.1.3-beta.4-final-final-actually-final-2. At Atlassian, we had APIs that were theoretically on v3 but had so many feature flags and compatibility modes that every request was basically choosing its own adventure.

The biggest lie is that you can deprecate old versions. You announce that v1 will be sunset in six months, and six years later it's still running because one important customer has a bash script from 2012 that they refuse to update. It's like trying to demolish a bridge while people are still driving on it. You end up maintaining every version forever, like a museum of your past mistakes that people are actively using.

My solution was to version the endpoints, not the API, so `/users` and `/v2/users` could coexist peacefully. This worked until someone decided we needed to version the response format too, so we ended up with headers like `Accept: application/vnd.company.v2+json` which is just version numbers with a college degree. Eventually, we gave up and just made everything backward compatible forever, which is expensive but at least honest about what we were doing anyway.

