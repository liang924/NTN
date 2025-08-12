# Functional block diagram of the DVB-S2 System
<img width="206" height="414" alt="image" src="https://github.com/user-attachments/assets/cc43c237-59da-4fe2-890e-75edeff3502f" />

## Mode Adaptation
<img width="301" height="667" alt="image" src="https://github.com/user-attachments/assets/6c688efd-bb51-4698-88ee-dc4fdefcd20a" />

### Input Stream Synchronization?

 **Input Stream Synchronization** ensures that data packets are aligned in time and structure before further processing, such as slicing or framing.  
 It is especially important when dealing with **multiple input sources** or **streams with timing jitter or drift**.

### When to Use Input Stream Synchronization

| Condition                                                                 | Required         | Reason                                                                                  |
|---------------------------------------------------------------------------|------------------|------------------------------------------------------------------------------------------|
| **Input consists of multiple input streams**                              | ✅ Required       | Timing across sources is inconsistent and must be aligned.                              |
| **Input is a Packetized Stream (unsynchronized)**                         | ✅ Recommended    | Ensures correct packet start alignment and avoids misaligned packets.                   |
| **Input is a Raw Bitstream or GSE Encapsulation (unsynchronized)**       | ✅ Recommended    | No sync signal is present; stream alignment is needed.                                  |
| **Input is a single source with time synchronization (e.g., TS with PCR)**| ❌ Can be skipped | Timing reference is available; no need to re-synchronize.                                |
| **Input has Constant Bit Rate (CBR) and does not rely on timestamps**     | ❌ Can be skipped | Stream is stable; misalignment is unlikely.                                              |
| **Input comes from a synchronized front-end (e.g., pre-processed modulator)** | ❌ Can be skipped | Data has already been aligned; synchronization module is not needed.                    |

---

### Transport Stream (TS)
Transport Stream is a transmission format defined by the MPEG-2 standard and is widely used in digital television and satellite communications. It encapsulates multiple types of data—such as video, audio, and subtitles—into a continuous data stream. Each packet has a fixed length of 188 bytes and includes a sync byte to help decoders align the data. TS is particularly suitable for unstable transmission environments due to its built-in error correction and synchronization mechanisms, and it is a common input format in DVB-S2/S2X systems.

### Adaptive Coding and Modulation (ACM)
Adaptive Coding and Modulation (ACM) is a technique that dynamically adjusts the modulation scheme and coding rate based on real-time channel conditions. When signal quality is good, the system uses higher-order modulation (e.g., 32APSK) and less error protection to maximize bandwidth efficiency. When the channel quality degrades (e.g., due to bad weather), it switches to more robust modulation and stronger error correction to ensure data integrity. ACM plays a key role in DVB-S2/S2X systems, allowing each receiver to obtain transmission parameters that best suit its conditions, thereby improving overall system performance.

### Why is "Is input type TS + ACM?" a conditional decision?

This decision point exists because **Null-Packet Deletion** is only applicable under specific conditions:

- The input data format is **Transport Stream (TS)** 
- The mode used is **ACM (Adaptive Coding and Modulation)**.

Only when both conditions are met will the system perform null-packet deletion, which helps improve bandwidth efficiency and enhances error protection in the modulator.
If the input is a **Generic Stream** (which does not include null packets), or if **CCM (Constant Coding and Modulation)** is used instead of ACM, this process is skipped.

###  Null-Packet Deletion (Applicable to ACM and Transport Stream Only)

- **Condition**: This process is applied **only when the input is in ACM mode** and the format is **Transport Stream (TS)**.
- **Operation**: The system identifies **MPEG null-packets** (with PID = 8191<sub>D</sub>) and removes them before modulation.
- **Purpose**:
  - Reduce the overall information transmission rate.
  - Enhance error protection performance in the modulator.
- **Receiver Recovery**: The removed null-packets are **re-inserted at the receiver** in their original positions to maintain data integrity.
- **Specification**: This process must comply with the specifications defined in **Annex D** of the standard.

###  Why is "Is input packetized?" an optional step?

1. **Different Input Types**  
   In DVB systems, input data may come from various sources, such as:

   - **Packetized formats**: e.g., MPEG Transport Stream (TS), which has a clear packet structure.
   - **Continuous byte streams**: e.g., certain streaming modes or non-standard data sources, which have no explicit packet boundaries.

2. **CRC checking is only applicable to packetized input**

   - If the input is packetized, each packet can be appended with **CRC-8 coding** to enable error checking at the receiver side.
   - If the input is a continuous stream, there is no defined "packet" unit, so **packet-level CRC cannot be applied**, and this step is skipped accordingly.

### CRC-8 Encoding (For Packetized Data Only)

#### When is it needed?

- If the input is a **continuous data stream** (UPL = 0): **no processing is needed**, transmit directly.
- If the input is **packetized** (UPL ≠ 0, fixed-length packets with a sync-byte): **CRC-8 encoding must be applied**.

#### How does it work?

1. **Remove the sync-byte at the beginning of each packet**.
2. Apply CRC-8 encoding to the remaining data (using a predefined polynomial).
3. The **computed CRC value** will **replace the sync-byte of the next packet**.

#### Why is it useful?

- It helps **detect transmission errors**.
- The CRC is generated on the sender side and can be used by the receiver to **verify data integrity**.

