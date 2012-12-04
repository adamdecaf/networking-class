# Chapter 5

Link Layer Services
- framing, link access
-- encapsulate datagram into from, adding header, trailer
-- channel access it shared medium
-- "MAC" address used in the frame headers to identify source, dest
--- different from IP address

- reliable delivery between adjacent nodes
-- seldom used on low bit-error link (fiber, some twisted pair)
-- wireless links: high error rates

- flow control
-- pacing between adjacent sending and receiving nodes

- error detection
-- errors caused by signal alteration
-- receiver detects presence of errors
--- signals sender for retransmission or drops frame

- error correction
-- receiver identifies and corrects bit errors

## Error detection

EDC: Error detection and correction bits
D: Data protected by error checking

Parity Checking
- single bit parity: detect single bit errors
- two dimensional bit parity: detect and correct single bit errors

Checksumming

    Let D be the data bits (as a binary number)
    Let r + 1 bit pattern, G
    Goal: Choose r CDC bits, R, s.t.
     <D,R> exactly divisible by G (mod 2)
     receiver knows G, divides <D,R> by G. (if the remainder is non-zero then there's an error)
     can detect all burst errors less than r+1 bits

Example

    Want:
        D2 XOR R = nG
     =
        D2 = nG XOR R
     =
        if we divide D2 by
        G, want remainer R


Ideal Multiple Access Protocol

- Broadcast channel of reate R bps
-- When one node wants to transmit, it can transmit at a rate of R
-- When M nodes want to transmit, each can send at an average rate of R/M
-- Fully decrentralized:
--- No special node to coordinate transmissions
--- no synchronization of clocks, slots

Random access protocol (Ethernet)
- Random access MAC protocol
-- how to detect collisions
-- how to recover from collisions

Carrier Sense Multiple Access
- Listen before you transmit
-- If the channel seems idle, wait the entire frame
-- If the channel seems busy, defer the transmission
-- When you notice a collision you send a runt frame (96 bits)

Ethernet
- dominate wired LAN technology

Frame structure

    -------------------------------------------------------------------------------
    |           |              |                |      |                  |       |
    |  Preamble | Dest Address | Source Address | Type |       Data       |  CRC  |
    |           |              |                |      |                  |       |
    -------------------------------------------------------------------------------

    Preamble:
     7 byte with pattern 10101010 followed by 10101011
     Used to sync clocks on receivers

     Dest Address: MAC address (6 bytes)
     Source Address: MAC Address (6 bytes)

     Type: Encoded protocol in the frame (IP, Novell IPX, AppleTalk)

Error Detection / Correction (Internet Checksums)
- Based upon polynomial division

    (x6 + x5 + x4 + x3 + x2 + 1) - (x6 + x4 + x3 + x + 1) =
    (x5 + x4 + x3 + x2 + x)

So, this really just becomes xor's!

    1101011001 -> x9 + x8 + x6 + x4 + x3 + 1
    10011 -> x4 + x + 1

    degree(G) = r (hence r+1 bits)
    degree(M) = m (or m+1 bits in frame)
    promote the frame's polynomial by r bits, so that it is degree(m+r)

    divide this polynomial by G(x) using polynomial division

               1100001000
           ______________
    10011 |11010110010000   <- Shift over by degree of generator
           10011 |      |
            10011|      |
            10011|      |
                010010  |
                 10011  |
                     1000

                    -> 11010110011000

ARP (Address Resolution Protocol) Protocol
- When a host wants to send a datagram but doesn't have the MAC address it will broadcast.
- Broadcast contains the source MAC address and who it is looking for. (So it can check back.)

Carrier Sense Multiple Access
- NIC receives datagram from network layer, creates frame
- If NIC is idle then transmit or wait if it's busy
- If NIC transmits transmits without another transmission NIC is done
- If NIC detects another transmission during it's transmission then abort and send jam signal
- After aborting, NIC enters exponentional back off after mth collision NIC chooses Kth
-- at random from {0, 1, 2,..., 2M - 1} NIC waits k * 512 bit times and returns to step 2

- Jam Signal: 48 bits of 1's
- Bit Time: .1 microsec for 10 mbps ethernet
