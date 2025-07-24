## Peculiarities of Traffic and QoS management in 5G NTN networks

- [Reference -- about NTN QoS](https://iris.cnr.it/retrieve/62e41ddc-9593-4291-a613-c9f72ccb8557/prod_486461-doc_201816.pdf?utm_source=chatgpt.com)

- Why I need to read this paper ?
- I can understand specific QoS measures should be added to the NTN & DVB system to adapt to satellite characteristics and operational requirements.

### Traditional QoS in GEO Satellite Systems

| Feature                       | Layer Involved                              | Description                                                                  |
| --------------------------------- | ------------------------------------------- | ---------------------------------------------------------------------------- |
| **Bandwidth Management**          | MAC Layer / Radio Resource Management (RRM) | Controls bandwidth allocation per user, handled mainly by MAC and scheduler. |
| **Priority Setting**              | MAC Layer                                   | MAC schedules packets based on priority.                                     |
| **Data Transmission Reliability** | RLC Layer / PHY Layer                       | Ensures accuracy via RLC retransmissions and physical-layer FEC.             |
| **Connection Stability**          | RRC Layer / Network Layer                   | Maintains connections through RRC connection control and handover.           |


### Enhanced/New QoS Features in Modern NTN (e.g., LEO)

| Feature                             | Layer Involved                                | Description                                                                  |
| --------------------------------------- | --------------------------------------------- | ---------------------------------------------------------------------------- |
| **Predictive Traffic Management**       | Application Layer / Management Plane          | Uses AI/ML models for demand prediction and bandwidth pre-allocation.        |
| **Dynamic QoS Adjustment**              | MAC / RRC / Network Layer                     | Adjusts QoS dynamically according to satellite movement and link changes.    |
| **Traffic Prioritization**              | MAC Layer / Network Layer                     | Assigns higher priority to emergency services and control signals.           |
| **Flexible SLA Management**             | Management Layer / Application Layer          | Dynamically adjusts SLA metrics such as latency, jitter, and packet loss.    |
| **Multi-layer QoS Management**          | Cross-layer (MAC, RLC, RRC, Management Layer) | Coordinates QoS across UE, satellite, and gateway layers.                    |
| **Delay/Error-Tolerant Mechanisms**     | RLC Layer / Transport Layer                   | Incorporates error correction and timeout mechanisms for high-latency links. |
| **Intelligent QoS Control (AI-Driven)** | Control Plane / Application Layer             | Applies AI for predictive control and proactive QoS optimization.            |

## A QoS Architecture for DVB-RCS Next Generation Satellite Networks
- [Reference -- about DVB QoS](https://citeseerx.ist.psu.edu/document?doi=f90e3ba2ecdee78b1210a829ecadecfc2043c870)
### QoS Mechanisms in DVB Systems

| **Mechanism / Function**            | **Layer**             | **Description** |
|------------------------------------|------------------------|-----------------|
| **DAMA (Demand Assignment Multiple Access)** | MAC Layer              | Dynamically allocates bandwidth based on real-time traffic demand. Fixed assignment for real-time services; on-demand for non-real-time services. |
| **DiffServ Architecture**          | IP Layer               | Differentiated services like EF (Expedited Forwarding), AF (Assured Forwarding), and BE (Best Effort) are used to manage varying latency and bandwidth requirements. |
| **User Resource Quota Control**    | User / Management Layer| Allocates resource shares per user to ensure fairness and avoid bandwidth monopolization. |
| **Admission Control**             | Cross-layer (MAC/IP)   | Ensures sufficient resources are available before admitting a new flow, preventing congestion. |
| **Policing / Shaping**            | MAC Layer              | Enforces traffic rate limits and shapes traffic to stay within predefined service agreements. |
| **Traffic Differentiation**       | MAC/IP Layer           | Assigns priority based on traffic type, enabling QoS differentiation. |
| **Cross-layer QoS Architecture**  | Cross-layer (MAC & IP) | Integrates queue management at MAC layer and traffic classification at IP layer for improved QoS coordination. |
| **QoS Proxy + QoS Server**        | Application / Control Layer | Enables dynamic QoS adjustment during application runtime, even for non-QoS-aware apps, enhancing multimedia performance. |


### Comparison of QoS Mechanisms in DVB vs. NTN Systems

| **Aspect**                        | **DVB Systems**                                                                 | **NTN Systems (e.g., 3GPP-based LEO)**                                              |
|----------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| **QoS Architecture Layers**      | Focused on MAC and IP layers using mechanisms like DAMA and DiffServ.           | Cross-layer design including MAC, RLC, PDCP, and Application layers.               |
| **Resource Allocation Method**   | Uses DAMA for on-demand allocation; fixed allocation for real-time flows.       | AI/ML-based predictive allocation and dynamic real-time adjustment.                |
| **Scheduling & Prioritization**  | Utilizes MAC queues and DiffServ classes (EF, AF, BE) for priority handling.    | Combines MAC and network-layer prioritization, e.g., emergency/control traffic.     |
| **Application Layer Involvement**| QoS Proxy/Server enables dynamic control, but mainly manual or centralized.     | Intelligent QoS control using AI for predictive and proactive optimization.         |
| **Flexible SLA Management**      | Achieved via class-based DiffServ treatment.                                    | Dynamically adjusts SLAs (e.g., latency, jitter, packet loss) in real-time.         |
| **Delay/Error Tolerance**        | Relies on RLC/PHY layer error correction (e.g., FEC); limited delay handling.   | Applies timeout adaptation and error control suited for satellite delay.            |
| **Cross-Layer Coordination**     | Basic MAC/IP cross-layer integration for scheduling and traffic classification. | Full cross-layer QoS control across MAC, RRC, RLC, and Application layers.         |
| **User Resource Quota**          | Ensures fairness by allocating per-user quotas.                                 | Focuses on predictive usage patterns and traffic prioritization.                    |
