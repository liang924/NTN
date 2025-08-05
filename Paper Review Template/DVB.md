> Reference https://www.etsi.org/deliver/etsi_ts/101500_101599/10154501/01.03.01_60/ts_10154501v010301p.pdf
# System Architecture

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

 # DVB-RCS2 actors and roles
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

# Protocol Architecture

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

# DVB-S2X super-frame structure
<img width="600" height="400" alt="image" src="https://github.com/user-attachments/assets/eaf57ad2-5e5b-4e44-a67f-cdc05d0516b7" />

**SOSF（Start of Super-Frame）** -- The SOSF contains a known sequence (preamble) that helps the receiver perform time synchronization, frequency synchronization, and carrier estimation. It is typically composed of predefined symbols and does not carry actual user data.

**SFFI（Super-Frame Format Indicator）** -- It is used to indicate the format (Format 0 to 7) adopted by the current super-frame. Different formats correspond to different PLFRAME types, payload sizes, modulation schemes, and other configurations. It is placed immediately after the SOSF (shown as the green block in the figure) and uses a small number of symbols to transmit the format index and essential control information.

**Format-Specific rules for resource allocation and content** -- This means that in the Payload section of the DVB-S2X Super-frame, both the content arrangement and resource allocation are determined based on the format (Format 0–7) indicated by the SFFI. Different formats (Format 0 to 7) may have different PLFRAME structures, modulation schemes (such as QPSK, 8PSK, 16APSK), FEC coding rates, pilot configurations, and support for beam hopping or VL-SNR applications.

# DVB-RCS2 super-frame structure 
<img width="400" height="600" alt="image" src="https://github.com/user-attachments/assets/bf9fc411-baeb-4929-b7b5-8b71224d8f91" />

**Super-frame** -- A super-frame is composed of multiple frames, and each frame is assigned a specific bandwidth and time duration based on user requirements.

**Frame** -- These small boxes are formed by the intersection of a timeslot and a frequency sub-channel, meaning that each box has a specific time interval and frequency range. They represent actual transmission resources that can be used to carry data. The system assigns these boxes to different users or purposes based on their needs.

**BTUs (Burst Time Units)** -- Each timeslot is further divided into several BTUs (Burst Time Units).A BTU is the smallest unit of resource allocation, used to transmit a burst of data.The left and right sides of the green block may represent different users or connections, with varying numbers of BTUs assigned based on their needs.


> Reference https://www.etsi.org/deliver/etsi_en/301500_301599/30154502/01.04.01_60/en_30154502v010401p.pdf

# Section 9.5: Return Link Timeslot Grid Control

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

# Section 9.6: Timeslot Access Method Control

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
# 9.7
## 9.7.1 Random Access Load Control for Logon

### 9.7.1.1 Stationary RA Load Control for Logon

**Purpose:**  
- Control the normal operating load level on the logon channel  
- Limit autonomous transmission intensity to comply with regulatory requirements

**Mechanism Description:**
- When an RCST sends an RA logon request without receiving a response or if rejected, it must apply a random hold-off interval before retransmitting.
- Retransmission parameters are provided by the NCC through the `Logon Contention Descriptor` (delivered in TIM-B).

**Initial Logon Attempt:**
- Hold-off interval is a uniformly distributed random variable in the range `[0, max_time_before_retry]`, defined by the NCC.

**Retransmission on Failure:**
- If the logon attempt fails without response, further retransmission occurs after a uniformly distributed random interval in the range `[0, n² × max_time_before_retry]`, where `n` is one more than the number of consecutive failures.

**Resetting the Counter `n` to 1:**
- RCST receives a logon response `TIM-U`
- NCC sets either:
  - Link Failure Recovery flag
  - Logon Link Failure Recovery flag in `TIM-B`
- RCST is explicitly woken up by a `TIM-U`
- A local operator manually restarts the logon procedure
- RCST connects to the forward link of another network (identified by NIT-ONID and RMT-INID)

**Note:**  
- Automatic return to the "Off/Standby" state **does not** reset `n`.

### 9.7.1.2 Dynamic RA Load Control for Logon

**Features and Operation:**
- The `max_time_before_retry` parameter from the stationary load control may be modified at runtime by the NCC.
- For large-scale outage recovery, the NCC may set the `Link Failure Recovery` flag in `TIM-B` to instruct the RCST to follow a predefined recovery procedure.
- This predefined procedure is **implementation dependent**.

## Section 9.7.2: Contention Control for Control Timeslots (Optional)

#### 1. Functional Overview

- **The RCST may optionally use contention control timeslots** to transmit control signals.
- This mechanism is **not mandatory**.
- Main usage scenario:
  - When **dedicated resources are insufficient** for sending capacity request signals, this serves as an alternative.
