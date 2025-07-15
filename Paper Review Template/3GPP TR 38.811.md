## Study on New Radio (NR) to support non-terrestrial networks 
> Reference : [Study on New Radio (NR) to support non-terrestrial networks](https://portal.3gpp.org/desktopmodules/Specifications/SpecificationDetails.aspx?specificationId=3234)
### Reason for choosing
It is a technical report proposed by 3GPP that specifically explores how 5G NR can be extended to NTN. It is one of the fundamental documents for understanding the development of satellite-based 5G.
### Problem Statement
- Traditional terrestrial networks cannot cover remote areas and air/sea transportation platforms.
- On high-speed moving platforms, 5G communication struggles to maintain stable and reliable connections.
- During disasters, terrestrial infrastructure is prone to failure, and there is a lack of alternative connectivity solutions.
- NTN systems experience high latency and Doppler effects, which challenge low-latency and high-reliability requirements.
- Existing terminals and protocols are not designed for NTN characteristics and require adjustments and optimization.

### Key Performance Indicators (KPIs)
- Propagation Delay
- Doppler Shift
- Channel Bandwidth
- UE Transmit Power
- UE Mobility

### Verification Method
#### System-level Methodology
- **Purpose**: Simulate overall network performance such as throughput, coverage, and user behavior at scale.
- **Simulation Type**: Drop-based simulation (users are randomly distributed).
- **Parameters Considered**:
  - Large-scale parameters (e.g., path loss, shadow fading)
  - Small-scale parameters (e.g., delay spread, angle spread)

#### Link-level Methodology
- **Purpose**: Simulate physical layer performance such as BER and SNR over a single radio link.
- **Simulation Type**: Uses CDL (Clustered Delay Line) or TDL (Tapped Delay Line) models.
- **Key Points**:
  - For each environment and elevation angle, one channel instance is selected from the system-level model.
  - Focuses on accurate physical layer behavior (multipath structure, delay profiles, angles, etc.)
- **Precision**: Higher accuracy than system-level; suitable for PHY algorithm evaluation.
