##  Performance and Verification Techniques for Airborne Satcom Terminals Based on 5G NR NTN and DVB-S2X/RCS2

[Reference](https://oss.wanfangdata.com.cn/www/%E5%9F%BA%E4%BA%8E5G%20NR%20NTN%E4%B8%8EDVB-S2XRCS2%E7%9A%84%E6%9C%BA%E8%BD%BD%E5%8D%AB%E6%98%9F%E9%80%9A%E4%BF%A1%E7%BB%88%E7%AB%AF%E6%80%A7%E8%83%BD%E5%8F%8A%E9%AA%8C%E8%AF%81%E6%8A%80%E6%9C%AF.ashx?isread=true&type=perio&resourceId=txjs202504005&transaction=%7B%22id%22%3Anull%2C%22transferOutAccountsStatus%22%3Anull%2C%22transaction%22%3A%7B%22id%22%3A%221947188371801546752%22%2C%22status%22%3A1%2C%22createDateTime%22%3Anull%2C%22payDateTime%22%3A1753080859505%2C%22authToken%22%3A%22TGT-2746816-PahkhMFYrSj0BMnnLci9m3csQzJIS4t7REmVtiJ4V2PnWlG1wQ-auth-iploginservice-79c46fff65-4cdpr%22%2C%22user%22%3A%7B%22accountType%22%3A%22Group%22%2C%22key%22%3A%22g_twkjdx%22%7D%2C%22transferIn%22%3A%7B%22accountType%22%3A%22Income%22%2C%22key%22%3A%22PeriodicalFulltext%22%7D%2C%22transferOut%22%3A%7B%22GTimeLimit.g_twkjdx%22%3A3.0%7D%2C%22turnover%22%3A3.0%2C%22orderTurnover%22%3A3.0%2C%22productDetail%22%3A%22perio_txjs202504005%22%2C%22productTitle%22%3Anull%2C%22userIP%22%3A%22140.118.162.83%22%2C%22organName%22%3Anull%2C%22memo%22%3Anull%2C%22orderUser%22%3A%22g_twkjdx%22%2C%22orderChannel%22%3A%22pc%22%2C%22payTag%22%3A%22%22%2C%22webTransactionRequest%22%3Anull%2C%22signature%22%3A%22i3t0ApQTqceKUqXrpf7Oltym8segRRniioSopfeY%2FSuW9hXR4%2FKhYNvCfEyeoXrLMA9zIlYTtKsY%5CnAXkdeUz9FDxAAqaFE2aFI%2BTW6KwaTBXPgIHGeHe9o1y%2Fjx9IMGzmqxeMHMWingIpI3L1PY2h4ceM%5CnKSOuvJKmFLSrgKufYiI%3D%22%7D%2C%22isCache%22%3Afalse%7D)

### System Function Comparison

| Feature                    | 5G NR NTN                                                                                  | DVB-S2X/RCS2                                                                                         |
|----------------------------|--------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| **Terminal State**         | Supports multiple states: idle, inactive, connected (via RRC); more efficient resource control | Only "connected" or "not connected"; no finer-grained states                                         |
| **Mobility Support**       | Seamless cell reselection and handover, including idle/inactive/connected mode transitions | Supports beam/gateway switch within same network; does not support inter-network handover            |
| **Data Transmission**      | Supports both continuous and burst transmissions of small to medium packets                | DL: continuous large blocks; UL: bursty small packets                                                 |
| **Multi-Connectivity**     | 5GC supports multi-connectivity (e.g., traffic steering, split); evolving for NTN          | Not supported                                                                                         |
| **Positioning Service**    | Supports GNSS and network-assisted positioning                                             | Not supported                                                                                         |
| **Reliability Mechanism**  | HARQ in PHY layer, ARQ in RLC layer                                                        | ARQ possible via vendor-specific methods; not standardized in DVB-S2X or RCS2                         |
| **Power Efficiency**       | Achieved via idle/inactive modes, lean carrier, and power-saving mechanisms                | Not defined                                                                                           |
| **Network Slicing**        | Fully supports end-to-end slicing for differentiated services                              | Not supported                                                                                         |
| **Synchronization** | DL: via periodic Synchronization Signal Blocks (SSB); UL: via Timing Advance (TA), controlled by UE or network | DL: continuous pilot-based sync signals (unless beam hopping); UL: uses dedicated control slots for sync  |
| **Security**         | Well-defined security architecture, supports authentication and PDCP-based encryption/integrity | Some high-level security needs identified, but no standardized framework defined                          |


### Operating Conditions Comparison

| **Aspect**                          | **5G NR NTN**                                                                                                                   | **DVB-S2X/RCS2**                                                                                                |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **Supported Platforms**          | Supports LEO, MEO, GEO, and HAPS (High Altitude Platform Stations).                                                             | Currently supports GEO only; NGSO (e.g., LEO) support is not yet standardized but may be implemented in future. |
| **Supported Frequency Bands**    | FR1 (410–7125 MHz), FR2-1 (24.25–52.6 GHz), FR2-2 (52.6–71 GHz).                                                                | Uses traditional satellite bands: C-band (4–8 GHz), Ku-band (12–18 GHz), Ka-band (26–40 GHz).                   |
| **Uplink Bandwidth Limitations** | Uplink bandwidth in NR can go up to 400 MHz or even more via carrier aggregation (e.g., FR2-2 supports up to 2000 MHz).         | Uplink channel bandwidths are limited (e.g., minimum 64 kHz, maximum 167 MHz depending on waveform and symbol). |
| **Network Slicing / QoS**        | Supports end-to-end QoS via QoS Flows, 5QI (5G QoS Identifiers), and network slicing.                                           | Not supported.                                                                                                  |


### Conclusion

DVB-S2X/RCS2: Best suited for fixed broadband satellite communication, with stable and mature technology.

5G NR NTN: Aimed at mobile communications and innovative applications, though its satellite performance still requires optimization.
