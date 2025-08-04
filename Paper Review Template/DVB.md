> Reference https://www.etsi.org/deliver/etsi_ts/101500_101599/10154501/01.03.01_60/ts_10154501v010301p.pdf
## System Architecture

<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/e1d7dde9-4c60-40d0-8a75-fcfe42e279e5" />

### 1. Transparent Architecture

- The satellite functions only as a signal repeater (no processing capability).
- RCST (Return Channel Satellite Terminal) communicates bidirectionally with the gateway via satellite links.
- Applicable to **star topology** or **mesh overlay topology**.
- **Main Components**:
  - **Transparent Satellite(s)**: No processing capability, pure signal forwarding.
  - **Hub / NCC / NMC**: Responsible for overall network control and management.
  - **RCST**: Terminal device that receives control information and transmits return link data.
  - **GW-RCST**: Gateway-type terminal that connects to terrestrial networks.
  
<img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/e63e28d3-4d6d-4498-adaa-ad780d25c570" />

### 2. Regenerative Architecture

- The satellite is equipped with an **On-Board Processor (OBP)** capable of demodulation, re-encapsulation, and packet forwarding.
- Supports **single-hop mesh topology**, suitable for high-speed point-to-point or point-to-multipoint applications.
- **Main Components**:
  - **Regenerative Satellite (OBP)**: Performs demultiplexing, routing, and packet encapsulation.
  - **Regenerative RCST**: Terminal that communicates directly with OBP in a single hop.
  - **Regenerative GW-RCST**: Gateway terminal supporting terrestrial network access.
  - **NMC / NCC**: Provides management and control plane functions.

 ## DVB-RCS2 actors and roles
 <img width="600" height="300" alt="image" src="https://github.com/user-attachments/assets/f2dce364-35ad-4e8b-9dc7-f893776bba6f" />

1. **Satellite Operator (SO)**
   - Manages the entire satellite system.
   - Sells transponder capacity to one or more Satellite Network Operators (SNOs).
2. **Satellite Network Operator (SNO)**
   - Owns one or more transponders and NCC/NMC.
   - Responsible for the time and frequency plan of a DVB network.
   - May divide the interactive network into multiple Operator Virtual Networks (OVNs), managed by SVNOs.
   - In the transparent architecture, the SNO owns the TS-GW (Transparent Satellite Gateway).
3. **Satellite Virtual Network Operator (SVNO)**
   - Assigned one or more OVNs with specific physical and logical resources.
   - Each RCST can only be assigned to one OVN at logon.
   - Each OVN is allocated a pool of SVN numbers to assign SVN-MAC addresses.
   - SVNOs provide connectivity services and may manage one or more RSGWs (Regenerative Satellite Gateways) in regenerative architectures.
4. **Subscriber (RCST)**
   - User terminal equipment that connects to the SVNO network.
5. **End-user**
   - The final users accessing satellite services through the RCST LAN interface.

### Protocol Architecture

<img width="500" height="750" alt="image" src="https://github.com/user-attachments/assets/75ae7bbd-f5b2-40c0-9f84-fca1e4b492e7" />

### 1. Physical Layer (L1)
- Forward Link uses DVB-S2 or DVB-S2X with Generic Stream Encapsulation (GSE).
- Return Link uses MF-TDMA with CRDSA and Return Link Encapsulation (RLE).
- Supports various modulation and coding schemes based on terminal profiles.
### 2. MAC / Access Layer (L2)
- Implements Demand Assignment Multiple Access (DAMA) and Slotted Aloha.
- Provides traffic classification and Quality of Service (QoS).
- Common Signaling Channel (CSC) manages link control and access.
### 3. Dynamic Connectivity Protocol (DCP)
- Supports dynamic connection setup in mesh topologies.
- Operates between MAC and Network layers for on-demand route establishment.
### 4. Network Layer (L3)
- Supports IPv4 and IPv6.
- Implements DHCP, static and dynamic routing (including OSPF).
- Includes multicast support, DiffServ QoS, and optional MPLS.
### 5. Management & Control Plane
- Uses SNMP v2c/v3, SDDP (Software and Data Distribution Protocol).
- Supports XML-based configuration and PEP negotiation.
- Enables remote control via HTTP and CLI.
- Manages RCST configuration, software updates, and antenna controls.
### 6. Security Layer
- Provides link-layer encryption (TRANSEC) for both user and control data.
- Supports TRANSEC_Certificate and TRANSEC_Chaff protocols.
- Enhances confidentiality, integrity, and protection against attacks.

