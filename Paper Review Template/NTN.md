
### System Architecture
<img width="1102" height="662" alt="image" src="https://github.com/user-attachments/assets/45979783-ed80-44c7-9c9a-0f12fb35c132" />

### NTN Payload
<img width="1060" height="858" alt="image" src="https://github.com/user-attachments/assets/82c75fa4-95c5-45b6-bbd5-14ca230bae4f" />

- Transparent Mode
  - Satellites only shift the signal frequency (up-conversion or down-conversion) and do not process any data content.
  - The data processing is handled by the ground Gateway and the gNB (base station).
  - The gNB can connect to multiple satellites at the same time, since each satellite acts like a "reflector" that simply forwards the signal down to Earth.
  - The system performance (e.g., coverage, throughput, and latency) depends on where the gateways are deployed.
  - There are no ISLs (Inter-Satellite Links), meaning satellites cannot communicate with each other. All signals must be sent back to the ground before being forwarded again.
- Regentive Mode
  - Satellites are equipped with processors that can receive and decode signals on their own instead of just forwarding them.
  - SDR and SDN technologies bring flexibility to the satellite system, allowing dynamic functionality adjustments as needed.
  - The connection between the user and the satellite uses 5G NR technology.
  - The feeder link between the satellite and the ground gateway can use any transport protocol.
  - With ISLs, satellites can forward data directly to each other, reducing latency in long-distance communication.
- CU-DU (Centralized Unit - Distributed Unite) Separated Structure
  - gNB is divided into CU (at GW) and DU (on satellites)
  - CU hosts RRC (Radio Resource Control), SDAP (Service Data Application Protocol), PDCP (Packet Data Convergence Protocol)
  - DU hosts RLC (Radio Link Control), MAC (Medium Access Control), PHY (Physical Layers)
  - F1 link (connects CU to DU) is implemented using the SRI (Satellite Radio Interface)
  - Each CU connects to multiple DU and perform coordination according to the CU-DU separation options
### Use Message sequence charts (MSCs) to show the steps required by an NTN UE to establish a connection with the gNB

<img width="813" height="645" alt="image" src="https://github.com/user-attachments/assets/14bc6721-6af8-4e87-87f1-f0d164ca4605" />

#### Power on procedure
- SSB / PBCH (gNB → UE)
  - The gNB broadcasts synchronization signals and basic system information. The UE receives and synchronizes.
- SIB1 (gNB → UE)
  - System Information Block 1 is transmitted, containing cell configuration and random access parameters.
- [Decode Cell ID / Beam ID] (UE local processing)
  - The UE decodes the Synchronization Signal Block (SSB) to obtain Cell ID and Beam ID.
- [Estimate K_offset & TA] (UE local processing)
  - The UE estimates the timing advance (TA) and frequency offset (K_offset) based on the SSB.

#### Random Access and RRC Connection
- RACH Preamble (Msg1) (UE → gNB)
  -The UE sends a preamble to initiate the Random Access Procedure.
- Random Access Response (Msg2) (gNB → UE)
  - The gNB responds with timing advance, temporary identifier, and other config.
- [Apply TA correction] (UE local processing)
  - The UE applies the timing correction based on the RAR.
- RRC Connection Request (Msg3) (UE → gNB)
  - The UE requests to establish an RRC connection.
- RRC Connection Setup (Msg4) (gNB → UE)
  - The gNB grants the connection and sends setup configurations.
- RRC Reconfiguration (gNB → UE) / Complete (UE → gNB)
  - Additional RRC configurations are exchanged and confirmed.
#### Registration Procedure
- NAS Registration (UE → AMF)
  - The UE sends a NAS registration request to the AMF (via gNB).
- Authentication Request / Response (AMF ↔ UE)
  - The AMF performs authentication with the UE.
- Security Mode Command / Complete (AMF ↔ UE)
  - Security settings like encryption and integrity protection are negotiated.
- Registration Accept / Complete (AMF ↔ UE)
  - The AMF accepts the registration, and the UE confirms.
#### Data Transfer Procedure
- PDU Session Establishment Request (UE → SMF)
  - The UE requests to establish a data session (PDU session).
- PDU Session Accept (SMF → UE)
  - The SMF accepts and sets up the data session.
- Start Data Transfer (UE ↔ UPF)
  - Data transfer begins between the UE and the UPF (User Plane Function).
### NTN O&M Parameters
- https://forge.3gpp.org/rep/sa5/MnS/-/tree/Rel-18/yang-models
### NTN RRM
- QoS
  | Item              | Terrestrial Network           | Non-Terrestrial Network (NTN)                          |
  |-------------------|-------------------------------|--------------------------------------------------------|
  | **Latency**        | < 20 ms                       | **Up to 500–600 ms (GEO)**                            |
  | **Bandwidth Stability** | Stable                        | **Highly variable** (due to weather, satellite motion) |
  | **Coverage**       | Local area                    | **Very large area**, requires beam hopping             |
  | **Backhaul Link**  | Stable, low latency           | **Variable, high latency**, possibly uses relay        |

- Beam hopping algorithm
  | Classification Method        | Type                            | Description                                                                                         |
  |-----------------------------|----------------------------------|-----------------------------------------------------------------------------------------------------|
  | Based on Time Scheduling  | **Static Beam Hopping**          | The beam hopping sequence and timing are pre-defined and do not adapt to real-time demands.  Simple design but lacks flexibility in resource allocation. |
  |                             | **Dynamic Beam Hopping**         | The hopping schedule is dynamically adjusted based on real-time user demand, traffic, and QoS needs.High efficiency but more complex to implement. |
  | Based on Hopping Entity   | **Single-Satellite Beam Hopping** | A single satellite transmits beams to different regions at different times.                        |
  |                             | **Multi-Satellite Cooperative Beam Hopping** | Multiple satellites coordinate beam hopping patterns to support wider coverage and diverse demand. |
  | Based on Coverage Scope   | **Full-Coverage Beam Hopping**   | All areas are served by beams within a scheduled time frame. The hopping pattern covers the entire service region. |
  |                             | **Selective Beam Hopping**       | Beams are focused only on high-demand areas, ignoring low-traffic or uninhabited regions to optimize resource use. |

- inter-satellite routing
  - Definition:Inter-satellite routing refers to the technique of transmitting data from one satellite to another via direct wireless links between satellites, known as Inter-Satellite Links (ISLs).
  - Purpose:To reduce reliance on ground gateways and enhance the efficiency and coverage of data transmission.
  - Operation Process:
    1. Wireless links (ISLs) are established between satellites;
    2. Data packets are forwarded from one satellite to another;
    3. The destination satellite eventually delivers the data to a ground station or user.
  - Advantages:
    1. Reduces transmission latency, especially in remote areas (e.g., oceans or polar regions);
    2. Improves coverage and network reliability;
    3. Increases network resilience, allowing communication to continue even if some ground stations fail.
