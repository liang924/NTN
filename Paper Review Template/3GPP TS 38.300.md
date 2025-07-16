## Reference
https://www.etsi.org/deliver/etsi_ts/138300_138399/138300/18.05.00_60/ts_138300v180500p.pdf
### Reason for choosing
This document is a 5G specification specifically designed for non-terrestrial networks such as satellites and high-altitude platforms, addressing challenges like latency, Doppler shift, and connection stability.

### Problem Statement
- Long delays (signals travel a long distance)
- Shifting frequencies (due to high-speed movement and Doppler effect)
- Changing coverage areas (because satellites keep moving, so devices must switch connections)
- Devices may have trouble syncing time or getting accurate location

This spec tries to tweak the current 5G system so it can handle those situations.It doesn’t need a full rebuild—just some smart adjustments to make it all work.

### Key Performance Indicators (KPIs)
- RACH success rate and access delay
- Handover success rate
- UE positioning accuracy
- Frequency offset compensation capability
- Coverage stability

### System Architecture
<img width="361" height="461" alt="ts drawio" src="https://github.com/user-attachments/assets/a54d4017-af6b-4a22-afe1-f8deec2cef0e" />
