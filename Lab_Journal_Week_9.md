# Lab Notebook Week 9
Supreeth Chinta

---

## Reflection

This week was much more productive. I came in on Tuesday feeling better and stayed for the full session. I worked on the HTTP server lab during class and also got all of my missing work checked off, including any Rustlings exercises I had not yet finished. Getting that backlog cleared felt like a real turning point after a couple of difficult weeks. The HTTP server assignment was the main new thing we were working on and it was genuinely interesting. The idea is that you build a small web server in Rust from scratch that listens for browser connections, reads what is being requested, and sends back the right response. It also uses a thread pool so multiple requests can be handled at the same time rather than one by one.

---

## Things I Need to Review

The thread pool was the part that required the most thought. The way it works is that when the server starts it creates a fixed number of worker threads that sit and wait for jobs. When a connection comes in it gets sent to the pool through a shared channel and one of the available workers picks it up. Because multiple workers share the same channel, there has to be a locking mechanism so only one worker can pull from it at a time. Getting the ownership model right so threads could share that channel safely without conflicting with each other took careful thinking about how Rust handles shared state between threads.

I also ran into a crash early on where the server would panic when a browser connected but did not send any data before dropping the connection. The server was not handling that empty case and just crashed instead of moving on. Understanding why that happened and fixing it was a good reminder that real programs need to handle edge cases that you might not think about right away. I also want to keep reviewing the exact format HTTP responses need to follow since getting the headers and line endings right was more detail-oriented than I expected.

---

## Goals

I want to stay on top of work going forward and not let a backlog build up again. I also want to keep thinking about concurrency and how thread pools work because those ideas come up in almost every real system. The server assignment gave me a solid foundation and I want to build on it.
