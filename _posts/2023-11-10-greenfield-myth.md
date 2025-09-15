---
---
# The Myth of the Greenfield Project

Every developer dreams of greenfield projects where you can do everything right from the start. No legacy code, no technical debt, no compromises. Then you start building and realize you're just creating tomorrow's legacy code today. At Atlassian, we started a greenfield project with the best intentions - microservices, event-driven, cloud-native, all the buzzwords. Two years later it had all the same problems as the system it was replacing, just with newer technology.

The problem with greenfield projects is that you don't know what you don't know. You make architectural decisions based on requirements that will change, optimize for problems you won't have, and ignore problems you will have. It's like planning your dream house before you've ever lived in a house. Sure, the indoor pool sounds great, but you forgot to include a place to store the vacuum cleaner. We built a beautiful, scalable system that could handle millions of users, then discovered our actual bottleneck was a third-party API that could handle twelve requests per second.

My favorite greenfield mistake was when we decided not to add logging initially because "we'll add it when we need it." The first production issue happened within hours, and we were debugging it completely blind, like trying to perform surgery in the dark. We added logging, but then had to wait for the issue to happen again. It was like installing a security camera after the robbery and hoping the thief comes back. The second rule of greenfield projects (after "you will recreate all the old problems") is "add logging first, ask questions later."

