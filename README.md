# NTN data collation

---

## 📘 Standards and Specifications

### 1. [ETSI EN 302 307-2 V1.3.1 (DVB-S2X)](https://www.etsi.org/deliver/etsi_en/302300_302399/30230702/01.03.01_20/en_30230702v010301a.pdf)
- Defines the physical layer and framing structure (BBFRAME, FECFRAME, PLFRAME, SuperFrame) for satellite downlink communication.
- Supports adaptive coding and modulation (ACM) and beam hopping in advanced systems.
https://www.etsi.org/deliver/etsi_en/302300_302399/30230701/01.04.01_60/en_30230701v010401p.pdf
### 2. [ETSI EN 301 545-2 V1.4.1 (DVB-RCS2)](https://www.etsi.org/deliver/etsi_en/301500_301599/30154502/01.04.01_60/en_30154502v010401p.pdf)
- Describes the return channel (uplink) structure based on MF-TDMA.
- Defines terminal burst scheduling, TBTP tables, and NCC control protocols.
https://www.etsi.org/deliver/etsi_en/301500_301599/30154502/01.01.01_60/en_30154502v010101p.pdf
---

## 📄 Implementation Guidelines

### 1. [ETSI TR 102 376-2 (DVB-S2X Implementation Guidelines)](https://dvb.org/wp-content/uploads/2020/02/A171-2_DVB-S2X_Implementation-Guidelines_Draft-TR-102-376-2_v121_Apr-2020.pdf)
- Provides recommendations for implementing DVB-S2X features such as SuperFrame, beam hopping, and ACM-based adaptation.

### 2. [ETSI TR 101 545-4 (DVB-RCS2 Lower Layer Guidelines)](https://www.etsi.org/deliver/etsi_tr/101500_101599/10154504/01.01.01_60/tr_10154504v010101p.pdf)
- Covers Layer 2 Signaling (L2S), terminal synchronization, TBTP, SCT/FCT signaling, and power control.

---

## 🧪 Simulation Tools

### 1. [ns-3 NTN Module (sns3-satellite)](https://github.com/sns3/sns3-satellite)
- Simulates LEO/GEO satellite links, delay characteristics, and traffic models in ns-3.
- Includes scheduling and multiple-beam capabilities.

### 2. [Hypatia](https://github.com/snkas/hypatia)
- Focused on LEO satellite routing and path scheduling with QoS differentiation.
- Supports ground-satellite-ground communication patterns.

### 3. [Xeoverse](https://arxiv.org/abs/2406.11366)
- A real-time simulation platform for large-scale LEO satellite constellations.
- Includes beam hopping, traffic-aware scheduling, and inter-satellite coordination.

---

## 🧩 Open Source Modules

### 1. [OpenNMS](https://www.opennms.org/)
- Enterprise-grade open-source network monitoring and management platform.
- Can be integrated with satellite gateways for health/performance tracking.

---

### Install guide (from Joanna)
- https://sixth-handball-b2f.notion.site/Installation-of-xeoverse-22ccecc6b77180a4ae31d3c9714a4bf8
- https://sixth-handball-b2f.notion.site/Installation-of-Hypatia-229cecc6b771809ab9ffd8e0e95efd2a
