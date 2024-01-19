## Link Layer

### Error Detection

#### Parity Checking

- **Even parity** used: parity bit set to `1` if count of `1` in data bits is odd so that the count of `1` is always even.

- **2D bit parity** can detect and correct single bit errors.

  ```
  1 1 1 0 | 1
  0 0 1 1 | 0
  1 1 1 1 | 0
  0 0 0 0 | 0
  --------+---
  0 0 1 0 | 1
  ```

#### Internet Checksum

- Used by IP, UDP, TCP.

#### Cyclic Redundancy Check (CRC)

Given:

- $D$: data of $d$ bits
- $G$: generator (bit pattern) of $r+1$ bits

To:

- Choose $r$ CRC bits, $R$, such that <$D,R$> exactly divisible by $G$ (mod 2)

CRC can detect all burst errors less than $r+1$ bits.

##### Calculation of CRC

$R = remainder[\frac{D \times 2^r}{G}]$

1. **Append $r$ zero bits** to the end of your data $D$. This will give you the modified data which we'll call $D'$.
2. **Divide $D'$ by $G$** using **binary division**, not long division. Remember that in binary division, subtraction is equivalent to addition (**XOR** operation).
3. **Keep track of the remainder**. Once you have completed the division, the remainder will be $r$ bits long. This is your CRC, $R$.
4. **Replace the $r$ zero bits** at the end of $D'$ with the remainder $R$. This gives you the final codeword <$D,R$> that is exactly divisible by $G$.

### Multiple Access Protocol

#### Channel Partitioning

- **TDMA**: Time
- **FDMA**: Frequency

#### Random Access

- **Slotted ALOHA**:
  - Time divided into slots (transmit 1 frame)
  - If collision, retransmit in next frame with probability $p$ until success.
- Simple **CSMA **(Carrier Sense Multiple Access)
  - Channel sensed idle => transmit entire frame
  - Channel sensed busy => defer transmission
- **CSMA/CD** (Collision Detection)
  - Collision detected: abort transmission & backoff
  - Exponential backoff: after $m$ th collision, back off `[0, 1, 2, ..., (2^m)-1].pickRandom() * 1 frame time`.

#### Taking Turns

- **Polling**: Master decides which node to transmit. Nodes poll the master.
- **Token Passing**: Node with token transmits. Token passed sequentially.

### LAN

#### MAC Address

- **Length**: 48 bits

#### ARP (Address Resolution Protocol)

- ARP Table: `Map<IPAddr, (MACAddr, TTL)>`

- **Example**: A wants to send datagram to B
  1. A send query: `{ SourceMAC: A's, SourceIP: A's, TargetMAC: FF-FF-FF-FF-FF-FF (Broadcast), TargetIP: B's }`
  2. B replies: `{ SourceMAC: B's, SourceIP: B's, TargetMAC: A's, TargetIP: A's }`
  3. A records `<IPAddr, (MACAddr, TTL)>` in ARP table.

#### Ethernet

- Connectionless
- Unreliable
- Uses CSMA/CD with binary (exponential) backoff

##### Ethernet Frame

- **Preamble (8 bytes)** 
- **Destination MAC Address (6 bytes)**
- **Source MAC Address (6 bytes)**
- **Type/Length (2 bytes):** Indicates the type of protocol inside the frame or the length of the payload.
- **Data and Pad (46-1500 bytes):** The actual data being transported, which is padded to meet the minimum length requirement for the frame.
- **CRC (4 bytes)**

#### Switches

- Switch forwarding table: `Map<MACAddr, (Interface, TTL)>`
- **Self-learns** received frames to fill the table.
  - **Flood** (send to all ports except the receiving port) if destination MAC address is unknown.

### WLAN

#### CSMA/CA (Collision Avoidance)

**Sender**

- Channel sensed idle for **DIFS** => transmit entire frame & wait for ACK
- Channel sensed busy => backoff for random time
- No ACK => backoff for increased time

**Receiver**

- Frame received OK => return ACK after **SIFS**

**RTS (Request to Send) - CTS (Clear to Send) Exchange**

1. Sender sends RTS to BS (Base Station)
2. BS broadcasts CTS
3. Heard CTS, sender transmits frame.