# Networking notes

== Chapter 2 -- Application Layer

2.1 - Principles of network applications
- Clients: Start conversations with servers
- Focused on clients and servers talking.

P2P
- No such client-server connections here, just peers talking to each other

Hybrid
- Skype
-- Clients connect to the server to figure out what others are online and to start connections
-- Clients then connect directly to another client for calls

Sockets
- Processes send and receive messages from through the socket

Web & HTTP
- uri's !!!!
- Most web servers support persistent http connections
- TCP slow start: Sending 1, 2, 4, ... packets to establish a solid connection
- Caching
