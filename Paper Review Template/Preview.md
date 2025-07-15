> Reference :
[NTN Structure](https://u.pcloud.link/publink/show?code=kZbSRB5ZcCoOvCSbE5f1t94U8EKD08cm4L7V#/filemanager?folder=27002009791)

### Reason for Choosing
This presentation clearly introduces the system architecture and key challenges of NTN
### Problem Statement
- **High Latency**  
  Round-trip delay (RTT) can reach up to 41.77 ms, which affects real-time communication.

- **Signal Blockage and Attenuation**  
  Risks increase with satellite movement and varying altitude, impacting link stability.

- **UE-to-NTN Synchronization Issues**  
  Difficulty in maintaining timing and frequency synchronization between User Equipment (UE) and satellite.

- **Limited Onboard Processing**  
  Transparent payload architecture centralizes processing on the ground, increasing end-to-end latency.

- **No URLLC Support**  
  Current NTN systems (as per Release 17) do not support Ultra-Reliable Low-Latency Communication.

- **Dependency on GNSS**  
  Assumes UE must support GNSS for synchronization and positioning, which increases design complexity.

- **Complex Beam Management**  
  Beam tracking and multi-connectivity for moving satellites and users create additional challenges.

- **DL/UL Protocol Split**  
  Divided processing across UE, satellite, and NTN gateway increases the complexity of protocol handling.

- **Limited Scope in Release 17**  
  Only transparent payload is supported; regenerative payload and advanced features are not yet standardized.

### Key Performance Indicators
- Link Delay / Latency
- Throughput
- Coverage Area
- Synchronization accuracy
- Power efficiency
