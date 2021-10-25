---
title: Testing Client Server Integration
category: [Software_Testing]
---

## Testing Client Server Integration

While testing client side code, server dependency also comes into picture which internally may have dependencies on Database, File servers etc.
There are always challenges due to flakiness, connection issues.

### Hermetic Servers

[Hermetic Servers](https://testing.googleblog.com/2012/10/hermetic-servers.html) blog post introduces the concept of hermetic server for testing.
Guidelines provided for hermetic server are very useful, as we can evaluate existing testing setup.

### Strategies for Testing Client-Server Interactions in Mobile Applications

[Strategies for Testing Client-Server Interactions in Mobile Applications](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/42109.pdf) paper talks about Google+ team's approach for using Record/ Replay mode using Hermetic server.
One more intersting part is smart JSON diffing which is something always requied in client-server testing.
e.g. last modified date will differ in record and replay modes.
