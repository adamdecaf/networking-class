# Chapter 4

NAT: Network Address Translation
- One IP used for outbound datagrams from the router, and thousands of local IP's behind the router.
- Dynamic IP's rather than static IP's
- Routers play as a middle man for source addresses and ports to pretend to be many connections through one source.
- NAT is sometimes controversial because it manipulates data in layer 4.

ICMP: Internet Control Message Protocol
- Control bits for IP communication.
- Used to signal if hosts are down or to find routers.
- CIDR: Classless Inter Domain Routing
-- a.b.c.d/x x is the # of bits in subnet portion of addreess. (Network range.)

DHCP: Dynamic Host Configuration Protocol
- Fourway handshake
- Goal: allow hosts to dynamically obtain IP address from network server.

* DHCP Discover
* DHCP Offer
* DHCP Request
* DHCP ACK
