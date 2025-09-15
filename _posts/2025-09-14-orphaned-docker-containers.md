---
---
# The Tragedy of Orphaned Docker Containers

Docker containers are like houseguests - easy to invite, hard to get rid of. At Atlassian, we had a CI/CD system that would spin up containers for testing and occasionally forget to clean them up. After six months, we discovered thousands of orphaned containers just sitting there, consuming resources, like digital squatters. The server was basically a container graveyard where old builds went to not quite die.

The command `docker system prune` is both the best and scariest command in Docker. It's like a reset button that might delete something important, or might free up 100GB of space, or might do both. Running it feels like playing Russian roulette with your infrastructure. We had one developer who ran it on production thinking it would only clean up unused images. It cleaned up everything that wasn't currently running, including stopped containers we were planning to debug. The post-mortem was just "Dave learned about the --help flag."

My favorite Docker bug was when we had containers that would resurrect themselves after being killed, like digital zombies. Turns out we had a orchestration system that was helpfully restarting them because it thought they'd crashed. We were basically fighting our own automation, killing containers that our other system would immediately respawn. It was like trying to bail out a boat while someone else is filling it with water. The solution was embarrassingly simple - tell the orchestrator to stop helping - but finding it required understanding three different systems that were all trying to be helpful.

