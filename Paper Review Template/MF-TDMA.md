# MF-TDMA
> [Reference](https://www.etsi.org/deliver/etsi_en/301500_301599/30154502/01.04.00_20/en_30154502v010400a.pdf?utm_source=chatgpt.com) ch7.5

## Superframe 
<img width="448" height="317" alt="image" src="https://github.com/user-attachments/assets/ccaedd38-f4e7-482b-9f8b-61562de10b59" />

**1. Structure**
- The **MF-TDMA return link** is organized in a **time × frequency grid**, called a **superframe**.  
- **Superframe**: Largest unit for resource allocation  
  - Consists of multiple **frames**  
  - Each frame consists of multiple **timeslots**  
- **Diagram interpretation**:  
  - **Vertical axis** → Different carrier frequencies  
  - **Horizontal axis** → Time progression  
- **Example (Carrier ↔ Frame Number)**:  
  - Carrier 0: F_nb 0, 2  
  - Carrier 1: F_nb 6, 8  
  - Carrier 2: F_nb 12, 14, etc.  

**2. Timing Constraints**
- **Superframe Duration** (ETSI specification): **25 ms ~ 750 ms**  
- Duration is determined by:  
    Superframe Duration = N_frames × Frame Duration

- Common practical configurations:  
  - **16–32 frames per superframe**  
  - **Frame Duration**: 20–40 ms  
  - Example:  
    - 16 × 40 ms ≈ 640 ms  
    - 32 × 20 ms ≈ 640 ms  

**3. Control and Allocation**
- **NCC (Network Control Center)** assigns superframe structure to each **RCST** (user terminal).  
- **SF-CTRL** (Superframe Control) message includes:  
  - Timeslot allocation  
  - Modulation and coding scheme  
  - User ID mapping  
- **Frame Number (F_nb)** is used to identify the order of frames in a superframe.  
  - May use cyclic or even/odd numbering, not necessarily consecutive (1, 2, 3, 4).  

**4. Design Considerations**
- **Short frame duration** → Higher control overhead, lower efficiency  
- **Long frame duration** → Lower allocation flexibility, higher delay  
- Engineering trade-off between **number of frames (N)** and **frame duration**  






---
## Superframe Sequence
<img width="509" height="233" alt="image" src="https://github.com/user-attachments/assets/beb0abe4-d2f4-4397-b521-bdaf8cc28579" />

- A **Superframe Sequence (SFS)** is a portion of return link bandwidth composed of a series of consecutive superframes of the same type, typically allocated to different RCSTs.
- The diagram shows two sequences: SFS1 (superframes 14 to 16) and SFS2 (superframes 236 to 239).
- Superframes in the same sequence are **continuous in time** and **can be in separate frequency bands**.
- Each superframe has a unique **superframe_count** (like a timestamp or index), with a maximum of 2^16.
- RCSTs schedule their transmissions based on the assigned SFS and are capable of storing the list of assigned logon timeslots.

---
## Frame
<img width="646" height="290" alt="image" src="https://github.com/user-attachments/assets/6ac09d56-a989-41dd-9354-30c95ab6f878" />

- Each frame is composed of one or more **BTUs (Bandwidth-Time Units)** forming a time-frequency slot grid.
- Horizontal axis: time; vertical axis: frequency. Each cell in the grid is a type-G BTU.
- A single frame may span across multiple carriers, forming a **multi-carrier frame**.

In the **MF-TDMA structure of DVB-RCS2**, the number of **timeslots** that a **frame** can be divided into mainly depends on:

1. **Frame Duration**
   - Commonly set to **20 ms ~ 40 ms** (can be shorter or longer in some systems).

2. **Timeslot Duration**
   - Determined by system requirements and the modulation & coding scheme (ModCod).
   - In ETSI standards, the minimum can be less than 1 ms (but too short increases control overhead).

3. **Carrier Bandwidth & Number of Carriers**
   - Each frame can contain multiple frequency channels, and each frequency channel is further divided into timeslots.

🔹 **Example of a common practical configuration**

- Frame Duration = **40 ms**  
- Timeslot Duration = **1 ms**  
- → Each frame can have up to **40 timeslots per frequency**.

If the system has **multiple carriers**, each carrier has its own timeslot set. For example:  
- 4 carriers × 40 timeslots per carrier = **160 timeslots per frame**.


<img width="967" height="431" alt="image" src="https://github.com/user-attachments/assets/d7d1e23b-a646-41af-b7bb-1c17ec1e3de4" />

- This figure illustrates a frame composed of different types of BTUs:
  - `TRF1`: 2 BTUs  
  - `TRF2`: 6 BTUs  
  - `CB`: Control burst  
  - `LB`: Logon burst  
  - `G`: General-purpose BTU (usage defined by TBTP2 messages)
- When a frame is received by the RCST, it decodes each BTU based on its assigned type defined in the TBTP2.
- The type of BTU indicates the purpose of the block (data, control, logon, etc.).

---
## Timeslot
<img width="966" height="254" alt="image" src="https://github.com/user-attachments/assets/756524a3-a3c7-42a6-b681-f347624bf99c" />

- Each **timeslot** typically contains one burst, which may occupy the entire timeslot duration, with **guard time** reserved to prevent burst interference.
- The figure shows a TRF2-type burst occupying a timeslot built from 6 BTUs.
- **burst_start_offset** defines how the burst is aligned with the start of the timeslot.
- Burst design must consider the appropriate burst type (TRF1, TRF2, CB, LB, etc.), each requiring different timeslot sizes.

## Guard Time
### What is the purpose?
Used to separate consecutive bursts on the same carrier to avoid interference caused by power transients and transmission timing errors.

### How is guard time determined?
It is determined by multiple factors:
- The size of the burst
- The size of the timeslot
- The burst start offset

### Who allocates it?
The NCC (Network Control Center) allocates and controls guard time via:
- **FCT2**: Frame Configuration Table 2  
- **BCT**: Broadcast Configuration Table  
- **TBTP2**: Traffic Burst Time Plan 2

<img width="1172" height="352" alt="image" src="https://github.com/user-attachments/assets/e4b01b5f-37ab-48ba-a81a-9f3d6456eb34" />

---

## The Dynamic MF-TDMA Transmission Channel
###  Core Concepts:
- Each RCST (user terminal) can dynamically use different:
  - Modulation schemes
  - Coding rates
  - Frequencies
  - Symbol rates
  - Start times and durations
###  Where are these parameters defined?
- BTP (Burst Time Plan)
- FCT2(Frame Configuration Table 2)
- BCT(Broadcast Configuration Table)
###  Dynamic transmission behavior:
- A single RCST may use different timeslots with varying bandwidths and durations.
- As shown in Figure 7-31, the RCST may jump between frequencies over time (indicated by the arrows).
  <img width="338" height="316" alt="image" src="https://github.com/user-attachments/assets/2989305d-bd7b-4344-982d-a23de60fcc4d" />