- **The actual utilization policy is implementation dependent**.

---

#### 2. Stationary RA Load Control for Control Signals (9.7.2.1)

- **The NCC defines the parameter `default_control_randomization_interval` in the TIM-U’s Lower Layer Service Descriptor**:
  - It specifies the **minimum randomization interval** for selecting a control timeslot using slotted ALOHA.
  - The RCST must **uniformly and randomly select one control timeslot** within this interval for transmitting control signals.
  - The set of control timeslots is provided by **SCT, FCT2, and TBTP2**, and is included in the **Superframe Specification (SFS)**.

- **Special condition — when the parameter is set to 255**:
  - The RCST shall interpret this as "**RA control signalling is not allowed**", even if control timeslots are present.

## 9.7.3 Contention Control for Traffic Timeslots

**Random Access Load Control Mechanism for Traffic Transmission Timeslots**

---

### 9.7.3.0 Introduction

- **Assignment of Control Mechanism**:
  - Each RA allocation channel statically receives its load control method via the `Random Access Traffic Method Descriptor`.
  - If `load_control_method = 0`:
    - It means **no load control is applied**, and upper-layer mechanisms are expected to regulate traffic flow.
  - If the value is non-zero:
    - The RCST must implement **stationary load control**, unless **dynamic control is enabled**.

- **RA Blocks**:
  - The superframe is divided into **RA blocks**, which serve as the basic units for load control.
  - If unspecified, the entire superframe is treated as a **single RA block** by default.

### 9.7.3.1 Stationary RA Load Control for Traffic

- Applicable when **dynamic load control is not enabled**.
- The RCST uses the control parameter values defined in the **Lower Layer Service Descriptor**.
- These parameters also serve as the **default values** for each RCST.
- If dynamic load control is enabled, parameter values are instead taken from the **Random Access Load Control Descriptor**.

### 9.7.3.2 Dynamic RA Load Control for Traffic

- **Parameters are provided by the NCC** via the `Random Access Load Control Descriptor`.
- Depending on the access mechanism, control applies to:
  - **Slotted ALOHA (SA)**: Control unit is the ALOHA timeslot.
  - **CRDSA**: Control unit is the entire RA block.

#### Core Logic in SA / CRDSA:

- Transmission timing is determined **randomly based on `back_off_time` and `back_off_probability`**.
- If there is unsent data in the buffer:
  - After back-off ends, the RCST decides whether to transmit based on the probability.
  - Transmission opportunity is defined as:
    - **SA**: The ALOHA timeslot.
    - **CRDSA**: The RA block.

#### Constraints:

- Transmission behavior within an RA block is governed by:
  - `max_unique_payload_per_block`
  - `max_consecutive_blocks_accessed`
  - `min_idle_blocks`

# 9.9 Control of RCST Transmission Characteristics

## 9.9.1 EIRP Control
- The RCST can adjust the reference EIRP in 0.5 dB steps as instructed by the NCC.
- Two EIRP control modes are defined:
  - **Constant EIRP**: Maintains the same EIRP across all transmissions.
  - **Constant Power Spectral Density**: Maintains the same spectral density for each transmission.
- The RCST reports **maximum power headroom** (difference between nominal max and min EIRP).
- If instructed to increase power and headroom ≥ 2 dB, RCST shall transmit at max allowed output.

## 9.9.2 Transmission Duration Control
- Burst duration is defined either directly via FCT2/BCT or indirectly via TBTP2.
- **Non-persistent CC**: Duration is governed by TBTP2 timeout.
- **Persistent CC**: Continues until revocation or unmet conditions arise.

## 9.9.3 Symbol Rate Control
- Symbol rate is based on the frame type (FCT2) and BTU duration.
- If frame number changes (in superframe), the initial assignment applies unless redefined.

## 9.9.4 Return Link MODCOD Control
- MODCOD can be specified directly or indirectly via TBTP2.
- When using TBTP2: `tx_type` may be predefined or changed via countdown control message.
- The change applies immediately if countdown = 0.

## 9.9.6 Contention Diversity Transmission Control (optional)
Required capabilities for CRDSA RCST:
1. Must support CR-CRDSA (VR-CRDSA optional).
2. Support single-carrier RA blocks when `noInstances > 2`.
3. Support for `noInstances = {1, 2, 3}`.
4. SA method if `noInstances = 1`, else CRDSA for `>1`.
5. RA block duration ≤ 150 ms.
6. RA block with slots = 64 to 128.
7. Support sub-multiple slot configurations.
8. RA blocks within single superframe, non-crossing.
9. Equal-sized RA blocks per frame.
10. Minimum of one unique payload per RA block.
11. RA blocks without pre-assigned `transmission_type`.
12. Proper signaling with `transmission_type` field unset.

