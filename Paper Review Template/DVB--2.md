> Reference : https://dvb.org/wp-content/uploads/2020/07/A155-2r3_Interactive-Satellite-System-DVB-RCS2_Part-2-Lower-Layers_Draft-EN-301-545-2-v141_July-2023.pdf

# 4.5 Protocol Stack Model
### Protocol Stack Structure
<img width="408" height="323" alt="image" src="https://github.com/user-attachments/assets/8de929a8-176d-4dbc-af26-f541e9dc4b6e" />

1. **Physical Layer**
   - Responsible for defining transmission parameters and constructing transmission frames.
   - Includes: synchronization, modulation, channel coding, frequency range setting, filtering, and power control.

2. **Data Link Layer**
   - Handles Logical Link Control (LLC) and Medium Access Control (MAC) protocols.

3. **Intermediate Layers**
   - Protocols that connect the application layer to the lower layers.
   - Not specified in detail in this document; defined in ETSI TS 101 545-3.

4. **Application Layer**
   - Provides interactive application functionalities, such as home shopping applications or script interpreters.
# 4.6 The Lower Layers 
## 4.6.0 Introduction
### 1. Payload Type Classification (for Return Link)

The RCST's Layer 1 payloads for the return link are categorized into four content types:

1. **Logon** – Used exclusively for Layer 2 Signalling (L2S)
2. **Control** – Used exclusively for L2S
3. **Traffic** – Intended for higher layer traffic
4. **Traffic/Control (Mixed)** – May carry both higher layer traffic and L2S, at RCST's discretion

> **Note:**  
> **L2S (Layer 2 Signalling)** handles management and control messages such as logon and network coordination.

### 2. Forward Link Payload Classification

For the forward link, two types of Layer 1 payload formats are defined:

- One format for **L2S only**
- One format for **Higher Layer Traffic only**

### 3. Diagram Structure – Figure 4-2 Explanation
<img width="650" height="246" alt="image" src="https://github.com/user-attachments/assets/c5a9d523-ffd8-45b5-86bd-2c99ea12cac5" />

The figure segments the lower layers at RCST into:

- **L2S Region** (on the left):
  - Logon
  - FLL2S (Forward Link L2 Signalling)
  - Control

- **Higher Layer Traffic Region** (on the right):
  - RLTraffic (Return Link Traffic)
  - FL HL Traffic (Forward Link Higher Layer Traffic)

These correspond to distinct logical channels and processing domains.

### 4. Virtual Interface Architecture

- The RCST may implement multiple **Layer 2 Virtual Interfaces**, each handling different types of traffic.
- Each interface can correspond to different services or Satellite Virtual Networks (SVNs).
- This separation allows higher layer traffic to be processed independently per domain.

### 5. Transmission Resource Assignment

- RCST can be assigned **satellite transmission resources** for Layer 1 allocation channels, which are used for:
  - **Random Access**
  - **Dedicated Access**
  - **Burst Time Plan**

- Any Layer 2 Virtual Interface may map its service aggregates to the Layer-1 allocation channels as needed.

> This allows flexible and efficient utilization of satellite resources for various service demands.

## 4.6.1 Lower Layer Services
<img width="735" height="722" alt="image" src="https://github.com/user-attachments/assets/0f1e943c-334b-4e5e-a00f-59977dbe4be6" />

This diagram explains **how user traffic and control signaling are mapped and allocated in the return link lower layers of a satellite system**. It illustrates the full data processing flow from upper-layer services down to the physical transmission layer.

### 1. Overview of the Diagram

- The data flow starts from the **Service Aggregate**, which contains various types of higher-layer application data (SDUs).
- It is processed through **Lower Layer Stream** and **Lower Layer Service**, which determine how resources are assigned.
- Depending on the traffic type (user data or signaling), different allocation channels are used.
- Ultimately, all data is aggregated into a **Connectivity Channel** and transmitted via a **Transmission Channel**.

---

### 2. Block-by-Block Explanation (Top to Bottom)

**Service Aggregate**
- Represents a set of SDUs from various applications (e.g., VoIP, streaming).
- These are the data units to be transmitted through the return link.

**Lower Layer Stream**
- Organizes and sequences data units from the Service Aggregate.
- This stream may include mixed traffic types.
  
**Lower Layer Service**
- Determines how the data should be mapped to resource channels.
- Uses:
  - **Request Class Signalling** for dynamic requests
  - Mapping to **Dedicated** or **Random Access Allocation Channels**

**Request Class Signalling**
- The RCST uses this block to signal the NCC (Network Control Center) about its resource needs.
- Different request classes are used (e.g., best-effort, guaranteed).
- Two transmission methods:
  - **Dedicated Access for Signalling**
  - **Random Access for Signalling**

---

### 3. Core Resource Allocation Channels
**Dedicated Access Allocation Channel for User Traffic**
- RCST is assigned specific timeslots or frequencies.
- Suitable for continuous data like video or VPN.
- Allocation controlled by **TBTP (Terminal Burst Time Plan)**.

