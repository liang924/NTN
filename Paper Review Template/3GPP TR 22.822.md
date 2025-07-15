> Reference :
[NTN Structure](https://u.pcloud.link/publink/show?code=kZbSRB5ZcCoOvCSbE5f1t94U8EKD08cm4L7V#/filemanager?folder=27002009791)

### Reason for Choosing
This presentation clearly introduces the system architecture and key challenges of NTN
### Problem Statement
- Latency
- Blockage
- Frequency Shift
- Synchronization
- UE Power Efficiency

### Key Performance Indicators
- Link Delay / Latency
- Throughput
- Coverage Area
- Synchronization accuracy
- Power efficiency
### System Architecture
<img width="638" height="411" alt="466271620-6a352504-5cd1-44a8-90eb-0576d4c57d3d-fotor-20250715105014" src="https://github.com/user-attachments/assets/6dedcabb-df08-4ab5-9b1f-1bf7aae8df74" />


Starting from the bottom left, we have the Terminal, which refers to the user equipment (UE or VSAT). It connects to the Satellite above through the Service Link.
However, several challenges arise in this communication:
- **Latency**: Especially with Low Earth Orbit (LEO) satellites at 1200 km altitude, the round-trip time (RTT) can reach up to 41.77 ms, which is a significant issue for low-latency 5G applications.
- **Doppler Shift**: Due to the high speed of satellite movement, the signal frequency may drift, leading to synchronization issues.
- **Blockage**: Buildings, mountains, or other obstacles can block the signal, causing temporary disconnection for users.

Looking at the satellite, there are two types of Payload designs:
- **Transparent Payload**: The satellite only handles RF processing and frequency conversion. All higher-layer protocol processing is done by the ground-based NTN Gateway and gNB. This design is simple but results in higher latency and more load on the ground infrastructure.
- **Regenerative Payload**: Part of the base station functionality, such as baseband layer conversion (BLC), is implemented directly on the satellite. This reduces latency and offloads processing from the ground.

Moving rightward, the Gateway connects the satellite to the Data Network and is responsible for synchronization with the ground. Accurate timing and coordination are crucial here.
Above, the Inter-Satellite Link enables satellites to communicate directly with each other. This eliminates the need to always send data back to the ground first and allows for more flexible network routing.
Finally, the dashed lines represent Multi-connectivity and Beam Hopping, which are strategies used to maint
