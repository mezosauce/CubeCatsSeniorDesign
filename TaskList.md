# HABSat-1 Flight Software Task List

**Project:** CubeCats Senior Design – HABSat-1 Flight Software  
**Team Members:** Caden O'Leary, Elmoataz Abdellah, Matthew Goldsberry, Seunghun Lee, Kristen Griessman  

---

## Team Assignment Summary

| Team Member | Subsystem / Domain Focus | Total Tasks Assigned |
| :--- | :--- | :---: |
| **Caden O'Leary** | Power Subsystem, Watchdog Petting, Ground Station Packet Decoding | 6 |
| **Elmoataz Abdellah** | ADCS Subsystem, Comms & Security (ASCON), SITL Environment, Ground Station DB | 8 |
| **Matthew Goldsberry** | Main Computer Queues, Data Processor CI Algorithms, IPC & Latency Validation | 5 |
| **Seunghun Lee** | Reprogrammability, Imager Adapter, Data Storage & Wear-Leveling | 6 |
| **Kristen Griessman** | Ground Station API Schemas, End-to-End Pipeline Validation | 2 |

---

## Master Task Table

| Task ID | Description | Subsystem / Component | Assignee | Status |
| :--- | :--- | :--- | :--- | :---: |
| **Task 001** | Design the static memory buffer allocation scheme for the `pyld_data` and `imgr_data` queues on the Main Computer. | Main Computer | Matthew Goldsberry | Pending |
| **Task 002** | Integrate On-Orbit Flight Software Reprogrammability if Main Computer’s main mission operations ever corrupt. | Main Computer / Bootloader | Seunghun Lee | Pending |
| **Task 003** | Develop the core `active_task` chlorophyll index computation algorithm for the Data Processor module. | Data Processor | Matthew Goldsberry | Pending |
| **Task 004** | Document the API contract and error handling responses for passing `health_status` from the Data Processor to the Main Computer. | Data Processor / Main Computer | Matthew Goldsberry | Pending |
| **Task 005** | Validate the inter-component CAN bus communication latency between the Data Processor and the Main Computer. | Main Computer / Data Processor | Matthew Goldsberry | Pending |
| **Task 006** | Research the I2C mutex locks needed for the ADCS Computer to prevent bus collisions during attitude sensor reads. | ADCS Subsystem | Elmoataz Abdellah | Pending |
| **Task 007** | Specify the exact 12-byte packet structure for sending `adcs_data` (including `pos_x`, `pos_y`, and `pos_z`) from the ADCS Computer to the Main Computer. | ADCS / Main Computer | Elmoataz Abdellah | Pending |
| **Task 008** | Simulate a setting for the development environment to run isolated unit tests on Main Computer’s communication with other subsystem components. | Test / SITL Environment | Elmoataz Abdellah | Pending |
| **Task 009** | Develop the F Prime `Svc::TlmChan` configuration to channelize the `vel_x`, `vel_y`, and `vel_z` attributes within the ADCS Computer. | ADCS Subsystem / F Prime | Elmoataz Abdellah | Pending |
| **Task 010** | Refine the faults handling logic for the ADCS Computer to correctly flag sensor dropouts to the Main Computer without triggering a full system reset. | ADCS Subsystem / FDIR | Elmoataz Abdellah | Pending |
| **Task 011** | Test the command ingestion pipeline routing `goal_pos_y` and `goal_pos_z` targets from the Main Computer to the ADCS Computer. | ADCS / Main Computer | Elmoataz Abdellah | Pending |
| **Task 012** | Investigate the SPI polling rate required for the Main Computer to accurately read the Power Computer's `charge_percentage` and `voltage` attributes. | Power Subsystem / Main Computer | Caden O'Leary | Pending |
| **Task 013** | Design the `time_to_empty` estimation algorithm to run iteratively on the Power Computer. | Power Subsystem | Caden O'Leary | Pending |
| **Task 014** | Document the state transitions and recovery steps for the `faults` attribute within the Power Computer module. | Power Subsystem / FDIR | Caden O'Leary | Pending |
| **Task 015** | Develop the hardware watchdog petting sequence between the Power Computer and the Main Computer's `health_status` buffer. | Power Subsystem / Watchdog | Caden O'Leary | Pending |
| **Task 016** | Validate the power subsystem's fault isolation logic, ensuring the Power Computer properly updates its `time_stamp` during transient voltage spikes. | Power Subsystem / FDIR | Caden O'Leary | Pending |
| **Task 017** | Research the maximum SPI bus throughput for writing `truth_imgr_data` from the Imager Adapter to the Main Computer. | Imager Adapter | Seunghun Lee | Pending |
| **Task 018** | Specify the byte alignment and frame dimensions for the `multi_imgr_data` frames outputted by the Imager Adapter. | Imager Adapter | Seunghun Lee | Pending |
| **Task 019** | Design the circular buffer mechanism to accurately track `packets_processed` inside the Data Storage module. | Data Storage | Seunghun Lee | Pending |
| **Task 020** | Develop the file chunking and `active_mode` flagging logic for the Data Storage component to prepare files for downlink. | Data Storage / Downlink | Seunghun Lee | Pending |
| **Task 021** | Test the `temp` and `health_status` reporting mechanisms of the Data Storage unit under simulated high-I/O read/write loads. | Data Storage | Seunghun Lee | Pending |
| **Task 022** | Obtain the required SQLite ORM libraries and setup the ground station database to receive `pwr_data` telemetry from the Main Computer. | Ground Station | Elmoataz Abdellah | Pending |
| **Task 023** | Specify the JSON schemas for the Ground Station API to exactly match the `adcs_data` and `imgr_data` structures buffered on the Main Computer. | Ground Station | Kristen Griessman | Pending |
| **Task 024** | Ensure security through Encryption, Decryption, and Authentication of packets by the Main Computer to and from the Ground Station. | Comms Security (ASCON-128) | Elmoataz Abdellah | Pending |
| **Task 025** | Refine the Ground Station packet decoding logic to handle fragmented `pyld_data` transmissions stored in the Data Storage module. | Ground Station | Caden O'Leary | Pending |
| **Task 026** | Validate the end-to-end data pipeline from the Main Computer's buffer to the Ground Station's database during a simulated pass execution. | End-to-End Mission Pipeline | Kristen Griessman | Pending |
| **Task 027** | Test the inter-process communication serialization between the Main Computer and Data Processor modules under maximum telemetry load. | Main Computer / Data Processor | Matthew Goldsberry | Pending |

