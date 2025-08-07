# DVB-RCS2
> [Reference](https://www.researchgate.net/publication/264358165_DVB-RCS2_overview?utm_source=chatgpt.com)

### 3.6. QoS Management

- The complete QoS system architecture is **revised and improved** in RCS2.
- Key elements:
  - Deciding the **QoS classes**.
  - Mapping QoS classes to **PHY/LL (Physical/Link Layer) resources**.
  - Tuning configuration **parameters at each level**.
  - Managing **Layer 2 control and management**.
  - Prioritization among various **traffic classes**.
- The system supports multiple:
  - **Coding and modulation options**
  - **Return channel formats**: Random Access (RA), Continuous Carrier (CC), and Multi-Frequency TDMA (MF-TDMA)
- This results in:
  - A **complex optimization challenge** for resource management.
  - No fixed algorithm is required, but the **capabilities must be defined**.
- Consistency across terminals:
  - Each terminal **advertises its capabilities** in a **harmonized manner** as per the **HLS (Higher Layer Specification)**.
- Benefits:
  - Operators can **tune optimization parameters** based on their own traffic profiles.
  - The system remains **flexible and upgradable** even as customer demands evolve.

### 3.7 Return Link Encapsulation

In IP communication systems with Adaptive Coding and Modulation (ACM), data fields are variable in length, and burst capacity can also change. This depends on the modulation scheme and the coding rate required under the given link conditions. IP data must be split and encapsulated into variable-sized containers for transmission over lower layers.

In the **forward link**, the system uses **Generic Stream Encapsulation (GSE)** over DVB-S2.  
In the **return link**, the techniques used in RCS1 are replaced by a new method called **Return Link Encapsulation (RLE)**.


### 3.8 Error Correction Coding

The main goal is to leverage recent advancements in coding performance. For short burst sizes on the return link, two turbo codes were proposed:

- A 16-state TurboΦ code  
- A 3D Turbo code  

These were extensions of the RCS1 coding scheme and developed by the same inventors.

After a comparative performance assessment, **TurboΦ** was chosen for RCS2 in linear modulation mode, based on the following findings:

- TurboΦ performs better than the eight-state 3D-TC in all but one test case, offering larger minimum distances in most cases.
- At eight decoding iterations, TurboΦ shows a 0 to 0.2 dB gain in the waterfall region; at five iterations, the gain can reach up to 0.3 dB.

The **coding gain** of TurboΦ compared to the RCS1 turbo code varies depending on modulation, coding rate, and burst size. However, it typically offers about **1 dB** improvement at low BER levels.  
This extra coding gain can help the system to:
- Reduce terminal transmit power, or  
- Increase the spectral efficiency of the system.

Additionally, the **DVB-RCS2 lower layer normative document** mandates:
- A combination of **convolutional coding** and **CPM (Continuous Phase Modulation)** for user terminals.  
- To allow future improvements in performance and spectral efficiency, a **generalized CPM waveform** has also been defined for potential use.

### 3.9 Antenna Alignment

One of the major cost factors in interactive satellite service installation is the effort required for antenna installation and alignment.

**Key Points:**

- **DVB-RCS2** provides signaling support for both **manual** and **automated alignment** of the user terminal antenna.
- Antenna alignment uses a **two-stage process**:
  1. **Forward link alignment** (done first)
  2. **Return link alignment** (starts only after the forward link is aligned)
- The return link alignment must meet **accuracy requirements specified by the gateway**.

**Advanced Support:**

- **Intelligent search algorithms** can:
  - Calculate **elevation** and **azimuth** angles of the user antenna.
  - Use **feedback from the gateway** for precise alignment.
  - **Minimize installation time** and **eliminate manual setup** if combined with motorized antenna control systems.

### 3.10 Security

Security in DVB-RCS2 is designed to provide:
- **Confidentiality**
- **Integrity**
- **Availability**
- **Non-repudiation**

#### Key Security Aspects in M-Planes and C-Planes:
- **Protection of channel activity**: e.g., hiding information on traffic volumes.
- **Protection of control/management information** for C-Plane and M-Plane signaling.
- **NCC and terminal authentication**: Only valid terminals can log on, preventing spoofing.

---

#### Broader Context:
- **Network-level security** is crucial for:
  - Government/military users
  - Corporate and consumer broadband subscribers
- Must meet expectations for **data privacy** and protection across different applications.

---

#### Challenge:
- **Security needs vary**:
  - From basic privacy to **military-grade encryption**
  - No one-size-fits-all solution is practical or cost-effective.

#### DVB-RCS2 Approach:
- Does **not mandate** specific security methods.
- Provides **general security guidelines** to allow flexible implementations.
- Examples of supported solutions include:
  - **FIPS-compliant** security for basic consumer needs
  - **TRANSEC** for secure military applications.

