## Transport Layer

### Internet Checksum

#### 1's Complement Sum

1. Change all 1's to 0's and all 0's to 1's (1's complement form)
2. Add together.
3. If there is a carry out of the most significant bit (leftmost), add this carry back into the least significant bit (rightmost) of the sum. This is called an **end-around carry**.

#### Calculation of Internet Checksum

1. Divide data into 16-bit words.
2. Add together using 1's complement sum.

### Reliable Data Transfer

#### Stop-And-Wait

#### Go-Back-N

**Sender**

- Window of up to $N$ packets (`nextseqnum - send_base < N`)
- Cumulative `ACK(n)`: ACKs all up to `#n`
- Timeout of `#n`: retransmit all higher than `#n`

**Receiver**

- Only ACK correct one with highest seqnum (`rcv_base - 1`)
- May buffer out-of-order packet

#### Selective Repeat

### TCP RTO

1. **For Estimated RTT:**
   $ \text{EstimatedRTT} = (1 - \alpha) \cdot \text{EstimatedRTT} + \alpha \cdot \text{SampleRTT} $
   where $ \alpha $ is a constant weight (typically, $\alpha = 0.125$).
2. **For DevRTT (the estimate of RTT variability):**
   $ \text{DevRTT} = (1 - \beta) \cdot \text{DevRTT} + \beta \cdot |\text{SampleRTT} - \text{EstimatedRTT}|$
   where $ \beta $ is a constant weight (typically, $\beta = 0.25$).
3. **For the Timeout Interval:**
   $ \text{TimeoutInterval} = \text{EstimatedRTT} + 4 \cdot \text{DevRTT} $

### Overhead

- TCP: 20 bytes
- UDP: 8 bytes
