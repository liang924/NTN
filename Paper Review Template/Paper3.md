## COMPARISON OF 5G NR AND DVB S2X/RCS2 TECHNOLOGIES IN BROAD BAND SATELLITE SYSTEMS

[Reference](https://trepo.tuni.fi/bitstream/handle/10024/150021/HuikkoTuomas.pdf?sequence=2)

### DVB-S2X/RCS2 system architecture
<img width="700" height="500" alt="image" src="https://github.com/user-attachments/assets/f8727266-9a7b-425b-9b4a-e81b4b266c93" />


###  NTN transparent/regenerative payload satellite access architecture
<img width="450" height="300" alt="image" src="https://github.com/user-attachments/assets/34534021-1fb8-4e76-af49-5667c5067a3b" /> <img width="450" height="300" alt="image" src="https://github.com/user-attachments/assets/2a66a83e-d3f4-4b01-aef0-1dea9e9d8b72" />

| Feature                        | NTN Transparent                         | NTN Regenerative                          | DVB-S2X/RCS2                                 |
|-------------------------------|-----------------------------------------|--------------------------------------------|-----------------------------------------------|
| Satellite Data Processing     | Forward-only (no decoding)              | Partial processing onboard                 | Forward-only based on modulation routing    |
| gNB Location                  | Ground-based                            | Onboard the satellite                      | No gNB; follows DVB protocol stack            |
| Uplink/Downlink Interfaces    | NR-Uu (UE ↔ Satellite ↔ gNB)            | NR-Uu + NG interface (UE ↔ gNB on satellite)| DVB-RCS2 (UL) / DVB-S2X (DL)                  |
| Scheduling & Protocol Stack   | Dynamic NR resource scheduling          | Faster onboard NR scheduling               | Fixed frames + CRA (Contention Resolution Algorithm) |
| Target Application Scenarios  | Lower cost, suitable for static users   | High flexibility, ideal for mobility       | Broadcasting, news, static users, latency not critical |

| **Aspect** | **5G NR NTN (Transparent)** | **DVB‑S2X / RCS2 (Transparent)** |
|------------|----------------------------|----------------------------------|
| **Terminal states** | *Idle / Inactive / Connected* | *Connected / Not Connected* |
| **Terminal mobility** | Idle/Inactive reselection ＋ Connected hand‑over | Same‑network beam / satellite / GW hand‑over only |
| **Data‑flow pattern** | DL & UL: continuous **or** bursty, small‑to‑medium blocks | DL: continuous, medium‑to‑large blocks • UL: bursty, small‑to‑medium blocks |
| **Multi‑connectivity** | ATSSS, traffic steering / splitting | *Not supported* |
| **Positioning service** | GNSS (+ possible network‑based) | *Not supported* |
| **Reliability aids** | PHY HARQ ＋ RLC ARQ | ARQ possible via RLE; **not in the standard** |
| **Energy saving** | Idle / Inactive modes, lean carrier, etc. | *None defined in standard* |
| **Network slicing** | End‑to‑end slicing available | *Not supported* |
| **Synchronization** | DL: SSB burst • UL: TA ＋ freq‑offset compensation | DL: pilot blocks in PLFRAME (except beam‑hop) • UL: dedicated sync time‑slots |
| **Security framework** | Full 5G authentication & integrity (RRC / PDCP) | Only high‑level needs listed; no detailed framework |

### DVB-S2 protocol stack with GSE implemented

<img width="879" height="451" alt="image" src="https://github.com/user-attachments/assets/54aff6eb-b3cb-458e-a8f4-d2c2acf03fce" />

1. IP Packet -- The original network data, such as web content or video streams.
2. GSE Encapsulation (GSE Layer) -- Multiple IP packets are encapsulated into a "GSE PDU" format to facilitate further processing.
3. BBFRAME (MAC Layer) -- After GSE processing, a MAC header (BBHeader) is added to create a BBFRAME, which acts as a key intermediate format linking the data layer to the coding layer.
4. Add FEC (Forward Error Correction – FECFRAME) -- To ensure that data can be recovered even in the presence of interference or noise, error correction codes are added:
   - BCHFEC (for error detection)
   - LDPCFEC (for error correction)
5. PLFRAME (Physical Layer Frame) -- A physical layer header (PLHeader) is added to the FECFRAME, forming the final format for transmission. One PLFRAME typically consists of 90 symbols.
6. Physical Transmission -- The data is then transmitted over the satellite. At the receiving end, the process is reversed to reconstruct the original IP packets.

### 5G NR radio protocol stack

<img width="689" height="730" alt="image" src="https://github.com/user-attachments/assets/fe5c6198-911f-481b-807f-112af47a518c" />

### Control Plane (Blue Section)

| Protocol Layer                   | Description                                                                                                                                    |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **NAS (Non-Access Stratum)**     | Manages interaction between UE and Core Network, including registration, authentication, and mobility management (handled by AMF in the core). |
| **RRC (Radio Resource Control)** | Controls connection setup/release, mobility management, encryption configuration, etc.                                                         |
| **PDCP**                         | Performs header compression, encryption, and integrity protection.                                                                             |
| **RLC (Radio Link Control)**     | Handles segmentation and reassembly, as well as error correction via ARQ.                                                                      |
| **MAC (Medium Access Control)**  | Responsible for scheduling, channel allocation, and HARQ operations.                                                                           |
| **PHY (Physical Layer)**         | Handles actual radio transmission including modulation, coding, and antenna control.                                                           |

### User Plane (Green Section)

| Protocol Layer                              | Description                                               |
| ------------------------------------------- | --------------------------------------------------------- |
| **SDAP (Service Data Adaptation Protocol)** | Maps QoS flows from applications to radio bearers.        |
| **PDCP**                                    | Same as in the control plane; used for data transmission. |
| **RLC**                                     | Same as above; handles error correction and segmentation. |
| **MAC**                                     | Same as above.                                            |
| **PHY**                                     | Same as above.                                            |

### Data Flow and Channel Mapping

| Abstraction Layer      | Description                                                                         |
| ---------------------- | ----------------------------------------------------------------------------------- |
| **QoS Flows**          | Define service quality requirements (e.g., voice vs. video).                        |
| **Radio Bearers**      | Data paths between UE and gNB.                                                      |
| **RLC Channels**       | Responsible for segmentation and reassembly of data.                                |
| **Logical Channels**   | Separate different types of data (control vs. user).                                |
| **Transport Channels** | Interface between logical channels and physical layer for actual data transmission. |


###  Parameters Used and Compared in Simulation

| Parameter Name              | Unit | Description |
|----------------------------|------|-------------|
| **Coupling Loss**          | dB   | Represents the path loss between the user terminal (UE) and the satellite or base station. Lower values indicate less signal loss and are therefore better. |
| **SINR (Signal-to-Interference-plus-Noise Ratio)** | dB   | Indicates the ratio of the signal strength to the sum of interference and noise. Higher values mean better signal quality. |
| **User Throughput**        | kbps | The actual data transmission rate per user. Higher throughput is preferable as it reflects better data delivery capacity. |
| **Erroneous Bits per User**| %    | The percentage of incorrect bits received by each user. Lower values are better, indicating more accurate data transmission. |

The DVB‑S2X/RCS2 system simulation uses SNS3, while the 5G NR NTN architecture is simulated using ALIX.