**Random Access Allocation Channel for User Traffic**
- Shared by multiple RCSTs.
- Used for bursty or short traffic like logon, small data uploads.
- Includes contention mechanisms like backoff.
- Managed by **FCT2 (Frame Composition Table v2)** or **TBTP2**.

### 4. Signaling Allocation Channels

**Dedicated Access for Signalling**
- Allocated exclusively for one RCST to communicate control messages.

**Random Access for Signalling**
- Shared by multiple RCSTs to send short signaling bursts.
- Useful during network entry or registration.


### 5. Aggregation and Transmission
**Connectivity Channel**
- Collects and consolidates data from all allocation channels.
- One or more receivers may be connected to a connectivity channel.
- One channel is implicitly reserved for the NCC and gateway.

**Transmission Channel**
- The final physical transmission path.
- Transmits data via satellite using predefined modulation, power, and timing.

### 4.6.2 Lower Layer Interfaces 
**Forward Link Interfaces at an RCST**

<img width="616" height="497" alt="image" src="https://github.com/user-attachments/assets/552b74bc-0e64-4778-ab9f-792151ebfdf9" />

**1. Bottom Layer: Forward Link Layer 1 Interface**
  - **Physical Layer**: Responsible for receiving, demodulating, and decoding satellite signals; this is the entry point for data into the RCST.
  - The received data is distributed to different Layer 2 interfaces depending on its purpose.

**2. Middle Layer: Three Types of Layer 2 Interfaces**

  - **Layer 2 Interface for SNO (Satellite Network Operator)**
     - Handles messages from the SNO.
     - Enables connectivity with the IPv4 M&C (Management and Control) interface.

  - **Layer 2 Interface for SVNO (Satellite Virtual Network Operator)**
     - Handles user data associated with SVNO.
     - Can be connected to the IPv4 M&C interface or higher-layer applications.

  - **L2S Interface (Lower Layer Signalling)**
     - Special interface for processing L2S signals (e.g., control commands from the NCC).
     - Initializes independently without requiring upper-layer support.

**3. Top Layer: Upper-Layer Application Interfaces**

  - **Generic Higher Layer Interface**
    - A general-purpose interface for user applications, such as internet access or multimedia services.

  - **IPv4 M&C Interface**
    - Uses IPv4 protocol for management and control communication.
    - Two instances are shown: one for the SNO and one for the SVNO.

### Overall Workflow Summary

1. The satellite transmits forward link signals to the RCST.

2. After the physical layer (Layer 1) receives the signal, it distributes the data based on content to:
   - The Layer 2 interface for SNO (e.g., operator control messages),
   - The Layer 2 interface for SVNO (e.g., user service data),
   - The L2S interface (e.g., system synchronization and logon control).

3. The processed data is then passed upward to the IPv4 M&C interface or higher-layer application interface.

**Return Link Interfaces at an RCST**


This diagram illustrates the architecture and flow of return link data at a Return Channel Satellite Terminal (RCST). It shows how user data and signaling messages are passed from higher-layer applications through various Layer 2 interfaces down to the physical transmission layer.

---

**1. Top Layer: Application & Control Sources**

  - **Generic Higher Layer Interface**
    - Provides general-purpose application data (e.g., user apps, web browsing, VoIP).
  
  - **IPv4 M&C Interface** ×2
    - Uses IPv4 protocol for management and control communications.
    - One connects to the **SVNO (Satellite Virtual Network Operator)**.
    - One connects to the **SNO (Satellite Network Operator)**.
    - Handles system-level signaling such as initialization, logon, and configuration.

**2. Middle Layer: Layer 2 Processing Interfaces**

  - **Layer 2 Interface for SVNO**
    - Receives data from both the generic application interface and IPv4 M&C.
    - Handles higher-layer user data or control messages related to the SVNO.
    - Forwards this data to an appropriate allocation channel below.

  - **Layer 2 Interface for SNO**
    - Handles network management and system control data from the SNO.
    - Also maps this data into allocation channels for transmission.

  - **L2S Interface (Layer 2 Signaling)**
    - Dedicated to low-layer signaling tasks (e.g., logon control, resource requests).
    - Sends signaling data into the **L2S Channels** for further transmission.

**3. Bottom Layer: Allocation & Transmission Channels**

  - **Allocation Channels (×3)**
    - Receive traffic from the Layer 2 interfaces.
    - Can be configured as:
      - **Dedicated Access Channels** for specific terminals.
      - **Random Access Channels** shared by multiple RCSTs.
    - All data is routed toward the Layer 1 physical interface.

  - **L2S Channels**
    - Carry signaling and control data generated from the L2S interface.
    - Used for logon, synchronization, and access requests.

  - **Return Link Layer 1 Interface**
    - Final point where all traffic from Allocation Channels and L2S Channels converge.
    - Responsible for physical modulation and uplink transmission to the satellite.
