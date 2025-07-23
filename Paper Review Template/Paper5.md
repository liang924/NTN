## Physical Layer simulative comparison of DVB-S2X/RCS2 and 3GPP 5G NR-NTN technologies over Geostationary Satellite Scenario 

[Reference](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=10946061)

This study compares the simulated physical layer performance between the Fifth Generation (5G) Non-Terrestrial Network (NR NTN) and Digital Video Broadcasting (DVB) technologies. Specifically, the downlink adopts the Second Generation Satellite Extensions (S2X) standard of DVB, while the uplink uses the Second Generation Return Channel via Satellite (RCS2) standard. The waveform configurations and channel models used in the analysis are designed based on a representative satellite communication system. This reference system assumes a transparent payload satellite with a fixed ground-based user terminal, operating in the 20–30 GHz frequency band (also known as the Ka-band), which corresponds to Frequency Range 2 (FR2-NTN) in 3GPP terminology.

- In this study, DVB-S2X and DVB-RCS2 technologies were simulated using a C++-based Link Level Simulator, while 5G NR PDSCH and PUSCH were evaluated using the 5G NR Link Level Simulator provided by MATLAB's 5G Toolbox.

### Comparison of Simulation Parameters and Waveform Configurations

| Parameter                        | **DVB-S2X**                        | **DVB-RCS2**                        | **NR PDSCH**                              | **NR PUSCH**                              |
|----------------------------------|------------------------------------|-------------------------------------|--------------------------------------------|--------------------------------------------|
| **Carrier Bandwidth**           | 210 MHz                            | 24 MHz                              | 200 MHz                                    | 200 MHz                                    |
| **Number of Resource Blocks**   | —                                  | —                                   | 7 to 132 RBs                               | Fixed at 40 RBs                             |
| **Subcarrier Spacing (SCS)**    | —                                  | —                                   | 120 kHz                                    | 60 kHz                                     |
| **Target Error Rate**           | FER: 1e-3, 1e-5                     | PER: 1e-3, 1e-5                      | BLER: 1e-3, 1e-5                            | BLER: 1e-3, 1e-5                            |
| **Info Bits per Code Block**    | ~15,000 to ~55,000                 | ~1,000 to ~5,000                    | ~1,200 to ~4,600                           | ~400 to ~8,400                             |
| **Min. Simulated Errors**       | 100                                | 100                                 | 10⁴                                        | 10 (due to many configurations)             |
| **MODCOD / MCS**                | Standard MODCOD                    | Standard MODCOD                     | Standard MCS (0–28)                        | Standard MCS                               |
| **Reference Signal Design**     | Pilots (density per Burst ID)      | Pilots + Preamble                   | DMRS (minimal density)<br>PTRS (enabled for high MCS) | Same as PDSCH                              |
| **Cyclic Prefix (CP)**          | Not applicable                     | Not applicable                      | Included (causes efficiency loss)          | Included                                   |
| **HARQ Support**                | Disabled (not simulated)           | Disabled (not simulated)            | Disabled                                   | Disabled                                   |
| **Error Protection Coding**     | LDPC + BCH                         | LDPC + BCH                          | LDPC                                       | LDPC                                       |
| **Other Specific Features**     | 5% roll-off                        | 20% roll-off, burst format, guard time | Cyclic Prefix, PTRS, DMRS, guard bands   | Same as PDSCH                              |
