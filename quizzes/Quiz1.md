# Quiz1 1
1)
    1000 bytes = 8000 bytes

    Transmission Delay
    8000 bits / 2x10^6 bits/sec = 8 / 2000seconds = 0.004 = 4msec

    Propagation Delay
    2500km / 2.5 x 10^5m/s = 1/100sec

2)

    Transmission Delay on first line = L/R1
    Transmission Delay on second line = L/R2
    Total = L/R1 + L/R2

3)

    4.5 packets ahead of you
    4.5 * 1500 bytes = 4.5*12000 bits = 540,000 bits

    Transmission Delay
    54000 / 2x10^6 bits/sec = 27/1000 seconds

4)
Yes, always worry about congestion control. What happens if packets are dropped due to outside factors.
Then, the packets that are dropped on a protocol that has reliable standards the dropped packets need to be
retransmitted.

Also, future growth has a factor, and it's smart to adjust for the future. (What if we grow?)
