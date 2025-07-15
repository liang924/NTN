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
### System Architecture
<img width="1328" height="417" alt="image" src="https://github.com/user-attachments/assets/adc4f52f-7834-479d-8be8-859481b19eeb" />

### Bent-pipe Satellite Architecture (RF Repeater)

- **Concept:**  
  The satellite acts purely as an RF repeater, without any protocol or signal processing. It simply forwards the signal like an optical fiber.

- **Process Flow:**
  1. Handheld or IoT devices communicate using **NR radio protocols**.
  2. Signals are sent to the **Bent-pipe Satellite** and forwarded to the ground.
  3. A ground-based **gNB (base station)** receives the signal.
  4. The gNB connects to the **5G Core Network**.
  5. Finally, it reaches the **Data Network**.

- **Interfaces:**
  - **NG (N2/N3):** Interface between gNB and 5G Core.
  - **N6:** Interface between the 5G Core and external data networks.

---

### Regenerative Satellite Architecture (Includes gNB/DU)

- **Concept:**  
  The satellite contains partial or full base station functionality (e.g., gNB-DU), allowing it to process some or all protocol logic onboard.

- **Process Flow:**
  1. Handheld or IoT devices use **NR radio protocols** to connect to the satellite.
  2. The **Regenerative Satellite** processes the signals internally.
  3. Processed data is sent to the ground over the **F1 interface** (between gNB-DU and gNB-CU).
  4. The gNB-CU connects to the **5G Core Network**.
  5. Finally, it connects to the **Data Network**.

- **Key Differences:**
  - Uses the **F1 interface**, allowing functional split between satellite and ground unit.
  - Reduces latency and improves efficiency.
  - Better suited for high-load or long-distance communication scenarios.

---

### 📊 Summary Comparison

| Feature                    | Bent-pipe Satellite          | Regenerative Satellite             |
|---------------------------|------------------------------|------------------------------------|
| Satellite Role            | RF repeater only             | Includes gNB/DU functionality      |
| Protocol Processing       | Done on the ground           | Partially or fully onboard         |
| Ground Interface          | NG (N2/N3)                   | F1 interface                       |
| Latency & Efficiency      | Higher latency, less efficient | Lower latency, more efficient     |
| Ideal Use Case            | Simple relay applications    | High load / advanced NTN scenarios|
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