---

## Detailed Task Checklist

### Main Computer & Data Processor Interfaces
- [ ] **Task 001** – Design the static memory buffer allocation scheme for the `pyld_data` and `imgr_data` queues on the Main Computer.  
  *Assignee:* Matthew Goldsberry
- [ ] **Task 003** – Develop the core `active_task` chlorophyll index computation algorithm for the Data Processor module.  
  *Assignee:* Matthew Goldsberry
- [ ] **Task 004** – Document the API contract and error handling responses for passing `health_status` from the Data Processor to the Main Computer.  
  *Assignee:* Matthew Goldsberry
- [ ] **Task 005** – Validate the inter-component CAN bus communication latency between the Data Processor and the Main Computer.  
  *Assignee:* Matthew Goldsberry
- [ ] **Task 027** – Test the inter-process communication serialization between the Main Computer and Data Processor modules under maximum telemetry load.  
  *Assignee:* Matthew Goldsberry

### Flight Software Architecture & Bootloader
- [ ] **Task 002** – Integrate On-Orbit Flight Software Reprogrammability if Main Computer’s main mission operations ever corrupt.  
  *Assignee:* Seunghun Lee

### ADCS Subsystem & Sensor Communication
- [ ] **Task 006** – Research the I2C mutex locks needed for the ADCS Computer to prevent bus collisions during attitude sensor reads.  
  *Assignee:* Elmoataz Abdellah
