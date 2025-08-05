# Return Link for User Traffic
> https://www.researchgate.net/publication/375013711_Satellite_Return_Link_Resource_Allocation_Strategy_Based_on_DVB-RCS2
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

#  Forward Link User Traffic
> https://dvb.org/wp-content/uploads/2019/12/a155-2_dvb-rcs2_lower_layers_satellite_v1_3_1_update.pdf?utm_source=chatgpt.com  (9.1.2& 9.1.3)
## 1. **Link Structure and Stream Configuration**

The NOC manages and configures the forward link for user traffic through the following mechanisms:

- **TDM Stream Segmentation**: Based on service requirements, the NOC divides the forward link into:
  - **Data-Only Streams**
  - **Signalling-Only Streams**
  - **Mixed Streams**

- **Forward Link Descriptors**:
  - **Satellite Forward Link Descriptor**
  - **Satellite Forward Link v2 Descriptor**  
  These descriptors define the purpose of each stream, resource ratio, and the target user group (defined by Population ID).

---

## 2. **Resource Scheduling and Spectrum Usage**

- The NOC determines the configuration of each stream in terms of:
  - Bandwidth (e.g., MHz allocated per stream)
  - Modulation and Coding Scheme (MODCOD)
  - Allocation timing (based on Superframe intervals)

- Resources are flexibly allocated according to user groups (Population ID):
  - For example, areas requiring high-speed data (e.g., video streaming) will be allocated higher bandwidth and better MODCOD in their corresponding stream.

---

## 3. **Control Information via RMT and TIM-U**

The NOC uses the following signaling mechanisms to guide RCSTs in handling forward link reception:

- **RMT (Receiver Map Table)**: Informs the RCST of which streams and Population IDs it is allowed to receive.

- **TIM-U (Terminal Information Message – User)**: Sends configuration data to each RCST including channel assignments, MODCOD settings, and timing parameters.

# Forward Link for Signalling (L2S)
> https://www.etsi.org/deliver/etsi_en/301700_301799/301790/01.04.01_40/en_301790v010401o.pdf?utm_source=chatgpt.com
## 1. Broadcast Slot and Frequency Resource Allocation

- **NOC configures the TDM carrier**:
  - The Forward Link for Signalling uses **TDM (Time Division Multiplexing)** mode.
  - The NOC assigns **specific frequencies, timing structures, and modulation parameters** to transmit L2S data.

- **L2S message segments (e.g., TIM-B / TIM-U) are inserted into the TDM carrier**:
  - TIM (Terminal Information Messages) contain control descriptors such as:
    - `Logon Contention Descriptor`
    - `Lower Layer Service Descriptor`
    - `FLD (Forward Link Descriptor)`

---

## 2. Broadcasting Targeted Control Messages by Population ID

- The NOC may classify RCSTs into different groups using **Population ID**:
  - Then selectively broadcasts messages related to:
    - Logon
    - Frequency synchronization
    - Resource allocation
  - This allows differentiated management based on the network segment or service type the RCST belongs to.

---

## 3. Managing Scheduling and Broadcast Cycles

- The NOC determines **when**, **how often**, and **at what interval** to:
  - Repeatedly send logon signalling
  - Broadcast updates like bandwidth reallocation or return link parameters (e.g., MODCOD, timeslot count)

---

## 4. Controlling and Adapting Content Format

- Based on the **protocol version** and **link conditions** supported by the RCST:
  - The NOC adjusts the format and length of the signalling data broadcast.
  - This includes:
    - Standard **TIM-B** format
    - **Extended signalling content** (e.g., multilingual support, regional frequency info)

# Return Link for Signalling
> https://dvb.org/wp-content/uploads/2019/12/a155-2_dvb-rcs2_lower_layers_satellite_v1_3_1_update.pdf?utm_source=chatgpt.com  (ch8 & 9)
## 1. Resource Types: Random Access vs. Dedicated Access

###  Random Access (RA)
- Used by RCSTs that are not yet logged in or are in the initial stages of connection.
- NOC broadcasts allowable RA parameters via **Logon Contention Descriptor** in **TIM-B messages**, including:
  - Number of available timeslots
  - Max retry delay (`max_time_before_retry`)
  - Retransmission mechanisms
- Supports **Slotted ALOHA** and **CRDSA** multiple access schemes.

###  Dedicated Access
- Assigned to authenticated and logged-in RCSTs.
- Controlled through the **Terminal Burst Time Plan (TBTP)**.
- Allocates exclusive timeslots to specific RCSTs to ensure reliable control message delivery.

---

## 2. Random Access Control Parameters

The NOC dynamically adjusts the access control to maintain system performance:

- `max_time_before_retry`: Defines the random wait interval after a failed attempt.
- `default_control_randomization_interval`: Sets the minimum randomized gap between RA attempts.
- Constraints such as:
  - `max_unique_payload_per_block`: Max allowed transmissions per RA block.
  - `max_consecutive_blocks_accessed`: Max number of consecutive used RA blocks.

---

## 3. Timeslot Configuration and Broadcasting

- In each **Superframe**, the NOC defines specific timeslots for signalling.
- This configuration is broadcast via:
  - **SCT** (Superframe Composition Table)
  - **FCT2** (Frame Composition Table v2)
  - **TBTP2** (Terminal Burst Time Plan v2)

---

## 4. Additional Stability and Recovery Controls

- **Dynamic Load Control**:
  - NOC adjusts access parameters based on network load to avoid collisions.
- **Failure Recovery Mechanism**:
  - During large-scale outages, NOC may set a recovery flag in TIM-B to trigger specific reconnect procedures at the RCST.

