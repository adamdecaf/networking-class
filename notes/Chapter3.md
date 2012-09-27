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

.... Something

TCP Round Trip Time and Timeout

- Setting the timeout

    EstimateRTT = (1 - a) * EstimatedRTT + a * SampleRTT
    Typically, a = 0.125

    EstimatedRTT plus a buffer
    DevRTT = (1 - b) * DevRTT + b * |SampleRTT - EstimatedRTT|
    Typicallt, b = 0.25

    TimeoutInterval  = EstimatedRTT + 4 * DevRTT

TCP Reliable Data Transfer
- TCP creates reliability ontop of IP's unreliable service.
- Pipelined segments
- Cumulative acks (one ack can work for all previous packets)
- TCP uses a single retransmission timer
- retransmits are triggered by: timeout events or duplicate acks

Vocab
- Flow control: Not sending too many packets to the receiver
- Congestion Control: Not sending too many packets over the link

TCP sender events
- Data rcvd from app
-- Create segment with seq number
-- seq number if byte-stream number of first data byte in segment
-- start timer if not already running
- timeout
-- restransmit segment that cased a timeout

TCP Flow Control
- Don't send too many packets to the receiver
- Buffer size is sent along TCP packets to tell the other party how much to send

TCP Connection Management

- TCP Handshake
-- 1) Client sends TCP SYN to the server with initial seq number. (no data)
-- 2) Server host receives SYN replies with SYNACK segment
-- 3) Client gets a SYNACK and replies with an ACK that may contain data.
SYN -> SYN ACK -> ACK

- TCP Teardown
-- client end system sends TCP FIN control segment to server
-- server gets a FIN and replies with an ACK
-- client gets the ACK and a FIN and sends an ACK back to the server
-- (server can start this too)
FIN -> (ACK, FIN) -> ACK
