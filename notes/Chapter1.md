# Networking notes

== Chapter 1
=== HW: Read Chapter 1

## Closer look at network structure

### Vocab

- Network Edge: Application and hosts (laptops)
- Access Networks: Wired, Wireless communication links
- Network Core: Interconnected routers, networks of networks
- DSL: Ditigal Subscriber Line
- ASDL: Asynchronus Digital Subscriber Line

Network Edge
- End systems: Web, Email, etc..
- Client / Server Model: Clients request from servers
- P2P: Distributed layout of clients and servers, no real orders

Cable Models
- Uses TV infrastructure rather than telephone
- HFC: Hybrid Fiber Coax
-- Up to 50mb down and 10mb up
- Dedicaed access that's shared between all of your neighbors.
- Internet -> Backbone -> Cable Headend -> Cable Clusters -> Fiber Node (Homes)

FDM: Frequency Division Multiplexer (Used to split data from TV signals)
- Every tv channel has a dedicated frequency
- Highest frequency is control line
- Next highest freq is the data lines
- Lowest frequency is tv lines

Fiber: Uses light
- OLT: Optical Line Terminator -- Moves from control office to the splitters
- ONT: Optical Network Terminator -- Moves from splitter to the homes

- POA: Passive Optical Network -- Few moving parts and uses optical switchers
- AON: Active Optical Network -- Uses ethernet uses hardware to route data

Ethernet Internet Access
- An ethernet switch which go between the router from the isp and computers
- Up to 42GBps speeds

Wireless Access
- 802.11b/g/n
- Wider-area networks: Setup for large areas

Home Networks
                                     - Ethernet
- Cable -> Modem -> Router/Firewall /
                                     - Wireless access

Twisted Pair -- Insumated copper wires
- CAT 3: Phone Wires - 10MBps
- CAT 5: 100MBps
The extra e on cables is additional twists in the cable.
- _|_ flow of electrons on pairs of wires. Causes resistence across wires.
- To minimize the angles, twist the pairs of wires so no felds are perpendicular

Coax -- Two connectors
- baseband: Legacy Ethernet, single channel
- boardband: Multiple channels, Hybrid fiber coax

Fiber
- Glass fiber carrying light.
- Each pusle is a bit, and very high speed
- Low error rate, (not distributed by electric fields or pulses)
- Repeaters are spaced far apart

Radio
- No physical wire, carried through electromagnetic spectrum.
- 3G ~ 1MBps

How does data get transfered throughout the net?
- Circut Switching
-- Guarantee bandwidth, similar to DSL, but it's reserved for you.
-- Unused resources are wasted

- Packet Switching
-- Dividing up all resources across all requets

Ex.
How long does it take to send a file of 640,000 bits from A to B over a
citcut-switched network?
- All link speeds: 1.536mbps
- Each link uses TDM with 24 slots/sec
- 500msec to establish end-to-end circuit

You get 1 slot / second
Your bandwidth = 1.536 * 10^6 / 24 = 6.4 * 10^4 (6.4KBps)
6.4 * 10^5 bits / 6.4 * 10^4 bits/sec
+ 500 msec
= 10.5 seconds

Packet Switching
- Don't divide the bandwidth equally, free-forall
- No setup, no overhead with establishing a connection.
- There can be starvation of the resources or congestion
- Packets wait in queues from hop to hop (switch to switch)
-- Switches that store and forward packets are called "Store and Forward"

Statistical Multiplexing
- Used in Packet Switching
- Equal statistical chance at every time packets can be sent.

Packet Vocab
- L: Length of the packet
- R: Rate at which you can transmit bits

Delays
- Transmission Delays

Packet Switching - Store and Forward
- takes L / R seconds to transmit a packet of L bits onto a link at R bits per second
- Routers wait until they can read a bit of the header before sending the packet on.
-- Needs to make sure that the header is intact, with a checksum
- Cut-Through switches will just stream the packet as they get it to the next location:port
- You add a bunch of delays when you have multiple links:
-- Assuming a propagartion delay of 0, the total delay will be kL/R, where k is the number of hops

Packet Switching vs Circuit Switching
- 10% of users will be active at any given time
- 1MB Link, 10kb/s per user
- Circuit Switching: Max 10 users
- Packet Switching: with 35 users, probability of > 10 users at the same time is 0.0004
- Packet Switching: Great for data in bursts, however, it can drop packets if the queue gets too full

How do we get that?
- 10 choose 35, 10!/((35-10)! * 35!)
-- Or: (.1^10 * ,9^25) for 10 to 0 and subtract it from 1

Internet Structure: Networks of Networks
- Tier-1 ISP: Verizon, Sprint, etc.. National and International Coverage
- Large Content Distributors: Google, Akamai, Facebook
- Treat each other as equals on these large scales.
- IXP: Internet Exchange Point
- Tier-2 ISP: Smaller and part of a range of Tier-1's net. Sometimes peer directly with other Tier-2's
- Tier-3 ISP: Local ISP's, customers of tier 1 or tier 2 networks (closest to end systems)
- Packets pass through many networks from their source to the destination.

- BGP: Border Gateway Protocol

- Delays
-- Processing, Queue, Transmission, Propagation
-- Transmission Delay
--- L/R
-- Propagation Delay
--- d: Length of physical link
--- s: Propagation Speed
--- d/s

Internet Protocol Stack
- Application: supporting network applications -- FTP, SMTP, HTTP
- Transport: Process to process transfer -- TCP, UDP
- Network: Routing of datagrams from source to destination -- IP/Routing PRotocols
- Link: Data transfer between neighboring network elements: Ethernet, 802.11
- Physical: Bits on the wire

ISO/OSI Reference Model
- Presentation: Allow applications to interpret meaning of data
-- encryption, compression, etc..
- Session: Synchronization, checkpointing, recovery of data