- [ ] **Task 007** – Specify the exact 12-byte packet structure for sending `adcs_data` (including `pos_x`, `pos_y`, and `pos_z`) from the ADCS Computer to the Main Computer.  
  *Assignee:* Elmoataz Abdellah
- [ ] **Task 008** – Simulate a setting for the development environment to run isolated unit tests on Main Computer’s communication with other subsystem components.  
  *Assignee:* Elmoataz Abdellah
- [ ] **Task 009** – Develop the F Prime `Svc::TlmChan` configuration to channelize the `vel_x`, `vel_y`, and `vel_z` attributes within the ADCS Computer.  
  *Assignee:* Elmoataz Abdellah
- [ ] **Task 010** – Refine the faults handling logic for the ADCS Computer to correctly flag sensor dropouts to the Main Computer without triggering a full system reset.  
  *Assignee:* Elmoataz Abdellah
- [ ] **Task 011** – Test the command ingestion pipeline routing `goal_pos_y` and `goal_pos_z` targets from the Main Computer to the ADCS Computer.  
  *Assignee:* Elmoataz Abdellah

### Power Subsystem & Watchdog Supervision
- [ ] **Task 012** – Investigate the SPI polling rate required for the Main Computer to accurately read the Power Computer's `charge_percentage` and `voltage` attributes.  
  *Assignee:* Caden O'Leary
- [ ] **Task 013** – Design the `time_to_empty` estimation algorithm to run iteratively on the Power Computer.  
  *Assignee:* Caden O'Leary
- [ ] **Task 014** – Document the state transitions and recovery steps for the `faults` attribute within the Power Computer module.  
  *Assignee:* Caden O'Leary
- [ ] **Task 015** – Develop the hardware watchdog petting sequence between the Power Computer and the Main Computer's `health_status` buffer.  
  *Assignee:* Caden O'Leary
- [ ] **Task 016** – Validate the power subsystem's fault isolation logic, ensuring the Power Computer properly updates its `time_stamp` during transient voltage spikes.  
  *Assignee:* Caden O'Leary

### Imager Adapter & Data Storage Management
- [ ] **Task 017** – Research the maximum SPI bus throughput for writing `truth_imgr_data` from the Imager Adapter to the Main Computer.  
  *Assignee:* Seunghun Lee
- [ ] **Task 018** – Specify the byte alignment and frame dimensions for the `multi_imgr_data` frames outputted by the Imager Adapter.  
  *Assignee:* Seunghun Lee
- [ ] **Task 019** – Design the circular buffer mechanism to accurately track `packets_processed` inside the Data Storage module.  
  *Assignee:* Seunghun Lee
- [ ] **Task 020** – Develop the file chunking and `active_mode` flagging logic for the Data Storage component to prepare files for downlink.  
  *Assignee:* Seunghun Lee
- [ ] **Task 021** – Test the `temp` and `health_status` reporting mechanisms of the Data Storage unit under simulated high-I/O read/write loads.  
  *Assignee:* Seunghun Lee

### Ground Station & Communications Security
- [ ] **Task 022** – Obtain the required SQLite ORM libraries and setup the ground station database to receive `pwr_data` telemetry from the Main Computer.  
  *Assignee:* Elmoataz Abdellah
- [ ] **Task 023** – Specify the JSON schemas for the Ground Station API to exactly match the `adcs_data` and `imgr_data` structures buffered on the Main Computer.  
  *Assignee:* Kristen Griessman
- [ ] **Task 024** – Ensure security through Encryption, Decryption, and Authentication of packets by the Main Computer to and from the Ground Station.  
  *Assignee:* Elmoataz Abdellah
- [ ] **Task 025** – Refine the Ground Station packet decoding logic to handle fragmented `pyld_data` transmissions stored in the Data Storage module.  
  *Assignee:* Caden O'Leary

### End-to-End Mission Testing
- [ ] **Task 026** – Validate the end-to-end data pipeline from the Main Computer's buffer to the Ground Station's database during a simulated pass execution.  
  *Assignee:* Kristen Griessman
