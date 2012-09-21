# Chapter 3

Basics for communication.

IP does not deal with ports, but TCP and UDP do handle ports. UDP/TCP is built upon IP so it relies on the IP packet.


                  0      7 8     15 16    23 24    31
                 +--------+--------+--------+--------+
                 |     Source      |   Destination   |
                 |      Port       |      Port       |
                 +--------+--------+--------+--------+
                 |                 |                 |
                 |     Length      |    Checksum     |
                 +--------+--------+--------+--------+
                 |
                 |          data octets ...
                 +---------------- ...

                      User Datagram Header Format

Note: UDP is used in most streaming communications. Because you can drop a frame here and there and the eye won't matter.

Internet Checksum
- Adds up the numbers in one's compliment to then wrap around the extra bit to be added to the result of the previous result.

IP Packets are not reliable, so how do we make communications on them reliable?
- Attempt to use reliable layers (senders and receivers) with unreliable layers to send data.

Reliable Data Transport 1.0
- Assume everything is fine and we just send and recieve

Reliable Data Transport 2.0
- Corruption
-- ACK (acknowledgement)
-- NAK (negative acknowledgement)
- Uses these (along with an FSM to build up)

Reliable Data Transport 2.1
- What if the ACK or NAK are corrupted?
-- Sequence numbers. (0 or 1) to signal so the receiver knows if this is a retransmitted packet or not.

Reliable Data Transport 2.2
- NAK less protocol
- Instead of sending a NAK you can send an ACK for the last packet received.

Reliable Data Transport 3.0
- underlying channel can loose packets (data or ACK's)
- So.... we can introduce a timer
- and keep track of retransmits
- set of FSM's that wait for the ack on the packet to be ACK'd to continue back on the next packet.
