# Chapter 4

NAT: Network Address Translation
- One IP used for outbound datagrams from the router, and thousands of local IP's behind the router.
- Dynamic IP's rather than static IP's
- Routers play as a middle man for source addresses and ports to pretend to be many connections through one source.
- NAT is sometimes controversial because it manipulates data in layer 4.

ICMP: Internet Control Message Protocol
- Control bits for IP communication.
- Used to signal if hosts are down or to find routers.
# CIDR: Classless Inter Domain Routing
-- a.b.c.d/x x is the # of bits in subnet portion of address. (Network range.)

# DHCP: Dynamic Host Configuration Protocol
- Fourway handshake
- Goal: allow hosts to dynamically obtain IP address from network server.

* DHCP Discover
* DHCP Offer
* DHCP Request
* DHCP ACK

# Interplay between routing and forwarding.
-- Vocab
Routing: Finding the best path
Forwarding: Sending a packet along to an interface or to the router.

-- Notes
- Use graphs to calculate costs and factors in routing.
- Link State: Global knowledge of costs on routes.
- Distance Vector: Knowledge of neighbors cost only.

Link-State routing algorithm
- global knowledge shared by broadcasts

    c(x,y): link cost from node from x to y (if there's no link, infinite)
    D(v): current value of cost of path from source to dest v
    p(v): predecessor node along path from source to v
    N': set of nodes whose least cost path is definitely known

Dijstra's Algorithm (Link State)
- When you boot you only know who you are connected to.

    1  function Dijkstra(Graph, source):
    2      for each vertex v in Graph:                              // Initializations
    3          dist[v] := infinity ;                                // Unknown distance function from
    4                                                               // source to v
    5          previous[v] := undefined ;                           // Previous node in optimal path
    6                                                               // from source
    7
    8      dist[source] := 0 ;                                      // Distance from source to source
    9      Q := the set of all nodes in Graph ;                     // All nodes in the graph are
    10                                                              // unoptimized - thus are in Q
    11      while Q is not empty:                                   // The main loop
    12          u := vertex in Q with smallest distance in dist[] ; // Start node in first case
    13          remove u from Q ;
    14          if dist[u] = infinity:
    15              break ;                                         // all remaining vertices are
    16                                                              // inaccessible from source
    17
    18          for each neighbor v of u:                           // where v has not yet been
    19                                                                                 removed from Q.
    20              alt := dist[u] + dist_between(u, v) ;
    21              if alt < dist[v]:                               // Relax (u,v,a)
    22                  dist[v] := alt ;
    23                  previous[v] := u ;
    24                  decrease-key v in Q;                        // Reorder v in the Queue
    25      return dist;

Distance Vector Algorithm

    d_x(y): cost of least-cost path from x to y
    then
    d_x(y) = min_v { c(x,y) + d_v(y) } // Minimum of the routers you know about

Distance Vector (Bellman-Ford) Algorithm
- When a link's cost improves it doesn't take long to propagate and finish updating all router tables.
- When a link's cost decreases it takes longer to propagate and finish updating all router tables. (count to infinity problem)
- Poisoned Reverse: Tell that a route is shitty when it actually is.

BGP - Border Gateway Protocol
- eBGP: Obtain information from neihboring ASs (external BGP)
- iBGP: Propagate reachability information to all internal routers (internal BGP)
- Sessions: Exchanging messages to other peers
-- AS-PATH: Contains ASs through which prefix advertisement has passed
-- NEXT-HOP: Indicated specific internal-AS router to next hop AS.

BGP Messages
- OPEN: Opens TCP connection to peer and auth sender
- UPDATE: advertises new path
- KEEPALIVE: Keep the connecion alive in the absence of UPDATES
- NOTIFICATION: Reports errors in pervious msg. (Also used to close the connection)

# Test Material
- :: 6th Edition
- Chapter 3
-- TCP Fairness, Slow start, AIMD (my bandwidth vs your bandwidth)
-- Congestion control: Tahoe vs Reno
- Chapter 4
-- Forwarding vs routing
-- Virtual circuts (draw a circut diagram)
-- Switching Fabrics
-- IP Layout (But no IPv6) (only 4.4.1 and 4.4.2)
-- Routing Algorithms: Distance Vector and Link State
-- Netmasks and CIDR
-- Packet Fragmentation (8 byte bounries) (Happens at the IP level, so TCP header is fragmented too) (only one TCP header, multiple IP headers)
--- Question: Two routers with a different MSS, what do the packets look like at the final
--- Only the first packet has the TCP header, but each fragment has an IP header
--- Target host is the only one that reassembles anything.

    A ------O---------O---------------- B
       MTU       MTU      What do you
     1000-ish  700-ish    see here?


    H1                                          H2
    |        R1           R2          R3        |
    |       |  |         |  |        |  |       |
    --------   -----------  ----------  ---------
     ETH / IP   FDDI / IP    PPP / IP    ETH / IP
     MTU=1500   MTU=1400     MTU=532     MTU=532
                            (3 packets) (3 packets)

                            Packet Sizes: 512, 512, 376 (Remember, 20 byte IP header)

                            Flags: (3 bits for flags, 3 flags)
                            Fragmented - True (Turned off on last packet)
                            Offset - 0, 64, 128 (13 bits of space, so multiples of 8 are used.)
