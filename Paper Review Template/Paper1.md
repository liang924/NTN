## Simulative Comparison of DVB-S2X/RCS2 and 3GPP 5G NR NTN Technologies in a Geostationary Satellite Scenario
Reference: https://arxiv.org/pdf/2502.13704

### Technical Architecture and Standard Background
**DVB-S2X/RCS2**-- are traditional satellite communication standards primarily designed for satellite broadcasting, news gathering, and point-to-point (PTP) connections. They employ static frame structures and modulation schemes aimed at enhancing spectral efficiency and expanding frequency ranges to support high data rate transmissions. However, they are relatively limited in dynamic resource allocation and multi-user support, being more suited to point-to-point or static configuration scenarios.

**NR NTN** -- builds on the current 5G New Radio standards by adding dynamic resource management for satellite communication, supporting high-frequency bands like Ka-band to improve spectrum efficiency, and incorporating multi-connectivity, multi-user scheduling, and adaptive modulation schemes to handle high mobility, multiple users, and high latency. It also supports flexible device configurations and network optimization, offering more advanced management and transmission features than traditional satellite standards.

### System-level performance and spectrum utilization
**DVB-S2X** demonstrates better performance in the down link (DL), achieving higher spectral efficiency.
**NR** performs better on the up link (UL), especially excelling in dynamic resource allocation and latency advantages.

### Modulation and coding techniques
**DVB-S2X** employs a relatively fixed frame structure and modulation schemes, providing efficient signal transmission capabilities. In contrast, **NR** utilizes dynamic scheduling and more flexible modulation schemes, enhancing performance for low-capability terminals and allowing for dynamic adjustment of resources based on user requirements.

### Resource allocation and scheduling strategies
**DVB-RCS2** adopts a relatively static approach to resource allocation, where scheduling and resource usage are mostly predefined and fixed, offering limited flexibility. In contrast, **NR** follows a real-time dynamic scheduling approach, allowing resource allocation to be adjusted based on current usage conditions. This not only saves bandwidth but also reduces latency and improves system responsiveness.

### Performance Performance (Throughput, Delay, SINR)
**DVB-S2X** performs well in high SINR environments and offers higher spectral efficiency under lower load conditions.
**NR** can reduce latency through dynamic resource allocation, showing significant advantages especially under low load or burst traffic scenarios, but may be more limited in bandwidth utilization.

### Control Plane and Protocol Layers
**DVB-RCS2** has a relatively simple control mechanism, involving fewer complex control signals.
**NR** integrates advanced control plane protocols (such as RRC, RRM), supporting greater flexibility and scalability, making it suitable for diverse mobility and terminal scenarios.

### Simulation Methods and Assumptions
Both are simulated in the GEO Ka-band, based on 3GPP standard parameters, resulting in high consistency in simulation conditions.
However, differences in resource management strategies, channel models, and load scenarios used in the simulations can influence the final performance comparison outcomes.
