---
---
# The Zen of Monitoring Systems That Monitor Themselves

Monitoring systems are like security cameras in a security camera store - at some point, you need to accept infinite recursion or just trust something. At Zenoss, we built a monitoring system, which naturally needed monitoring, so we built a monitor for the monitor. Then someone asked what monitors the monitor monitor, and we realized we'd entered a philosophical debate that predates computers.

The classic problem is when your monitoring system fails, how do you know? It's not going to alert you that it can't send alerts. It's like expecting a dead smoke detector to beep about its own death. We solved this with a heartbeat system where the monitor had to check in regularly, and if it didn't, we assumed it was dead. Of course, this required another system to monitor the heartbeats, and suddenly we were back in recursion hell.

My solution was what I called "mutual monitoring" - having multiple systems monitor each other in a circle, like a trust exercise for software. System A monitors B, B monitors C, C monitors A. If any link breaks, someone notices. It's not perfect (what if they all fail simultaneously?), but it's better than the alternative, which is finding out your monitoring has been dead for a week when a customer calls to ask why their site has been down for a week.

