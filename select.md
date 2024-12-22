# select() syscall

## Introduction
You might think that select() is for **asynchronous I/O**, but it is actually for **synchronous I/O multiplexing**. Don't worry, I'll explain **select()** and the concepts of **multiplexing** and **synchronous I/O** in detail. It may sound very complex at first but the I will simplify it.

## Explanation
Let’s consider a scenario where **select()** is helpful. Suppose you've written a server and client program using socket programming in C. When a client connects to the server, they may exchange messages for a few minutes. If another client tries to connect during this conversation, it would normally have to wait until the first client finishes.

Here’s where **select()** comes in. It allows the server to monitor multiple file descriptors (like client connections) and react to any activity. If a new client attempts to connect, or if an existing client sends a message, **select()** will notify the server, and the server can handle the request without waiting for the current client to finish.

**Multiplexing** means handling multiple streams of data in a single *process or thread* without creating separate processes for each. **Synchronous** means that the program waits (or "blocks") until an event happens, such as input data being available.

## Syntax
```
#include <sys/select.h>

int select(int nfds, fd_set *readfds, fd_set *writefds,
            fd_set *exceptfds, struct timeval *timeout);
```
`nfds (int nfds):` This argument specifies the highest-numbered file descriptor that you want to monitor, plus 1.
`readfds (fd_set *readfds):` This is a set of file descriptors that you want to check if they are ready for reading.
`writefds (fd_set *writefds):` This is a set of file descriptors you want to check if they are ready for writing.
`exceptfds (fd_set *exceptfds):` This is a set of file descriptors you want to check for exceptional conditions.
`timeout (struct timeval *timeout):` This is a timeout value that specifies how long select() should wait before returning. It is a time limit for how long select() should block and wait for an event to occur.
