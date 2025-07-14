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
### 🧩 1. Mode Adaptation
- Accepts MPEG-TS or Generic Streams
- Optional functions:
  - Input stream synchronization
  - Null-packet deletion (for ACM or TS)
  - CRC-8 encoding for error detection
  - Slicing into data fields
  - Add **Base-Band Header (BBHEADER)**

### 🧵 2. Stream Adaptation
- Pads data to match base-band frame size
- Scrambles data for energy dispersal

### 🛡 3. FEC Encoding
- **BCH Encoder**: burst error correction
- **LDPC Encoder**: powerful forward error correction
- **Interleaving**: improves noise robustness

### 🔄 4. Mapping
- Bit-to-symbol mapping (QPSK, 8PSK, 16APSK, 32APSK)
- Gray-mapping used

### 🧱 5. PL Framing
- Adds **PLHEADER**
- Inserts optional **pilot symbols**
- Outputs **PLFRAME**

### 📡 6. Modulation
- Root-raised cosine filter (roll-off: 0.35 / 0.25 / 0.20)
- Final RF signal via I/Q modulation

---

## ✨ 3. Key Enhancements in DVB-S2X

### ✅ MODCODs & Filtering
- Finer MODCOD steps
- Sharper roll-off filters

### ⚡ Efficiency
- Time-slicing of wide-band signals
- Multi-transponder bonding

### 🧭 Advanced Signaling
- Optional **Super-frame** structure
- Extended **PLHEADER** for:
  - More MODCODs
  - Mobile Frame (VL-SNR)
- **GSE-HEM** mode: higher BBFRAME efficiency
- **GSE-Lite** stream signaling

### 🛰 Beam-Hopping (Annex E)
- Periodic and random beam switching
- Supports VL-SNR down to -10 dB

---
