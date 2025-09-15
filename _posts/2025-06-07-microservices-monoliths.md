---
---
# Why Microservices Are Just Distributed Monoliths With Extra Steps

Everyone loves microservices until they have to debug a request that touches seventeen different services, each with its own logs, metrics, and idea of what "user ID" means. At Atlassian, we split our monolith into microservices and ended up with a distributed monolith where everything still depended on everything else, but now with network latency between the dependencies.

The promise of microservices is that teams can work independently, but then you need a service mesh to handle communication, a distributed tracing system to debug issues, a service registry to find things, and suddenly you've traded application complexity for operational complexity. It's like solving your messy room problem by getting seventeen smaller rooms - the mess is still there, just distributed.

My favorite microservice antipattern was when we had two services that called each other in a loop, creating a distributed infinite recursion that was somehow harder to detect than a regular infinite recursion. Service A would call Service B for user data, Service B would call Service A for authentication, Service A would call Service B to verify the authentication, and around and around they went like two people trying to go through a door at the same time. The fix was embarrassingly simple - someone needed to go first - but finding it required distributed tracing that looked like abstract art.

