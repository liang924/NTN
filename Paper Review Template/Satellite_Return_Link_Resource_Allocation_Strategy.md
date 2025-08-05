> Return Link for User Traffic
## 1. RCST Behavior: Data Preparation and Request

The **Return Channel Satellite Terminal (RCST)** is the user-end equipment responsible for transmitting user data into the satellite system.

### Operation Flow:

- **Data Sources**: May include voice calls, real-time video, web access, file uploads, etc.

- **Queue Classification**: Data is placed into different priority queues according to service types, typically:
  - **EF (Expedited Forwarding)**: High real-time requirement (e.g., VoIP, video conferencing)
  - **AF (Assured Forwarding)**: Medium priority, tolerates slight delay (e.g., web browsing, streaming)
  - **BF (Best Effort)**: No strict timing requirement (e.g., email, file transfer)

- **Request Generation**: The RCST aggregates service-classified requests into packets and sends them to the **NOC (Network Operations Center)** to request transmission resources (such as bandwidth and timeslots).

---

## 2. NOC Behavior: Scheduling and Resource Allocation

The **Network Operations Center (NOC)** functions as the central control station, responsible for distributing limited satellite resources across multiple RCSTs.

### Core Processing Flow:

#### (1) Priority Sorting

- Requests are sorted based on their service classification (EF, AF, BF):
  - **EF** has the highest priority
  - **BF** is the lowest and processed last

#### (2) RQM-LWDF Scheduling Algorithm

- NOC applies the **Rate and QoS-aware Modified Largest Weighted Delay First (RQM-LWDF)** algorithm, which combines delay weight and resource demand.

- Each packet is scored based on:
  - Packet delay time
  - Required transmission rate
  - Acceptable loss rate

- Higher scores are prioritized in the allocation process.

#### (3) Timeslot Allocation using Reverse Time Slot Tree

- The time-frequency spectrum is structured as a **Reverse Time Slot Tree**.

- Each slot is assigned a descending ID (e.g., starts from 255 downwards).

- **Advantage**: Enables faster identification and dynamic allocation of idle timeslots, suitable for a rapidly changing network environment.

---

## 3. Actual Transmission: RCST Executes Data Transfer

After receiving allocation information from the NOC:

- The RCST maps its packets into the assigned timeslots.

- Then it transmits the data through the satellite return link to the ground gateway or designated destination nodes.
