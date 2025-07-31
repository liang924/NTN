### DVB-S2X super-frame structure
<img width="1262" height="506" alt="image" src="https://github.com/user-attachments/assets/eaf57ad2-5e5b-4e44-a67f-cdc05d0516b7" />

**SOSF（Start of Super-Frame）** -- The SOSF contains a known sequence (preamble) that helps the receiver perform time synchronization, frequency synchronization, and carrier estimation. It is typically composed of predefined symbols and does not carry actual user data.

**SFFI（Super-Frame Format Indicator）** -- It is used to indicate the format (Format 0 to 7) adopted by the current super-frame. Different formats correspond to different PLFRAME types, payload sizes, modulation schemes, and other configurations. It is placed immediately after the SOSF (shown as the green block in the figure) and uses a small number of symbols to transmit the format index and essential control information.

**Format-Specific rules for resource allocation and content** -- This means that in the Payload section of the DVB-S2X Super-frame, both the content arrangement and resource allocation are determined based on the format (Format 0–7) indicated by the SFFI. Different formats (Format 0 to 7) may have different PLFRAME structures, modulation schemes (such as QPSK, 8PSK, 16APSK), FEC coding rates, pilot configurations, and support for beam hopping or VL-SNR applications.

### DVB-RCS2 super-frame structure 
<img width="634" height="739" alt="image" src="https://github.com/user-attachments/assets/bf9fc411-baeb-4929-b7b5-8b71224d8f91" />

**Super-frame** -- A super-frame is composed of multiple frames, and each frame is assigned a specific bandwidth and time duration based on user requirements.

**Frame** -- These small boxes are formed by the intersection of a timeslot and a frequency sub-channel, meaning that each box has a specific time interval and frequency range. They represent actual transmission resources that can be used to carry data. The system assigns these boxes to different users or purposes based on their needs.

**BTUs (Burst Time Units)** -- Each timeslot is further divided into several BTUs (Burst Time Units).A BTU is the smallest unit of resource allocation, used to transmit a burst of data.The left and right sides of the green block may represent different users or connections, with varying numbers of BTUs assigned based on their needs.

### 5G NR frame structure

<img width="1057" height="671" alt="image" src="https://github.com/user-attachments/assets/b925bbd5-21d5-40a4-b84a-5607f456e1a8" />

**Frame** -- A high-level time unit in 5G NR with a fixed duration of 10 ms.

**Subframe** -- Each frame is divided into 10 subframes, each lasting 1 ms. Each subframe can be further divided into 1 to x slots, and the number of slots depends on the numerology (parameter μ).
> For example:
> 
> Numerology μ = 0 ➜ slot duration is 1 ms ➜ each subframe contains 1 slot
> 
> Numerology μ = 1 ➜ slot duration is 0.5 ms ➜ each subframe contains 2 slots

The figure illustrates the difference between 15 kHz SCS (μ = 0) and 30 kHz SCS (μ = 1):

Green bar: 1 slot (14 OFDM symbols)

Yellow bar: 2 slots (each also contains 14 OFDM symbols)

**Slot** -- 	A subframe is further divided into 1 to 64 slots, depending on the numerology. Typically, a slot contains 14 OFDM symbols.

**SCS(Subcarrier Spacing)** -- The frequency spacing between subcarriers. It's determined by the numerology. For example: μ = 0 → 15 kHz; μ = 1 → 30 kHz.

**RE(Resource Element)** --	The smallest resource unit: 1 subcarrier × 1 OFDM symbol. Shown as a red square in the figure.

**PRB(Physical Resource Block)** --	A group of 12 subcarriers × 14 OFDM symbols. It is the fundamental unit of resource allocation for data transmission and reception. Shown as blue blocks.

### Comparison: 5G NTN Frame vs. DVB-S2X Super-frame vs. DVB-RCS2 Super-frame

| Aspect                     | **5G NTN (NR Frame)**                                                                 | **DVB‑S2X Super-frame**                                                   | **DVB‑RCS2 Super-frame**                                                    |
|----------------------------|----------------------------------------------------------------------------------------|---------------------------------------------------------------------------|----------------------------------------------------------------------------|
| **Usage Direction**     | General purpose (supports uplink & downlink), suitable for mobile communications       | Downlink (Gateway ➜ UE), supports broadcast and beam hopping              | Uplink (UE ➜ Gateway), supports multi-user time-shared transmission        |
| **Structure Unit**       | Frame ➜ Subframe ➜ Slot ➜ OFDM Symbol ➜ RE                                             | SOSF ➜ SFFI ➜ Payload (optionally includes SFH)                           | Super-frame ➜ Frame ➜ Timeslot ➜ BTU                                       |
| **Time Granularity**     | Frame = 10 ms; Subframe = 1 ms; Slot length depends on numerology (μ)                 | Super-frame length defined in number of symbols (e.g., 612,540 symbols)   | Flexible; each timeslot typically consists of hundreds of symbols          |
| **Format/Mode**         | Determined by numerology (μ = 0~4 → different SCS)                                     | Uses Format 0–7 to define payload rules (e.g., VL-SNR, Beam hopping)      | No format concept; uplink resources allocated dynamically by MAC layer     |
| **Minimum Unit**        | Resource Element (RE) = 1 OFDM symbol × 1 subcarrier                                   | Symbol groups with embedded sync and scrambling structure                 | Burst Time Unit (BTU)                                                      |
| **Reset Periodicity**   | No explicit scrambler reset; changes at slot/symbol boundaries                         | Scrambler reset occurs at beginning and end of each super-frame           | No scrambler reset; scheduling controlled by MAC                           |
| **Resource Allocation** | Uses BWP + PRB, dynamically adjusted based on UE status                                | SFFI defines pilot, PLFRAME, FEC settings per format                      | Uses DRA (Demand-based Resource Allocation) for uplink scheduling          |
| **Specialized Features**| Supports mobility, low-latency control, high throughput                                | Supports VL-SNR, beam hopping, broadcast content delivery                 | Supports multi-user dynamic uplink and high-capacity transmissions         |
| **Specification Source**| 3GPP TS 38.211, 38.214 (with NTN extensions)                                           | ETSI EN 302 307‑2 (Annex E)                                               | ETSI EN 301 545‑2 (includes MAC and uplink structure)                      |
