# System definition 
#### 1. What does this system do?

It converts digital signals from MPEG transport stream multiplexers or generic sources  
→ into a format suitable for **satellite transmission**.

---

#### 2. What data formats are supported?

The system supports:
- **MPEG Transport Streams (TS)**
- **Generic Streams (GS)**
- And optionally **Multi-Protocol Encapsulation (MPE)**

---

#### 3. What is the design goal?

To achieve **Quasi Error Free (QEF)** transmission quality.

---

#### 4. What does QEF mean?

If signal quality is good (above C/N+I threshold):
- At a bitrate of 5 Mbps (e.g., single TV service),
- There will be **less than one uncorrected error per hour**
- Meaning: **Packet Error Ratio (PER) < 10⁻⁷**

---
# System architecture
<img width="926" height="497" alt="image" src="https://github.com/user-attachments/assets/b0b6ce0b-0bd1-44e6-a389-f68fffcc702e" />

#### 1. Mode Adaptation
- Accepts one or more **input streams** (e.g., MPEG-TS or Generic Streams)
- Performs optional steps:
  - Synchronization
  - Null-packet deletion (for ACM/TS)
  - **CRC-8 encoding** for error detection
- Buffers and slices the input into data chunks
- Adds **Base-Band Signalling**

#### 2. Stream Adaptation
- Adds **padding** if needed to align with Base-Band Frame size
- Scrambles data for energy distribution

#### 3. FEC Encoding
- **BCH encoder**: corrects burst errors
- **LDPC encoder**: adds powerful forward error correction (FEC)
- **Interleaver**: shuffles bits for better robustness

#### 4. Mapping
- Converts coded bits into **modulation symbols**
- Supports QPSK, 8PSK, 16APSK, 32APSK (with Gray mapping)

#### 5. PL Framing
- Adds **Physical Layer Header**
- Inserts **pilot symbols** (optional)
- Generates PLFRAMES for transmission

#### 6. Modulation
- Applies **Base-Band Filtering** using root-raised cosine filter
- Final step: **Quadrature Modulation** to RF

---
