##  5G New Radio in Nonlinear Satellite Downlink: A Physical Layer Comparison with DVB-S2X

[Reference](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9604976)

### Introduction
- Satellite communications face waveform design challenges due to power constraints and the use of nonlinear high-power amplifiers (HPAs) operating near saturation.
- Currently, 5G NR only supports CP-OFDM for downlink, but its high peak-to-average power ratio (PAPR) is not suitable for satellite transmission, leading to nonlinear distortion.
- In contrast, single-carrier waveforms such as DFT-s-OFDM are more suitable for satellite links, and are already adopted for uplink but not yet standardized for downlink.
- Simulation results indicate that using DFT-s-OFDM for downlink can improve performance in terms of EVM (Error Vector Magnitude), OOBE (Out-of-Band Emission), and BLER (Block Error Rate).

DFT-s-OFDM was traditionally used only for uplink transmission in earlier 3GPP releases. However, starting from Release 17, it was included as an optional waveform for uplink. In Release 18, discussions and proposals have emerged to consider it for downlink transmission as well, especially in satellite communication scenarios. Nevertheless, it has not yet been fully standardized as a downlink waveform.

Although DVB-S2X was not directly simulated with its native waveform in this experiment, the HPA (High Power Amplifier) model used, which is commonly associated with DVB-S2X evaluations, highlights the robustness of DVB-S2X’s design in tolerating nonlinearity. In contrast, the default CP-OFDM waveform in 5G NR shows performance limitations under the same conditions.
To match or surpass DVB-S2X in NTN or satellite communication scenarios, 5G NR must adopt more suitable waveforms, such as:
- Downlink support for DFT-s-OFDM
- Spectrally-shaped enhanced versions of DFT-s-OFDM

Simulation results show that under nonlinear amplifier conditions, traditional DVB designs are more robust in waveform selection. However, once waveform optimizations are applied, 5G NR demonstrates greater flexibility and potential, especially in aspects like low latency and dynamic resource scheduling.

### physical layer link-level simulation
This experiment is a **physical layer link-level simulation** focused on comparing **DVB-S2X** and **5G NR for NTN** under **nonlinear High Power Amplifier (HPA)** conditions.

| Item | Description |
|------|-------------|
| **Simulation Type** | Link-level simulation focusing on signal transmission between UE and satellite/gNB. It does **not** include core network behaviors. |
| **Scope** | Evaluates the impact of **nonlinear amplifiers (e.g., HPA)** on the following parameters:<br> - Error Vector Magnitude (EVM)<br> - Out-of-Band Emission (OOBE)<br> - Block Error Rate (BLER)<br> - Peak-to-Average Power Ratio (PAPR) |
| **Simulation Conditions** | Uses HPA models defined by DVB-S2X and Ka-band parameters. Compares 5G NR standard waveforms (CP-OFDM, DFT-s-OFDM). |
| **Comparison Targets** | - **DVB-S2X** uses single-carrier modulation with lower PAPR<br> - **5G NR** uses multi-carrier OFDM which requires PAPR suppression techniques |
| **Objective** | To evaluate whether 5G NR NTN should adopt lower-PAPR waveforms (e.g., DFT-s-OFDM) for downlink, similar to DVB-S2X. |