### DVB-S2X super-frame structure
<img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/eaf57ad2-5e5b-4e44-a67f-cdc05d0516b7" />

**SOSF（Start of Super-Frame）** -- The SOSF contains a known sequence (preamble) that helps the receiver perform time synchronization, frequency synchronization, and carrier estimation. It is typically composed of predefined symbols and does not carry actual user data.

**SFFI（Super-Frame Format Indicator）** -- It is used to indicate the format (Format 0 to 7) adopted by the current super-frame. Different formats correspond to different PLFRAME types, payload sizes, modulation schemes, and other configurations. It is placed immediately after the SOSF (shown as the green block in the figure) and uses a small number of symbols to transmit the format index and essential control information.

**Format-Specific rules for resource allocation and content** -- This means that in the Payload section of the DVB-S2X Super-frame, both the content arrangement and resource allocation are determined based on the format (Format 0–7) indicated by the SFFI. Different formats (Format 0 to 7) may have different PLFRAME structures, modulation schemes (such as QPSK, 8PSK, 16APSK), FEC coding rates, pilot configurations, and support for beam hopping or VL-SNR applications.

### DVB-RCS2 super-frame structure 
<img width="400" height="600" alt="image" src="https://github.com/user-attachments/assets/bf9fc411-baeb-4929-b7b5-8b71224d8f91" />

**Super-frame** -- A super-frame is composed of multiple frames, and each frame is assigned a specific bandwidth and time duration based on user requirements.

**Frame** -- These small boxes are formed by the intersection of a timeslot and a frequency sub-channel, meaning that each box has a specific time interval and frequency range. They represent actual transmission resources that can be used to carry data. The system assigns these boxes to different users or purposes based on their needs.

**BTUs (Burst Time Units)** -- Each timeslot is further divided into several BTUs (Burst Time Units).A BTU is the smallest unit of resource allocation, used to transmit a burst of data.The left and right sides of the green block may represent different users or connections, with varying numbers of BTUs assigned based on their needs.


## 🔹 Section 9.5: Return Link Timeslot Grid Control

**Objective:**  
To manage and arrange the timeslot configuration on the return link for efficient and flexible resource allocation.

**Key Points:**

- **Control Entities:**  
  The timeslot grid can be managed by the SCT (Superframe Composition Table), FCT2 (Frame Composition Table v2), and BCT (Broadcast Configuration Table), either independently or in combination with TBTP2 (Terminal Burst Time Plan Table v2).

- **Dynamic Adjustment:**  
  The timeslot structure supports dynamic operation. The TBTP2 can decide in real-time which unit timeslots to use, potentially aggregating adjacent timeslots into larger ones to accommodate larger burst transmissions.

- **Overlapping Frame Management:**  
  Supports overlapping frame configurations within the superframe sequence. The NCC (Network Control Center) may alternate allocation across these overlapping frames to optimize utilization.

---

## 🔹 Section 9.6: Timeslot Access Method Control

**Objective:**  
To determine the media access method used in each timeslot (e.g., random access or dedicated access).

**Key Points:**

- **Access Method Determination:**  
  The access method for each timeslot is decided either by the FCT2 or TBTP2.

- **Dedicated Access:**  
  Timeslots assigned explicitly for a specific RCST are determined by TBTP2, ensuring guaranteed quality of service.

- **Random Access:**  
  Timeslots used for shared, bursty transmission needs may be configured by either FCT2 or TBTP2.

- **Continuous Transmission Control:**  
  If a timeslot is used for continuous transmission, this may be preconfigured either via TBTP2 or through a CC Control Descriptor delivered in a TIM-U message.

---
