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
