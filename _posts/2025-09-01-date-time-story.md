---
---
# The Never-Ending Story of Date and Time

Every programmer thinks they understand dates and times until they have to deal with time zones, daylight saving time, leap seconds, and historical calendar changes. Then they realize that time is a social construct that computers pretend to understand. At Florida Blue, we had a bug where appointments would disappear for one hour every year when daylight saving time ended. They weren't deleted, they just existed in an hour that happened twice, and we were only showing the first one.

The best part is when people say "just store everything in UTC" like that solves everything. UTC is great until you need to show a user when something happened in their local time, and now you need to know not just their current time zone but what their time zone was when the event happened, because time zones change. India used to have hundreds of time zones. Russia has changed its time zones eleven times. The database that tracks time zone changes is updated multiple times per year.

My favorite time bug was when we calculated age by subtracting birth year from current year, which worked great except for people born on December 31st who were apparently a year older for one day. Or the system that scheduled daily jobs at 2:30 AM, which didn't exist one day per year when daylight saving started. The job just... didn't run, like it took a vacation day nobody approved. Now I treat dates and times like explosives - handle with extreme care and assume they're trying to kill you.

