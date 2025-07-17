# Reference
https://www.etsi.org/deliver/etsi_ts/138300_138399/138300/18.05.00_60/ts_138300v180500p.pdf

## 16.14 Non-Terrestrial Networks 
### 16.14.1 Overview  (p.208-210)
#### Introduction
- Basic Components of an NTN :
  - UE: A mobile phone or IoT device on the ground waiting to receive signals.
  - NTN Payload: Forwarding signals between the UE and the ground.
  - NTN Gateway: Connects the signals received from the satellite to the actual 5G core network (e.g., AMF/UPF).
- Types of Links :
  - Service Link： NTN Payload ↔ UE
  - Feeder Link： NTN Payload ↔ NTN Gateway
- Transparent Mode : The satellite does not decode the signal; it simply “forwards” the signal from the UE or the Gateway.
- NTN Coverage Types :
  | Type                    | Description                                                              | Example                                |
  |-------------------------|--------------------------------------------------------------------------|----------------------------------------|
  | Earth-fixed             | The satellite's beam continuously covers the same area on Earth          | GSO satellite                          |
  | Quasi-Earth-fixed       | The beam covers a fixed area for a period of time, then moves elsewhere  | NGSO with directional beams            |
  | Earth-moving            | The beam footprint continuously moves across the Earth's surface         | NGSO without directional beamforming   |

- Support for Multiple Gateways and Payloads : One Gateway can serve multiple Payloads, and a single Payload can also be served by multiple Gateways.
- GNSS Support Requirements for the UE
#### Why do I need to talk about this section?
It’s here to help me understand the whole NTN setup before we dive into the nitty-gritty.
### 16.14.2 Timing and Synchronization (p.210-212)
#### Introduction
This section explains that NTN, signals experience significant delay and frequency offset due to the long distances involved—such as communication via satellites. Therefore, both timing and frequency need to be compensated and synchronized to ensure the signal arrives accurately and on time.
It defines several key parameters to achieve this, including:

| Name                | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| **Common TA**       | The time the UE must advance its transmission so that the signal arrives at the satellite on time. |
| **K_offset**        | A scheduling offset that accounts for the total delay of the service link plus the Common TA.       |
| **K_mac**           | The approximate round-trip delay between the Reference Point (RP) and the gNB, used at the MAC layer. |
| **Service link RTT**| The round-trip time between the UE and the satellite.                      |
| **Feeder link RTT** | The round-trip time between the satellite and the ground gateway.          |

It also describes:

- How the UE uses GNSS to calculate its distance and location in order to perform timing and frequency pre-compensation.

- That Doppler shift–induced frequency offset is compensated by the UE (on the service link side) and by the network (on the feeder link and transponder side).

- How delay-sensitive functions like HARQ scheduling and random access are adjusted based on these parameters.

### Why is this section important?

Because NTN involves long-distance and high-speed-moving nodes like satellites, conventional timing and frequency strategies used in terrestrial networks won’t work reliably.

This section helps us understand:
- Why NTN needs these special compensation mechanisms;
- How the system keeps the UE and gNB time-aligned;
- How the system avoids signals arriving too early or too late and causing transmission failures.

### HARQ Operation Modes:
- **Downlink (DL):**
  - HARQ feedback can be **enabled or disabled**.
  - If **disabled**, the network can start the next HARQ process **before the previous HARQ RTT completes**, allowing continuous transmission despite long delays.

- **Uplink (UL):**
  - HARQ mode can be configured **per HARQ process**.
  - Supports different HARQ types such as **HARQ Mode A** and **HARQ Mode B**.

### Notes on HARQ Configuration:

- The HARQ setting is determined **by the network**.
- If HARQ feedback is **not enabled**, uplink retransmissions may rely on **SPS (Semi-Persistent Scheduling)**.
- If **HARQ Mode B** is enabled, it may be configured using **Configured Grant (CG)** settings.

### Timing Synchronization During Connection Setup

- In NTN, **broadcast messages (e.g., SIB)** include timing parameters, especially:
  - **Common TA (Timing Advance)**
- The UE must calculate the **round-trip time (RTT)** between itself and the **Reference Point (RP)** to correct its transmission timing.

### GNSS-Aided Positioning and Compensation

- The UE uses **GNSS positioning information** to correct:
  - **Timing offset**
  - **Frequency offset**


### 3. Responsibility for Frequency Offset Compensation

| Item                                  | Who Compensates?      |
|---------------------------------------|------------------------|
| Doppler shift on the service link     | **UE (self-compensated)** |
| Doppler shift on the feeder link      | **Network-compensated**   |
| Frequency error of satellite transponder | **Network-compensated**   |

### Timing Advance Reporting Mechanisms

- The UE can report TA values in the following scenarios:
  - **Random Access Procedure (RA)**
  - **Event-triggered reporting in connected mode**
 
### System Architecture
<img width="1102" height="662" alt="image" src="https://github.com/user-attachments/assets/45979783-ed80-44c7-9c9a-0f12fb35c132" />
