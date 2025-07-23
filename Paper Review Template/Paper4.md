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
