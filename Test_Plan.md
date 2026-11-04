# Test Plan

## What is being tested this cycle, by requirement ID and component, and what is not

### In-Scope Verification and Validation Targets

This test cycle focuses on verifying and validating the core Command and Data Handling (CDH), autonomous execution, and fault-recovery capabilities of the HABSat-1 On-Board Computer (OBC) prototype flight software. The specific design components and requirement IDs undergoing testing include:

* **Main Computer (D0 / D1 / D2 Stack):**
  * **Command Security & Validation:** Decryption, cryptographic tag verification, sequence replay protection, NVM key isolation, critical command two-step safeguards, and syntax/bounds/mode validation of non-amateur telecommands (L1-PRJ-021, L2-SYS-049, L2-MIS-079, L3-OBC-129, L3-OBC-130, L3-OBC-131, L4-OBC-185, L4-OBC-186, L4-OBC-187, L4-OBC-188, L4-OBC-189, L4-OBC-190, L4-OBC-191, L4-OBC-192, L4-OBC-193, CON-06, CON-08, CON-09).
  * **Telemetry, Command ACK & Time-Tagged Scheduling:** Health telemetry collection, periodic 49-second beacon generation, execution confirmation/rejection reporting, non-volatile command outcome logging, and scheduled command queueing/dispatch (L2-SYS-043, L2-SYS-060, L2-MIS-082, L2-MIS-083, L3-OBC-132, L3-OBC-135, L3-OBC-136, L3-OBC-140, L3-OBC-149, L3-OBC-168, L4-OBC-194, L4-OBC-195, L4-OBC-196, L4-OBC-197, L4-OBC-198, L4-OBC-202, L4-OBC-203, L4-OBC-204, L4-OBC-205, L4-OBC-231, L4-OBC-232, L4-OBC-233).
  * **Autonomous Pass Execution Sequencer & State Machine:** Autonomous 10-mode flight state transitions, TLE/target forwarding to ADCS, 16-slot pass schedule queueing and conflict resolution, pre-pass constraint checking (SoC >= 20%, GSD <= 90 m), target lock gating, synchronized imager triggering, and ground pass preemption (L0-PRJ-001, L0-PRJ-002, L1-SCI-009, L1-PRJ-020, L2-SYS-038, L2-MIS-074, L2-MIS-081, L3-OBC-137, L3-OBC-151, L3-OBC-152, L3-OBC-153, L3-OBC-154, L4-OBC-209, L4-OBC-234, L4-OBC-235, L4-OBC-236, L4-OBC-237, L4-OBC-238, L4-OBC-239, L4-OBC-240, L4-OBC-241, L4-OBC-242, L4-OBC-243).
  * **Fault Recovery, Watchdog Supervision & Reconfiguration:** System reset handling, software exception recovery, preemptive task priority scheduling, zero dynamic heap memory allocation enforcement, RAM utilization protection, hardware watchdog petting, golden-image boot recovery, faulted bus node isolation, on-orbit parameter/software updates, and umbilical diagnostics (L0-PRJ-004, L1-SCI-012, L1-MIS-015, L2-SYS-026, L2-SYS-027, L2-SYS-044, L2-SYS-048, L2-SYS-053, L2-SYS-059, L3-OBC-156, L3-OBC-159, L3-OBC-160, L3-OBC-161, L3-OBC-162, L3-OBC-163, L3-OBC-164, L3-OBC-165, L3-OBC-166, L3-OBC-172, L3-OBC-175, L3-OBC-176, L4-OBC-247, L4-OBC-248, L4-OBC-249, L4-OBC-250, L4-OBC-251, L4-OBC-252, L4-OBC-254, L4-OBC-255, L4-OBC-256, L4-OBC-263, L4-OBC-264, L4-OBC-265, L4-OBC-266, L4-OBC-267, L4-OBC-268, CON-01, CON-02, CON-03, CON-05, CON-10).
  * **Deployment & Safety Inhibit Timers:** Mandatory post-dispenser deployment wait (30 min) and transmission wait (45 min) monotonic timers, burn-wire current limiting (<= 2.5 A), microswitch debouncing (100 ms), and autonomous 1-week startup sequencing (L2-MIS-071, L2-MIS-072, L2-MIS-073, L3-OBC-169, L3-OBC-170, L4-OBC-213, L4-OBC-214, L4-OBC-215, L4-OBC-216, L4-OBC-217).

* **Data Processor (D0 / D1 / D2 Stack):**
  * **Science Data Processing:** Ingestion of 4-band raw multispectral frames (620 nm, 650 nm, 680 nm, 708 nm), onboard Chlorophyll Index (CI) calculation, arithmetic divide-by-zero protection, telemetry reporting, power gating, and execution timeout enforcement (L1-SCI-008, L3-OBC-150, L3-OBC-167, L4-OBC-244, L4-OBC-246, L4-OBC-261, L4-OBC-262).
  * **Inter-Component Data Offloading:** High-speed S-Band downlink data path routing (ADR-002), lossless image compression, frame segmentation, flow control, and raw frame transfer CRC verification and retry logic (L2-SYS-061, L2-MIS-075, L3-OBC-133, L4-OBC-199, L4-OBC-200, L4-OBC-223, L4-OBC-245).

* **Data Storage (D0 / D1 / D2 Stack):**
  * **Memory Buffer & Lifecycle Management:** SPI NAND Flash and SPI MRAM storage allocation, 30-second state persistence, mutex-serialized concurrent access, bad-block remapping, wear-leveling reporting, CRC file integrity verification, high utilization telemetry warnings (85%), FIFO log rollover (99%), and ground-verified handshake image purging (L2-SYS-042, L2-MIS-084, L3-OBC-144, L3-OBC-145, L3-OBC-146, L3-OBC-147, L3-OBC-148, L4-OBC-212, L4-OBC-224, L4-OBC-225, L4-OBC-226, L4-OBC-227, L4-OBC-228, L4-OBC-229, L4-OBC-230, L4-OBC-253).

* **Communication Subsystem Interfaces (UHF Telemetry/Command Radio & S-Band Downlink Radio):**
  * **Link Operations:** Dual-radio operational redundancy (ADR-004), primary S-Band image streaming (L3-OBC-133), backup UHF preview/metadata routing (L3-OBC-134, L4-OBC-201), uplink reception priority over half-duplex channels (L4-OBC-206), amateur radio digipeater 64-kb ring buffering and duty-cycle rate limiting (L1-PRJ-018, L2-MIS-080, L3-OBC-155, L4-OBC-207, L4-OBC-208, CON-04), and ground-commanded RF inhibit/enable controls (L1-PRJ-019, L2-MIS-078, L3-OBC-171, CON-07).

* **ADCS & Power Subsystem Hardware Interfaces:**
  * **ADCS/GPS Interface:** ECEF position and LVLH attitude estimation georeference tagging (L1-SCI-010, L2-SYS-040, L2-SYS-041, L3-OBC-173, L4-OBC-260), onboard auxiliary sensor readout (L4-OBC-259), primary GPS 1PPS and fallback ground time synchronization (L3-OBC-141, L3-OBC-142, L3-OBC-143, L4-OBC-218, L4-OBC-219), and I2C/CAN bus error handling.
  * **Power (EPS) Interface:** Periodic vitals monitoring and threshold evaluation (L3-OBC-138, L4-OBC-220, L4-OBC-221), mode-based power rail commanding and graceful shutdown (L4-OBC-210, L4-OBC-211), standby/peak power bounds (L3-OBC-157, L3-OBC-158), Maximum Power Point Tracking (MPPT) control loop feedback (L2-SYS-046), thermal setpoints and charging cutoffs (L2-SYS-050, L3-OBC-174, L4-OBC-257), and EPS backup beacon failover / watchdog heartbeat (ADR-004, L4-OBC-258).

### Out-of-Scope Items & Exclusions

The following components, features, and third-party systems are explicitly excluded from testing during this cycle, along with the engineering rationale for their exclusion:

1. **Commercial Off-The-Shelf (COTS) Board Hardware Fabrication:** Physical silicon fabrication, trace routing, and chip-level semiconductor physics of the COTS EnduroSat OBC Type I motherboard, STM32 microcontroller silicon, and SPI MRAM chips are excluded. Verification relies on manufacturer-provided datasheets, flight heritage certifications, and acceptance testing.
2. **Uncalibrated Secondary Payload Hardware:** Physical testing of secondary partner payload instruments is deferred ('Won't' scope for current prototype cycle) pending final partner selection. Software interfaces maintain isolated stub handlers (`SecPayload_CacheManager`, `SecPayload_ScriptParser`).
3. **Real-Time Voice Amateur Radio Transceiver Operations:** High-bandwidth real-time voice repeating across amateur bands is deferred ('Could' scope). Testing is strictly restricted to digital AX.25 UI-frame packet digipeating (L2-MIS-080).

---

## Verification and Validation Strategy

### Strategy Narrative

The HABSat-1 software verification and validation (V&V) strategy ensures both technical compliance with system specifications and fulfillment of stakeholder operational needs:

* **Verification (Building the Product Right against the Spec):** Rigorous Software-in-the-Loop (SITL) unit and integration testing, complemented by Hardware-in-the-Loop (HITL) bench testing, verifies every flight software component against the formal Assignment 9 L3/L4 technical requirements. Executed autonomously by the HABSat-1 development team (Caden O'Leary, Elmoataz Abdellah, Matthew Goldsberry, Seunghun Lee, Kristen Griessman) using CI/CD automated test harnesses, static analysis (Cppcheck), and logic analyzers.
* **Validation (Building the Right Product for Stakeholders):** Full end-to-end mission profile simulations validate that system capabilities satisfy primary and secondary stakeholder expectations. Validated against operational user stories:
  * **Satellite Operators (US-01):** Ground station command ingestion, ASCON-128 cryptographic authentication, and command execution ACK reporting (L2-MIS-082).
  * **Environmental Data Researchers (US-02):** Multispectral GSD <= 90m per pixel (L1-SCI-009) with ECEF/LVLH georeference metadata headers (L1-SCI-010) and onboard Chlorophyll Index data products (L4-OBC-244).
  * **Future CubeCats Members (US-03):** Complete software architecture documentation, Doxygen API contracts, and clear code modularity.
  * **Amateur Radio Community (US-04):** Regulatory compliance with FCC 45-minute RF transmission inhibits (L2-MIS-072) and public beacon broadcasting (L2-SYS-060). Validated in coordination with Faculty Advisor Dr. Hawkins and UC CubeCats leadership.

### Test-Pyramid Architecture

| Test Layer | Approximate Test Count | Primary Coverage & Verification Focus |
| :--- | :--- | :--- |
| **Layer 1: Unit Tests** | ~150 tests | Isolated function-level validation of C/C++ drivers, ASCON-AEAD128 crypto primitives, telemetry packet encoding/decoding, Chlorophyll Index math algorithms, and bounds checkers. Target: 90%+ code coverage. |
| **Layer 2: Integration Tests** | ~45 tests | Inter-component communication across CAN bus, SPI, and UART lines; FreeRTOS queue IPC handling; F' `Svc::CmdDispatcher` and `Svc::TlmChan` message passing; and device driver bus recovery. |
| **Layer 3: System Tests** | ~20 tests | End-to-end autonomous 10-mode mission sequencer state machine; emergency Safe Mode transition; hardware watchdog reset triggers; multi-pass image buffer purging; and power rail isolation. |
| **Layer 4: Acceptance / Pilot Demos** | ~10 tests | Complete ground-to-space operational pass scenarios; simulated 45-minute post-launch deployment sequences; and HITL ground station telemetry pipeline integration. |

### Hardware, Sensor, and Science Algorithm Test Variables & Metrics

* **Embedded Hardware & Bus Signals:**
  * **Supply Voltage Rails:** Monitored target tolerance +/- 0.1 V across 3.3V and 5.0V buses during high-I/O peak processing.
  * **SPI Bus Throughput:** Sustained data transfer rate >= 10 Mbps between Imager Adapter and NAND Storage.
  * **CAN Bus Latency:** Inter-component message transmission latency < 15 ms under 80% bus utilization.
* **Sensor Interfaces (ADCS / GPS / Thermal):**
  * **GPS Time Synchronization Jitter:** Spacecraft epoch clock alignment jitter < 1.0 ms relative to GPS 1PPS pulse (L4-OBC-218).
  * **Thermal Operating Range:** Verification of software thermal cutoff actuation across -40°C to +60°C operating bounds across 10 thermal-vacuum trial runs (L2-SYS-050).
* **Science Algorithm (Data Processor Chlorophyll Index):**
  * **Processing Latency:** Computation time per 4-band multispectral image set < 2.5 seconds.
  * **Numerical Accuracy:** Floating-point Chlorophyll Index output precision within Δ < 0.001 of numpy reference values across 50 synthetic/drone calibration image sets (L4-OBC-244, L4-OBC-246).

---

## Table of Measurable Success Criteria

| Metric | Target Threshold | Measurement Method | Requirement ID |
| :--- | :--- | :--- | :--- |
| **Command Decryption & Validation Latency** | < 50 ms per telecommand frame | Hardware timer benchmark from RF frame ingress to dispatcher routing in SITL test harness | L3-OBC-129, L3-OBC-130, L4-OBC-185, L4-OBC-186 |
| **Ground Sampling Distance (GSD)** | <= 90 meters/pixel at nadir | Geometric optical model calculation using ADCS position state vector | L1-SCI-009, L2-MIS-074, L4-OBC-237 |
| **Post-Launch RF Inhibit Duration** | >= 45.0 minutes continuous hold | Monotonic tick counter log verification following simulated dispenser switch opening | L1-PRJ-019, L2-MIS-072, L4-OBC-216 |
| **Image Downlink Throughput** | >= 7 image sets downlinked per 24 hrs | Automated benchmark stream test over 2.4 Mbps S-Band link setup | L2-SYS-061, L3-OBC-133 |
| **Asynchronous Fault Preemption Latency** | < 100 ms response execution time | Logic analyzer trace from CAN fault alert assertion to power rail isolation handler | L3-OBC-139, L4-OBC-222 |
| **Dynamic Memory Allocation (Flight)** | 0 bytes post-initialization | Static code analysis (cppcheck) and FreeRTOS heap tracking assertions | L4-OBC-248 |
| **Hardware Watchdog Reset Timeout** | 500 ms +/- 50 ms window | Oscilloscope pulse capture on watchdog GPIO pin upon intentional execution freeze | L2-SYS-048, L4-OBC-250 |
| **Chlorophyll Index Math Accuracy** | Floating-point delta Δ < 0.001 | Automated PyTest assertion comparing Data Processor output against reference numpy model | L1-SCI-008, L4-OBC-244, L4-OBC-246 |
| **NAND Storage Warning Trigger** | Assert flag at 85% +/- 1% capacity | Simulated flash memory write fill test tracking telemetry log flags | L4-OBC-229 |
| **Real-Time Clock Drift Rate** | <= 20 ppm uncalibrated drift | Frequency counter timing analysis over 48-hour continuous run | L4-OBC-217 |

---

## Test Cases

The test cases below follow the mandatory five-column template (ID | Description | Steps | Expected Result | Status) and cover all 182 test cases defined in the Week 9 Technical Specification Document Traceability Matrix (TC-001 through TC-310). Every major ("shall" / Must) requirement is verified by at least three test cases within its functional requirement group, and every group includes happy path, edge case, and failure condition scenarios.

### Group 1: Telecommand Security, Decryption, and Authentication (L2-MIS-079, L3-OBC-129–130, L4-OBC-185–189, CON-06, CON-08)

| ID | Description | Steps | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC-079** | Non-amateur telecommand encryption enforcement (Happy Path). Traces to L2-MIS-079. | 1. Send encrypted 0x11 and unencrypted 0x11 over UHF.<br>2. Observe Radio_SecurityHandler. | Encrypted 0x11 accepted; unencrypted non-amateur 0x11 rejected immediately. | Not Run |
| **TC-129** | ASCON-AEAD128 telecommand decryption (Happy Path). Traces to L3-OBC-129, L4-OBC-185. | 1. Inject valid ASCON-128 packet for command 0x12.<br>2. Run Radio_SecurityHandler. | Decrypts in < 50 ms; payload matches raw command; Svc::CmdDispatcher routes command. | Not Run |
| **TC-130** | Cryptographic authenticity check on telecommands (Happy Path). Traces to L3-OBC-130, L4-OBC-186. | 1. Send telecommand with valid 128-bit MAC tag and nonce N=105.<br>2. Verify tag. | Tag check passes; sequence counter updates to N=105; ACK DL-12 returned. | Not Run |
| **TC-185** | Max-length 255B frame decryption prior to parsing (Happy Path). Traces to L4-OBC-185. | 1. Send 255B encrypted UART frame (16B IV, 4B header, 219B ciphertext, 16B tag). | Ciphertext decrypts in-place using 40B static RAM prior to parser call. | Not Run |
| **TC-186** | Pre-execution MAC tag verification (Happy Path). Traces to L4-OBC-186. | 1. Send command 0x04 with valid 128-bit MAC tag.<br>2. Monitor dispatcher gate. | Tag verified before execution; Low-Power Mode transition executes. | Not Run |
| **TC-187** | Replay protection on duplicate sequence counter (Edge Case). Traces to L4-OBC-187. | 1. Re-send telecommand with previously used sequence counter N=105. | Frame rejected; execution blocked; replay counter increments by 1; NACK queued. | Not Run |
| **TC-188** | Write-protected NVM key isolation (Edge Case). Traces to L4-OBC-188. | 1. Attempt unauthenticated read/write to MRAM key sector. | Access blocked by protection registers; keys remain isolated and unchanged. | Not Run |
| **TC-189** | Corrupted MAC tag rejection (Failure Condition). Traces to L4-OBC-189, EC-35. | 1. Flip 2 bytes in ASCON 128-bit MAC tag and inject into UHF buffer. | Authentication fails; frame dropped immediately; security rejection counter increments. | Not Run |
| **TC-306** | ITAR/EAR export compliance of cipher and NVM keys (Happy Path). Traces to CON-06, L1-PRJ-021. | 1. Audit crypto source files and Git repo for restricted code or keys. | Only public-domain CC0 ASCON-128 code present; keys isolated in onboard NVM. | Not Run |
| **TC-308** | Encryption guard on private downlinks and commands (Failure Condition). Traces to CON-08. | 1. Trigger DL-05/DL-11 downlink with null key pointer fault. | Unencrypted private downlink blocked; security fault asserted; zero cleartext sent. | Not Run |

### Group 2: Command Validation, Safeguards, Acknowledgment, and Scheduling (L2-SYS-049, L2-MIS-082–083, L3-OBC-131–132, L3-OBC-168, L4-OBC-190–198, CON-09)

| ID | Description | Steps | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC-049** | Execution of valid Ground Station commands (Happy Path). Traces to L2-SYS-049. | 1. Uplink valid commands 0x01 and 0x15 in Standby Mode.<br>2. Monitor subsystem execution. | Both commands validate and execute within < 50 ms. | Not Run |
| **TC-082** | Positive ACK and error-coded NACK reporting (Happy Path). Traces to L2-MIS-082. | 1. Uplink valid command 0x01 and invalid opcode 0xFF.<br>2. Capture UHF downlink (0xA2). | OBC sends ACK (DL-12) for 0x01 and NACK with error reason code for 0xFF. | Not Run |
| **TC-083** | Time-tagged command queueing and future epoch execution (Happy Path). Traces to L2-MIS-083. | 1. Uplink command 0x11 tagged for epoch T+300 s.<br>2. Advance RTC to T+300 s. | Command queues, sends scheduled ACK, and executes autonomously at T+300 s. | Not Run |
| **TC-131** | Composite syntax, bounds, and mode validation (Happy Path). Traces to L3-OBC-131. | 1. Send command 0x15 with Lake Erie coords (41.7 N, -81.2 W, 174 m) in Standby Mode. | Syntax, CRC-16, bounds, and mode checks pass; command routes to ADCS. | Not Run |
| **TC-132** | Telecommand confirmation and rejection downlink logging (Happy Path). Traces to L3-OBC-132. | 1. Uplink 5 valid commands and 1 malformed command.<br>2. Check GS SQLite log. | All 6 status responses received via 0xA2 and logged at Ground Station. | Not Run |
| **TC-168** | Autonomous dispatch of scheduled telecommands across orbit (Happy Path). Traces to L3-OBC-168. | 1. Queue 4 time-tagged commands.<br>2. Advance clock across 45-min orbit window. | All 4 commands execute in chronological epoch order without ground link. | Not Run |
| **TC-190** | Oversized packet (>255B) and bad CRC-16 rejection (Failure Condition). Traces to L4-OBC-190, EC-33. | 1. Inject 260B UART frame and 1-bit CRC-corrupted frame.<br>2. Monitor Radio_BufferManager. | Both frames discarded without buffer overflow; syntax error NACK queued. | Not Run |
| **TC-191** | Out-of-bounds parameter rejection (Edge Case). Traces to L4-OBC-191, EC-11, EC-59, EC-63. | 1. Send 0x15 with latitude = +95.0 deg and 0x10 with start_idx > end_idx. | Validator rejects both prior to dispatch; out-of-bounds NACK returned. | Not Run |
| **TC-192** | Mode authorization guard in Safe Mode (Failure Condition). Traces to L4-OBC-192. | 1. Place OBC in Safe Mode.<br>2. Send imaging downlink command 0x11. | Mode guard blocks 0x11; payload rails stay off; NACK 0xE001 returned. | Not Run |
| **TC-193** | Two-step confirmation safeguard for critical commands (Edge Case). Traces to L4-OBC-193. | 1. Send 0x06 (Reboot) alone.<br>2. Send 0x06 followed by valid confirmation token. | Unconfirmed 0x06 does not reboot; confirmed 0x06 executes controlled reboot. | Not Run |
| **TC-194** | Positive execution ACK generation (Happy Path). Traces to L4-OBC-194. | 1. Execute valid command 0x08 (Exit RF Inhibit).<br>2. Check 0xA2 queue. | Positive ACK (cmd 0x08, status 0x00) queued within 10 ms. | Not Run |
| **TC-195** | Negative NACK generation with error code (Failure Condition). Traces to L4-OBC-195. | 1. Send 0x03 (Exit Safe Mode) while SoC = 25% (< 40%, EC-21). | Command rejected; NACK with error code 0xE002 queued for downlink. | Not Run |
| **TC-196** | Non-volatile logging of command outcomes (Happy Path). Traces to L4-OBC-196. | 1. Run 3 valid and 2 invalid commands.<br>2. Read SPI log register 0x0100. | All 5 command outcomes and timestamps persisted in SPI storage. | Not Run |
| **TC-197** | 16-slot schedule queue full boundary check (Edge Case). Traces to L4-OBC-197. | 1. Fill static queue with 16 time-tagged commands.<br>2. Send 17th scheduled command. | First 16 stored; 17th rejected with queue-full NACK and zero heap allocation. | Not Run |
| **TC-198** | Epoch timer dispatch accuracy (Happy Path). Traces to L4-OBC-198. | 1. Queue command 0x04 for epoch 1800000500.<br>2. Advance RTC to target epoch. | Command dispatches within 1 RTOS tick (< 10 ms) of target epoch. | Not Run |
| **TC-309** | Multi-step validation across destructive commands (0x05–0x07, 0x09, 0x14) (Edge Case). Traces to CON-09. | 1. Send each destructive command with an expired confirmation token. | Pending critical action cancelled on timeout; zero destructive actions occur. | Not Run |

### Group 3: Downlink Operations, Frame Segmentation, Flow Control, and Telemetry Packaging (L2-SYS-043, L2-SYS-061, L2-MIS-075, L3-OBC-133–136, L4-OBC-199–202)

| ID | Description | Steps | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC-043** | Subsystem health telemetry collection for downlink (Happy Path). Traces to L2-SYS-043. | 1. Run 10 polling cycles out of ground contact.<br>2. Trigger downlink (0x01). | All 10 historical health snapshots retrieved from storage and downlinked. | Not Run |
| **TC-061** | Daily S-Band downlink capacity of >= 7 image sets (Happy Path). Traces to L2-SYS-061. | 1. Stage 7 compressed 4-band image sets in NAND.<br>2. Stream over 2.4 Mbps S-Band link. | All 7 image sets downlink within daily pass window with 100% CRC integrity. | Not Run |
| **TC-075** | Ground-commanded image downlink from storage (Happy Path). Traces to L2-MIS-075. | 1. Uplink command 0x11 for Image ID 0x03.<br>2. Monitor DP and S-Band stream. | OBC enables DP/S-Band rails (0x21), sends 0x12, and streams Image 0x03. | Not Run |
| **TC-133** | Primary S-Band image streaming with truncated block retry (Failure Condition). Traces to L3-OBC-133, EC-39. | 1. Start S-Band downlink (0x11).<br>2. Inject truncated file block from storage (EC-39). | Downlink_BlockRequester retries block fetch from storage and completes stream. | Not Run |
| **TC-134** | Backup UHF routing of image previews and metadata (Happy Path). Traces to L3-OBC-134. | 1. Uplink command 0x13 (Send Image via UHF) for Image 0x02.<br>2. Capture 0xA2 frames. | OBC routes compressed thumbnail and georeference header over UHF (DL-06). | Not Run |
| **TC-135** | Full telemetry downlink with link loss retry (Edge Case). Traces to L3-OBC-135, EC-36. | 1. Uplink command 0x01.<br>2. Drop ground carrier lock mid-burst (EC-36). | Radio_TxController retries 3x before re-buffering payload for next pass. | Not Run |
| **TC-136** | Historical fault log dump via command 0x0B (Happy Path). Traces to L3-OBC-136. | 1. Seed 5 fault records in SPI storage (0x0100).<br>2. Uplink command 0x0B (Send Errors). | OBC reads error logs from storage and transmits encrypted DL-11 frames over UHF. | Not Run |
| **TC-199** | Sequential transfer frame segmentation and CRC-16 (Happy Path). Traces to L4-OBC-199. | 1. Trigger downlink of 2 MB image and 16 KB log.<br>2. Inspect frame sequence numbers. | Files segmented into sequential frames with valid sequence numbers and CRC-16. | Not Run |
| **TC-200** | S-Band flow control and DMA underrun idle insertion (Edge Case). Traces to L4-OBC-200, EC-38. | 1. Stream at 42 MHz SPI DMA.<br>2. Induce DMA underrun (EC-38) and radio buffer-full signal. | Downlink_StreamManager inserts idle frames on underrun and pauses on buffer-full. | Not Run |
| **TC-201** | UHF preview fallback on S-Band synthesizer lock fault (Failure Condition). Traces to L4-OBC-201, EC-40. | 1. Simulate S-Band synth lock failure (EC-40).<br>2. Send 0x13 for UHF thumbnail. | Downlink_LockMonitor flags fault; OBC downlinks preview and metadata via UHF. | Not Run |
| **TC-202** | On-demand packaging of current health and fault logs (Happy Path). Traces to L4-OBC-202. | 1. Send command 0x01.<br>2. Decode frames in Ground Station F' GDS. | Frames contain complete current vitals, historical logs, and fault bitmasks. | Not Run |

### Group 4: Housekeeping Beacons, RF Inhibit Controls, and Amateur Radio Digipeater (L1-PRJ-018–019, L2-SYS-060, L2-MIS-078, L2-MIS-080, L3-OBC-140, L3-OBC-155, L3-OBC-171, L4-OBC-203–208, CON-04, CON-07)

| ID | Description | Steps | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC-018** | Amateur radio community support via public beacon and digipeater (Happy Path). Traces to L1-PRJ-018. | 1. Operate OBC in Standby/Repeater Mode.<br>2. Decode 49-s beacon and uplink amateur frame (0x02). | Unencrypted beacon decodes cleanly; amateur packet is digipeated on UHF downlink. | Not Run |
| **TC-019** | FCC regulatory compliance for RF hold and inhibit controls (Happy Path). Traces to L1-PRJ-019. | 1. Verify 45-min post-deployment RF silence and ground-commanded RF inhibit (0x07). | Zero RF emissions occur during 45-min hold or active RF inhibit state. | Not Run |
| **TC-060** | Periodic housekeeping beacon when not actively downlinking (Happy Path). Traces to L2-SYS-060. | 1. Run OBC in Standby Mode with no active downlink.<br>2. Monitor UHF TX over 5 min. | Unencrypted beacon (0xA1) transmits every 49 s; pauses during active downlink. | Not Run |
| **TC-078** | Ground-commanded shutdown and re-enablement of transmitters (Happy Path). Traces to L2-MIS-078. | 1. Send confirmed 0x07 (Enter RF Inhibit).<br>2. Verify silence.<br>3. Send 0x08 (Exit RF Inhibit). | Command 0x07 disables UHF/S-Band TX; 0x08 restores RF and resumes 49-s beacons. | Not Run |
| **TC-080** | Amateur digipeater in nominal mode and suppression during imaging (Edge Case). Traces to L2-MIS-080. | 1. Uplink amateur Repeat Message (0x02) in Standby Mode.<br>2. Uplink 0x02 in Imaging Mode. | First packet rebroadcasts via 0xA3; second packet is suppressed during Imaging Mode. | Not Run |
| **TC-140** | Immediate heartbeat assembly and dispatch after telemetry poll (Happy Path). Traces to L3-OBC-140. | 1. Run 60-s subsystem telemetry poll in Standby Mode (SoC = 75%).<br>2. Monitor 0xA1 TX. | OBC builds updated heartbeat packet immediately after poll and sends to UHF radio. | Not Run |
| **TC-155** | Amateur repeater packet staging and rebroadcast on UHF link (Happy Path). Traces to L3-OBC-155. | 1. Inject valid AX.25 amateur frame (0x02, 120B) into UHF UART.<br>2. Monitor 0xA3 output. | OBC validates callsign header, stages payload, and triggers UHF rebroadcast. | Not Run |
| **TC-171** | Commanded RF inhibit persistence across processor reboot (Edge Case). Traces to L3-OBC-171. | 1. Engage RF Inhibit (0x07).<br>2. Trigger watchdog reboot.<br>3. Check RF state post-boot. | Bootloader reads RF_INHIBIT flag from MRAM (0x0010) and keeps transmitters disabled. | Not Run |
| **TC-203** | Unencrypted housekeeping beacon field assembly check (Happy Path). Traces to L4-OBC-203. | 1. Capture RADIO_BEACON_TX (0xA1) frame.<br>2. Parse fields against injected vitals. | Unencrypted frame contains accurate time, mode, mV, SoC, temps, boot count, and faults. | Not Run |
| **TC-204** | Fixed 49-second housekeeping beacon cadence check (Happy Path). Traces to L4-OBC-204. | 1. Log timestamps of 20 consecutive RADIO_BEACON_TX (0xA1) dispatches. | Inter-beacon interval measures 49.0 s +/- 0.05 s with zero downlink collisions. | Not Run |
| **TC-205** | Automatic beacon suppression in Low-Power Mode and burn cycle (Edge Case). Traces to L4-OBC-205, EC-42. | 1. Enter Low-Power Mode (0x04).<br>2. Trigger 5-s antenna burn-wire pulse (EC-42). | Beacons suspend in Low-Power Mode; UHF_DeploySafety inhibits RF during 5-s burn. | Not Run |
| **TC-206** | Half-duplex uplink reception preemption over outgoing beacon/repeater (Edge Case). Traces to L4-OBC-206, EC-34. | 1. Queue outgoing 0xA1/0xA3 simultaneously with incoming uplink command 0x01 (EC-34). | Radio_Arbiter preempts outgoing TX, ingests uplink command first, then resumes TX. | Not Run |
| **TC-207** | Dedicated 64-kb circular ring buffer isolation for repeater packets (Edge Case). Traces to L4-OBC-207. | 1. Flood UHF receiver with 10 KB of 0x02 frames (> 64-kb buffer).<br>2. Check adjacent RAM. | Ring buffer overwrites oldest amateur frames; zero corruption of mission buffers. | Not Run |
| **TC-208** | Maximum transmission duty-cycle rate limiting on repeater (Failure Condition). Traces to L4-OBC-208. | 1. Inject continuous back-to-back 0x02 packets at max UART rate for 120 s. | Duty-cycle limiter throttles 0xA3 rebroadcasts to prevent PA overheating or battery drain. | Not Run |
| **TC-304** | Public beacon formatting and moderated amateur repeater filter (Happy Path). Traces to CON-04. | 1. Inject malformed amateur frame into 0x02 handler.<br>2. Verify beacon/repeater output. | Malformed frame dropped cleanly; valid frames conform to amateur radio standards. | Not Run |
| **TC-307** | Combined FCC RF hold timer and NOAA GSD threshold enforcement (Failure Condition). Traces to CON-07. | 1. Attempt RF TX at T+20 min (< 45 min) and imaging at GSD = 95 m/pixel (> 90 m). | Both RF TX and imaging capture are blocked by regulatory software guards. | Not Run |

### Group 5: Operational Mode State Machine, Power Rail Control, and Post-Deployment Startup Sequencing (L2-SYS-046, L2-MIS-071–073, L3-OBC-137, L3-OBC-156–158, L3-OBC-169–170, L4-OBC-209–216, L4-OBC-261)

| ID | Description | Steps | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC-046** | Positive orbit-average energy balance across nominal modes (Happy Path). Traces to L2-SYS-046, EC-26. | 1. Simulate 95-min orbit with MPPT charging and pulse-charge conflict retry (EC-26). | MPPT_ControlLoop resolves switch conflict; net orbital battery SoC delta is positive. | Not Run |
| **TC-071** | Mandatory 30-minute post-dispenser deployment wait timer (Happy Path). Traces to L2-MIS-071, EC-78. | 1. Boot OBC after dispenser exit.<br>2. Attempt deployable actuation at T+15 min and T+30 min. | Deploy_SafetyTimer blocks actuation before 30.0 min and actuates PIN_DEP_* at 30.0 min. | Not Run |
| **TC-072** | Mandatory 45-minute post-dispenser RF transmission wait timer (Happy Path). Traces to L2-MIS-072. | 1. Boot OBC after dispenser exit.<br>2. Monitor UHF/S-Band TX lines from T=0 to T+45 min. | Transmitters remain strictly silent until cumulative uptime reaches 45.0 min. | Not Run |
| **TC-073** | Autonomous startup, deployment, and detumbling within 1 week (Happy Path). Traces to L2-MIS-073. | 1. Run post-ejection sequence without ground contact.<br>2. Monitor deployables and ADCS mode. | OBC deploys solar/antennas after 30 min, commands Detumble (0x01), and reaches Standby. | Not Run |
| **TC-137** | Subsystem operational state configuration per active mode (Happy Path). Traces to L3-OBC-137. | 1. Transition FSM through Checkout, Standby, Imaging, and Downlink modes.<br>2. Check CAN bus. | OBC sends matching CMD_ADCS_SET_MODE (0x02) and CMD_PWR_RAIL_ON/OFF (0x21/0x22) frames. | Not Run |
| **TC-156** | Pre-launch state reset upon cycling deployment switches (Happy Path). Traces to L3-OBC-156. | 1. Cycle onboard deployment switches during ground test.<br>2. Read MRAM register 0x0010. | OBC resets all subsystems to Pre-Launch Mode and clears persisted mission flags. | Not Run |
| **TC-157** | OBC Standby Mode power consumption <= 0.45 W verification (Happy Path). Traces to L3-OBC-157. | 1. Place OBC in Standby Mode with DP rail off (0x22).<br>2. Measure current on Keysight supply. | Main Computer draws 104–123 mA (~0.40 W), remaining below the 0.45 W Standby limit. | Not Run |
| **TC-158** | OBC peak power consumption <= 2.50 W during active image processing (Happy Path). Traces to L3-OBC-158. | 1. Run simultaneous Main Computer pass control and RP2350 CI calculation.<br>2. Measure bus power. | Combined Main Computer and Data Processor peak power remains <= 2.50 W. | Not Run |
| **TC-169** | Dual 30-min deployable and 45-min RF hold enforcement across brownout (Edge Case). Traces to L3-OBC-169. | 1. Inject power brownout at T+20 min uptime.<br>2. Reboot and verify remaining hold times. | OBC resumes cumulative timers from MRAM (0x0010), deploying at T+30m and TX at T+45m. | Not Run |
| **TC-170** | Autonomous startup sequencing with solar array current verification (Happy Path). Traces to L3-OBC-170. | 1. Actuate PIN_DEP_SOLAR_ACT at T+30 min.<br>2. Poll MSG_PWR_DEPLOY_CONFIRM (0x54) and 0x41. | EPS confirms solar current generation (0x54) and ADCS confirms detumble complete (0x41). | Not Run |
| **TC-209** | Deterministic 10-mode Finite State Machine transition verification (Happy Path). Traces to L4-OBC-209. | 1. Exercise all valid transitions across the 10 operational modes and test invalid transitions. | All valid transitions execute deterministically; invalid direct transitions are blocked. | Not Run |
| **TC-210** | Staggered 50 ms subsystem power rail switching (Edge Case). Traces to L4-OBC-210, EC-22. | 1. Request simultaneous enable of Imager, DP, and S-Band rails (0x21, EC-22).<br>2. Trace current. | Power_Sequencer staggers rail turn-on by 50 ms intervals, preventing inrush current spike. | Not Run |
| **TC-211** | Graceful subsystem shutdown gating on pending storage writes (Edge Case). Traces to L4-OBC-211, EC-64. | 1. Command mode transition while DP write is pending (0x0200 = 0x00).<br>2. Monitor rail cut (0x22). | OBC sends shutdown notice, waits until DS_CHECK_IMAGE_INDEX = 0x01, then cuts rail. | Not Run |
| **TC-212** | 30-second non-volatile state persistence to SPI MRAM (Happy Path). Traces to L4-OBC-212. | 1. Run OBC for 5 minutes across mode changes.<br>2. Monitor SPI writes to register 0x0010. | Mode, mission flags, boot count, and inhibit timers persist to MRAM every 30.0 s. | Not Run |
| **TC-213** | Premature deployment command rejection during 30-min inhibit (Failure Condition). Traces to L4-OBC-213, EC-78. | 1. Issue deployable pulse trigger at T+10 min post-ejection (EC-78).<br>2. Check GPIO pins. | Deploy_SafetyTimer queues/blocks trigger; GPIO pins remain LOW until 30.0 min elapses. | Not Run |
| **TC-214** | Deployable burn-wire PWM current limiting at 2.5 A threshold (Edge Case). Traces to L4-OBC-214, EC-77. | 1. Actuate burn-wire with low-resistance load drawing > 2.5 A (EC-77).<br>2. Monitor PWM duty. | Deploy_CurrentLimiter clamps driver output via PWM so current never exceeds 2.5 A. | Not Run |
| **TC-215** | Deployable microswitch 100 ms debouncing and 2x retry on stuck mechanism (Failure Condition). Traces to L4-OBC-215, EC-43, EC-79. | 1. Inject contradictory switch bounce for 60 ms (EC-79) and indeterminate state (EC-43). | Deploy_Debouncer filters bounce over 100 ms and retries burn sequence up to 2 times. | Not Run |
| **TC-216** | Ground testing deployment switch cycle zeroing MRAM timers (Happy Path). Traces to L4-OBC-216. | 1. Cycle physical deployment switches on bench.<br>2. Read MRAM register 0x0010. | All post-deployment timers zero out and mission phase flags clear to Pre-Launch state. | Not Run |
| **TC-261** | Data Processor power rail gating during Standby Mode (Happy Path). Traces to L4-OBC-261. | 1. Verify Rail 0x01 state in Standby Mode, then enter Imaging/Downlink Mode. | DP rail remains disabled (0 W) in Standby and enables only for CI processing or S-Band TX. | Not Run |

### Group 6: System Timekeeping, GPS 1PPS Synchronization, and Ground Time Sync Fallback (L3-OBC-141–143, L4-OBC-217–219, L4-OBC-243)

| ID | Description | Steps | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC-141** | Continuous system clock and spacecraft epoch time maintenance (Happy Path). Traces to L3-OBC-141. | 1. Initialize spacecraft epoch clock and run across 24 simulated hours.<br>2. Query telemetry time. | System clock and epoch counter increment monotonically with zero missed seconds. | Not Run |
| **TC-142** | Autonomous spacecraft epoch synchronization against ADCS GPS time (Happy Path). Traces to L3-OBC-142. | 1. Inject valid ADCS GPS time packet and 1PPS pulse.<br>2. Measure OBC epoch clock offset. | OBC disciplines its epoch clock to within < 1.0 ms of GPS reference time. | Not Run |
| **TC-143** | Ground Station Sync Time (0x16) fallback when GPS is unavailable (Happy Path). Traces to L3-OBC-143. | 1. Disable GPS receiver input (simulating eclipse outage, EC-04).<br>2. Uplink Sync Time (0x16). | OBC updates spacecraft epoch clock to match ground telecommand timestamp. | Not Run |
| **TC-217** | Monotonic tick counter continuity and RTC drift <= 20 ppm (Happy Path). Traces to L4-OBC-217. | 1. Run uncalibrated RTC and monotonic tick counter for 48 hours against frequency counter. | Monotonic counter never decreases; RTC frequency drift remains <= 20 ppm. | Not Run |
| **TC-218** | Primary GPS 1PPS interrupt dropout fallback to internal oscillator (Edge Case). Traces to L4-OBC-218, EC-14. | 1. Suppress 1PPS interrupt signal for 10 consecutive seconds (EC-14), then restore pulse. | GPS_TimeKeeper falls back to internal oscillator without clock jump and resyncs on next 1PPS. | Not Run |
| **TC-219** | Corrupted GPS NMEA checksum rejection and ground sync recovery (Failure Condition). Traces to L4-OBC-219, EC-15. | 1. Inject GPS time frame with corrupted checksum (EC-15).<br>2. Uplink valid Sync Time (0x16). | Corrupted GPS frame is rejected; subsequent ground Sync Time (0x16) updates epoch cleanly. | Not Run |
| **TC-243** | In-pass timeout evaluation immunity to mid-pass epoch clock step (Edge Case). Traces to L4-OBC-243. | 1. Start imaging pass warmup timer.<br>2. Uplink Sync Time (0x16) advancing epoch clock by +300 s. | Warmup timeout evaluates monotonic tick counter and does not falsely abort mid-pass. | Not Run |

### Group 7: Subsystem Health Monitoring, Thermal Regulation, and Internal Telemetry (L2-SYS-050, L3-OBC-138–139, L3-OBC-149–150, L3-OBC-174, L4-OBC-220–222, L4-OBC-231–233, L4-OBC-257–259)

| ID | Description | Steps | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC-050** | Internal component operation and thermal cutoff verification across -40°C to +60°C (Happy Path). Traces to L2-SYS-050. | 1. Sweep simulated thermistor inputs across -40°C to +60°C.<br>2. Verify telemetry and thermal guards. | All internal subsystems operate nominally inside [-40°C, +60°C] and trigger cutoffs outside bounds. | Not Run |
| **TC-138** | Periodic 60-second subsystem telemetry collection and analysis (Happy Path). Traces to L3-OBC-138. | 1. Run OBC scheduler for 180 s.<br>2. Monitor CAN polls 0x01 (ADCS), 0x20 (EPS), and 0x32 (Imager). | OBC polls all subsystems at exact 60.0 s intervals and updates Svc::TlmChan channels. | Not Run |
| **TC-139** | Immediate processing of asynchronous subsystem fault alerts (Happy Path). Traces to L3-OBC-139. | 1. Inject async CAN alert MSG_IMG_HARDWARE_FAULT (0x63) mid-polling cycle.<br>2. Measure response time. | OBC preempts background tasks and processes fault alert in < 100 ms without waiting for 60-s poll. | Not Run |
| **TC-149** | Main Computer self-health and status telemetry collection (Happy Path). Traces to L3-OBC-149. | 1. Trigger 60-s telemetry cycle.<br>2. Inspect Main Computer health struct in Svc::TlmChan. | CPU load, SRAM usage, internal temp, uptime, CAN status, and boot count are recorded accurately. | Not Run |
| **TC-150** | Data Processor health and processing status telemetry collection (Failure Condition). Traces to L3-OBC-150, EC-76. | 1. Poll DP status during CI run.<br>2. Simulate hardware accelerator hang (EC-76). | Processor_DSPMonitor surfaces fault flag to Main Computer, resets core, and logs fallback status. | Not Run |
| **TC-174** | Thermal control actuation and subsystem operating inhibits (Failure Condition). Traces to L3-OBC-174, EC-25, EC-37, EC-56. | 1. Inject battery temp = 46°C (> 45°C, EC-25), S-Band PA = 86°C (> 85°C, EC-37), and imager = 61°C (EC-56). | Charge current cuts to 0 A (EC-25), S-Band rate throttles 50% (EC-37), and imager powers down (EC-56). | Not Run |
| **TC-220** | Fixed 60-second telemetry polling scheduler determinism under load (Happy Path). Traces to L4-OBC-220. | 1. Execute heavy background logging alongside 60-s telemetry scheduler over 10 cycles. | Polling jitter remains < 10 ms across Power, ADCS, Comms, Thermal, and Payload polls. | Not Run |
| **TC-221** | Telemetry threshold evaluation and disconnected thermistor fault handling (Edge Case). Traces to L4-OBC-221, EC-32. | 1. Inject battery voltage out-of-bounds and disconnected NTC reading (-273°C, EC-32). | Evaluator asserts threshold fault flag and Monitor_SensorFault applies ambient model fallback. | Not Run |
| **TC-222** | < 100 ms preemption latency on critical asynchronous fault alerts (Happy Path). Traces to L4-OBC-222. | 1. Assert MSG_PWR_LOW_BATTERY_ALERT (0x51) on CAN bus.<br>2. Measure GPIO/CAN response on logic analyzer. | High-priority ISR/task preempts normal threads and issues rail-off command (0x22) in < 100 ms. | Not Run |
| **TC-231** | Main Computer and Data Processor internal temperature sampling every 60 s (Happy Path). Traces to L4-OBC-231. | 1. Vary MCU thermal sensor ADC values.<br>2. Read reported temperatures across 3 polling cycles. | Reported processor temperatures match calibrated ADC inputs within +/- 0.5°C every 60 s. | Not Run |
| **TC-232** | Main Computer and Data Processor supply voltage and current telemetry (Edge Case). Traces to L4-OBC-232, EC-29. | 1. Poll 0x20/0x53 vitals during nominal and shunt-saturation current spike (EC-29). | Nominal mV/mA values log every 60 s; shunt exceedance triggers Monitor_OvercurrentGuard alert. | Not Run |
| **TC-233** | CPU load, RAM utilization, uptime, and reboot counter telemetry (Happy Path). Traces to L4-OBC-233. | 1. Run synthetic 70% CPU load and trigger 1 controlled reboot.<br>2. Read processor resource telemetry. | Telemetry accurately reports ~70% CPU load, exact static RAM usage, uptime reset, and boot_count + 1. | Not Run |
| **TC-257** | 60-second thermal setpoint regulation for heaters and cutoffs (Edge Case). Traces to L4-OBC-257, EC-25. | 1. Drop simulated battery temp below low setpoint, then raise above 45°C (EC-25), then cool to 37°C. | Heater rail enables at low setpoint; charging disables at > 45°C and resumes when cooled < 38°C. | Not Run |
| **TC-258** | Periodic Main Computer watchdog heartbeat to Power Subsystem (Failure Condition). Traces to L4-OBC-258, ADR-004. | 1. Verify nominal heartbeat to EPS within the window.<br>2. Halt OBC heartbeat to test EPS failover. | Nominal heartbeat prevents EPS reset; halting heartbeat triggers EPS power-cycle and UHF failover beacon. | Not Run |
| **TC-259** | Onboard EnduroSat auxiliary accelerometer and magnetometer readout (Happy Path). Traces to L4-OBC-259. | 1. Poll board-level 3-axis accelerometer and magnetometer over internal I2C during 60-s cycle. | Auxiliary body-rate and magnetic field vectors are sampled cleanly and packaged in OBC telemetry. | Not Run |

### Group 8: Data Storage Management, File Integrity, Bad-Block Remapping, and Verified Purging (L2-SYS-042, L2-MIS-084, L3-OBC-144–148, L4-OBC-223–230, L4-OBC-253)

| ID | Description | Steps | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC-042** | Storing at least 7 complete multispectral image sets in NAND Flash (Happy Path). Traces to L2-SYS-042. | 1. Write 7 complete 4-band multispectral image sets to SPI NAND Flash.<br>2. Query 0x0200 index. | Flash stores all 7 image sets without error; DS_CHECK_IMAGE_INDEX (0x0200) returns 0x01 (Stored). | Not Run |
| **TC-084** | Verified handshake image retention until explicit Ground Station purge (Happy Path). Traces to L2-MIS-084. | 1. Downlink Image 0x05 twice with simulated link drop on first pass.<br>2. Send confirmed 0x14 purge. | Image 0x05 remains intact across failed pass and is deleted only after confirmed 0x14 command. | Not Run |
| **TC-144** | Onboard non-volatile mass storage capacity verification (>= 8 GB baseline) (Happy Path). Traces to L3-OBC-144. | 1. Initialize SPI NAND Flash driver.<br>2. Query total addressable block count and byte capacity. | Storage driver reports full baseline capacity with sufficient margin for > 7 image sets and logs. | Not Run |
| **TC-145** | Radiation-tolerant SPI MRAM persistence for critical states and timers (Happy Path). Traces to L3-OBC-145. | 1. Write mission flags and inhibit timers via DS_WRITE_FLAG (0x0010).<br>2. Power-cycle board and read 0x0010. | DS_READ_FLAGS returns identical 3-byte bitmask and timer values from MRAM after power cycle. | Not Run |
| **TC-146** | End-to-end store, lossless compress, decompress, and delete operations (Happy Path). Traces to L3-OBC-146. | 1. Compress raw image, write to NAND, read back, decompress, verify pixels, and delete file. | Decompressed image is bit-for-bit identical to raw source; deletion frees all allocated blocks. | Not Run |
| **TC-147** | Protection of unpurged payload images against premature buffer overwrite (Edge Case). Traces to L3-OBC-147. | 1. Capture 7 images without sending Ground Station purge command 0x14.<br>2. Attempt buffer clear. | Imager Adapter and NAND storage reject unauthenticated buffer clear; all 7 images stay locked. | Not Run |
| **TC-148** | Data storage health and status telemetry collection under SPI bus dropout (Failure Condition). Traces to L3-OBC-148, EC-72. | 1. Poll storage telemetry during nominal run.<br>2. Disconnect SPI MISO/SS line mid-poll (EC-72). | Storage_BusRecovery flags SPI hardware error, routes logs to SRAM ring buffer, and recovers on reset. | Not Run |
| **TC-223** | Lossless image compression with execution slot timeout adaptation (Edge Case). Traces to L4-OBC-223, EC-74. | 1. Compress high-entropy 4-band image set.<br>2. Constrain processing slot timer (EC-74). | Processor_DynamicScheduler completes lossless packaging within slot without altering pixel values. | Not Run |
| **TC-224** | Stored file CRC-32 calculation on write and verification on readback (Failure Condition). Traces to L4-OBC-224. | 1. Write image file with computed CRC-32.<br>2. Flip 1 bit in flash page and read file back. | Readback CRC-32 check detects 1-bit corruption immediately and flags file integrity error. | Not Run |
| **TC-225** | Authenticated Purge Stored Image (0x14) deletion and camera buffer clear (Happy Path). Traces to L4-OBC-225. | 1. Send authenticated, two-step confirmed command 0x14 for Image ID 0x04.<br>2. Monitor CAN 0x33. | OBC deletes Image 0x04 in NAND Flash and sends CMD_IMG_PURGE_BUFFER (0x33) to Imager Adapter. | Not Run |
| **TC-226** | Free storage capacity calculation and reporting every 60 seconds (Happy Path). Traces to L4-OBC-226. | 1. Write 50 MB of test data to NAND Flash.<br>2. Trigger 60-s telemetry poll. | Reported free capacity decreases by exactly 50 MB in the 60-second storage telemetry packet. | Not Run |
| **TC-227** | Automatic bad-block remapping and counter increment on write failure (Failure Condition). Traces to L4-OBC-227, EC-71. | 1. Inject simulated NAND program-fail status on target block 0x04A0 during image write (EC-71). | Storage_BadBlockManage marks 0x04A0 bad, remaps chunk to spare block, and increments bad-block count. | Not Run |
| **TC-228** | Flash wear-leveling block distribution and status telemetry (Happy Path). Traces to L4-OBC-228. | 1. Execute 1,000 cyclic file write/delete operations.<br>2. Inspect block erase count distribution. | Writes distribute evenly across physical erase blocks; wear-leveling metrics report in telemetry. | Not Run |
| **TC-229** | High storage utilization warning flag assertion at 85% capacity (Edge Case). Traces to L4-OBC-229. | 1. Fill NAND Flash to 84.9% (flag LOW), then write data to reach 85.1% capacity.<br>2. Poll telemetry. | Warning flag STORAGE_WARN_85 transitions HIGH at 85.1% and clears after purging below 85%. | Not Run |
| **TC-230** | FIFO historical telemetry log rollover at 99% capacity preserving images (Edge Case). Traces to L4-OBC-230, EC-69. | 1. Fill NAND Flash to 99.1% with locked science images and old telemetry logs (EC-69).<br>2. Write new log. | Storage_SpaceManager overwrites oldest unflagged telemetry logs in FIFO order; science images stay intact. | Not Run |
| **TC-253** | Mutex serialization of concurrent storage writes from Imager and Telemetry threads (Edge Case). Traces to L4-OBC-253, EC-70. | 1. Trigger simultaneous SPI file writes from DP image offload and Main Computer log thread (EC-70). | Storage_FileLockArbiter serializes writes via FreeRTOS mutex with zero interleaved bytes or corruption. | Not Run |

### Group 9: ADCS Ephemeris Forwarding, Attitude/Position Georeferencing, and Autonomous Pass Execution Sequencer (L0-PRJ-001–002, L1-SCI-008–010, L1-PRJ-020, L2-SYS-038, L2-SYS-040–041, L2-MIS-074, L2-MIS-081, L3-OBC-151–154, L3-OBC-173, L4-OBC-234–242, L4-OBC-260)

| ID | Description | Steps | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC-001** | End-to-end Lake Erie HAB multispectral image collection demonstration (Happy Path). Traces to L0-PRJ-001. | 1. Uplink Lake Erie target coords (0x15) and TLE (0x12).<br>2. Run pass sequencer through capture and CI processing. | Complete 4-band multispectral image set and CI map of Lake Erie are captured, georeferenced, and stored. | Not Run |
| **TC-002** | Drone-rated multispectral imager orchestration via Imager Adapter (Happy Path). Traces to L0-PRJ-002. | 1. Enable Imager rail (0x21).<br>2. Send warmup (0x30) and burst trigger (0x31) over CAN. | Imager Adapter orchestrates drone-rated sensor warmup and burst capture without bus errors. | Not Run |
| **TC-008** | 4-band (620, 650, 680, 708 nm) 10 nm FWHM capture and filter wheel homing retry (Edge Case). Traces to L1-SCI-008, EC-57. | 1. Command 4-band capture (0x31).<br>2. Inject filter wheel position out-of-bounds reading (EC-57). | MultiImg_FilterHoming retries homing sequence, indexes all 4 spectral bands, and completes capture. | Not Run |
| **TC-009** | Ground Sampling Distance (GSD) <= 90 m/pixel verification at nadir (Happy Path). Traces to L1-SCI-009. | 1. Supply LEO orbital altitude (500 km) and nadir attitude state vector to pass pre-check. | Calculated GSD is between 70 m and 90 m per pixel; pass constraint verification passes. | Not Run |
| **TC-010** | Geographic center coordinate reference tagging on each image set (Happy Path). Traces to L1-SCI-010. | 1. Complete image capture over Lake Erie target.<br>2. Inspect stored image metadata header. | Header contains verified geographic center coordinates derived from synchronized ECEF/LVLH vectors. | Not Run |
| **TC-020** | NOAA remote sensing compliance via GSD check and downlink encryption (Happy Path). Traces to L1-PRJ-020. | 1. Verify pre-pass GSD gate and ASCON-AEAD128 encryption on S-Band/UHF image downlinks. | All downlinked remote sensing data streams are encrypted with ASCON-128 and comply with NOAA rules. | Not Run |
| **TC-038** | Active ADCS target pointing across entire imaging pass window (Happy Path). Traces to L2-SYS-038. | 1. Issue CMD_ADCS_SET_MODE (0x04 Target Tracking) at pass lead time.<br>2. Monitor attitude error. | ADCS maintains closed-loop target tracking across the entire scheduled pass window. | Not Run |
| **TC-040** | LVLH orientation determination and NaN/+Inf matrix fallback guard (Failure Condition). Traces to L2-SYS-040, EC-01, EC-05. | 1. Poll LVLH attitude during capture.<br>2. Inject solar flare saturation (EC-05) and NaN matrix value (EC-01). | SunSensor_Filter masks saturated reading; ACDS_MatrixGuard falls back to last valid LVLH state matrix. | Not Run |
| **TC-041** | ECEF position determination and eclipse dead-reckoning fallback (Edge Case). Traces to L2-SYS-041, EC-04, EC-13. | 1. Poll ECEF position during capture.<br>2. Simulate GPS lock loss in orbital shadow (EC-04). | ACDS_NavFallback switches smoothly to dead-reckoning propagation until GPS lock restores. | Not Run |
| **TC-074** | Imaging criteria rejection when target GSD >= 90 m/pixel (Edge Case). Traces to L2-MIS-074. | 1. Configure high off-nadir slant range yielding GSD = 94 m/pixel.<br>2. Trigger pass pre-check. | Sequencer rejects imaging attempt prior to rail turn-on due to GSD >= 90 m/pixel violation. | Not Run |
| **TC-081** | Semi-autonomous nominal mission pass execution without ground contact (Happy Path). Traces to L2-MIS-081. | 1. Load pass schedule queue and disconnect Ground Station.<br>2. Advance clock across 3 orbits. | OBC autonomously executes scheduled passes, processes CI maps, and returns to Standby Mode. | Not Run |
| **TC-151** | Forwarding uplinked TLEs (0x12) and target coords (0x15) to ADCS (Happy Path). Traces to L3-OBC-151. | 1. Uplink TLE set (0x12) and target coordinates (0x15).<br>2. Capture CAN bus frames 0x03–0x06. | OBC forwards all TLE chunks (0x03) and IEEE 754 Lat/Lon/Alt frames (0x04–0x06) to ADCS and receives 0x40 ACK. | Not Run |
| **TC-152** | Pre-imaging constraint verification gate before camera activation (Happy Path). Traces to L3-OBC-152. | 1. Set SoC = 65%, GSD = 78 m, and zero faults.<br>2. Run pre-pass verification at lead time. | OBC verifies all constraints pass before enabling payload power rail (0x21). | Not Run |
| **TC-153** | Scheduled ADCS attitude mode commanding and S-Band pointing predictor fallback (Edge Case). Traces to L3-OBC-153, EC-46. | 1. Command mode transitions (0x01–0x05).<br>2. Delay ADCS pointing update thread during S-Band pass (EC-46). | ADCS transitions modes on schedule; SBand_PointPredictor falls back to last predicted ephemeris vector. | Not Run |
| **TC-154** | Payload imager burst capture command and overlapping trigger queueing (Edge Case). Traces to L3-OBC-154, EC-53, EC-54. | 1. Send CMD_IMG_TRIGGER_BURST (0x31) with exposure = 12,000 ms (EC-53) and a second trigger during readout (EC-54). | TruthImager_ExposureControl caps exposure at 10,000 ms; StateSequencer queues second trigger until readout finishes. | Not Run |
| **TC-173** | Synchronized ECEF position and LVLH attitude metadata association (Happy Path). Traces to L3-OBC-173. | 1. Trigger burst capture (0x31).<br>2. Verify timestamp alignment between capture and ADCS state vectors. | Captured image set is bound to ECEF and LVLH vectors sampled within < 50 ms of shutter trigger. | Not Run |
| **TC-234** | Ephemeris target forwarding and automatic pass schedule request (0x07) (Happy Path). Traces to L4-OBC-234. | 1. Uplink new TLE (0x12).<br>2. Monitor CAN sequence 0x03 followed by CMD_ADCS_REQ_SCHEDULE (0x07). | OBC forwards TLE to ADCS, automatically transmits 0x07, and ingests MSG_ADCS_SCHEDULE_PACKET (0x43). | Not Run |
| **TC-235** | Fixed-capacity 16-pass schedule queue retention and empty-queue idle behavior (Edge Case). Traces to L4-OBC-235. | 1. Evaluate pass sequencer with empty queue (0 entries), then populate all 16 PassRecord slots. | When empty, sequencer stays idle in Minimal Drag (0x03) with rails off; when full, holds 16 passes in static RAM. | Not Run |
| **TC-236** | Duplicate pass dropping and overlapping window priority tie-breaking (Edge Case). Traces to L4-OBC-236. | 1. Ingest duplicate Pass ID 0x04 and two overlapping passes with priorities P=1 and P=3. | Duplicate Pass 0x04 is dropped; overlapping window selects higher-priority pass (P=3) and skips P=1. | Not Run |
| **TC-237** | Pre-pass abort when battery SoC < 20%, GSD >= 90 m, or critical fault active (Failure Condition). Traces to L4-OBC-237. | 1. Set simulated battery SoC to 18% (< 20% threshold).<br>2. Trigger scheduled pass at lead time. | Pre-pass check fails; payload rail stays off; pass aborts with LOW_SOC_PASS_ABORT telemetry flag. | Not Run |
| **TC-238** | Lead-time target preparation sequence (Rail ON, ADCS Track, Imager Warmup) (Happy Path). Traces to L4-OBC-238. | 1. Advance clock to pass lead time.<br>2. Capture outgoing CAN commands from Main Computer. | OBC enables Imager rail (0x21), commands ADCS Target Tracking (0x02/0x04), and starts sensor warmup (0x30). | Not Run |
| **TC-239** | Synchronized capture gating on both ADCS target lock (0x42) and warmup ready (0x61) (Edge Case). Traces to L4-OBC-239. | 1. Assert MSG_IMG_WARMUP_READY (0x61) 3 s before MSG_ADCS_TARGET_ACQUIRED (0x42).<br>2. Monitor 0x31 trigger. | OBC withholds CMD_IMG_TRIGGER_BURST (0x31) until both 0x61 and 0x42 are asserted within window. | Not Run |
| **TC-240** | Post-pass payload rail power-down and Minimal Drag return upon capture complete (0x62) (Happy Path). Traces to L4-OBC-240. | 1. Assert MSG_IMG_CAPTURE_COMPLETE (0x62).<br>2. Monitor CAN commands to EPS and ADCS. | OBC disables Imager rail (0x22), sends CMD_ADCS_STOP_TRACK (0x08), and sets ADCS to Minimal Drag (0x03). | Not Run |
| **TC-241** | Mid-pass fault abort on warmup timeout, imager fault (0x63), lock timeout (0x44), or low battery (0x51) (Failure Condition). Traces to L4-OBC-241, EC-52, EC-60. | 1. Initiate pass and inject MSG_ADCS_POINTING_TIMEOUT (0x44) in Run A and warmup > 60 s in Run B. | Sequencer immediately aborts pass, cuts camera power (0x22), sends 0x08 Stop Track, and logs ABORT_FAULT. | Not Run |
| **TC-242** | Immediate imaging pass preemption upon Ground Station carrier detect (Edge Case). Traces to L4-OBC-242. | 1. Start active imaging pass.<br>2. Assert RADIO_CARRIER_DETECT with incoming ground telecommand (0x07). | Active pass aborts in < 100 ms; camera rails cut (0x22); ADCS transitions to Ground Station Pointing (0x05). | Not Run |
| **TC-260** | Image georeference sidecar header generation upon capture completion (Happy Path). Traces to L4-OBC-260. | 1. Complete image burst (0x62).<br>2. Read generated image metadata header in SPI storage. | OBC queries ADCS ECEF/LVLH vectors and writes complete georeference sidecar header with image file. | Not Run |

### Group 10: On-Board Chlorophyll Index Processing and Data Processor Pipeline Supervision (L3-OBC-167, L4-OBC-244–246, L4-OBC-262)

| ID | Description | Steps | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC-167** | Dedicated RP2350 Data Processor Chlorophyll Index execution offloading (Happy Path). Traces to L3-OBC-167, ADR-001. | 1. Trigger CI pipeline (0x10) on RP2350 while Main Computer runs 100 Hz ADCS/CDH loops. | RP2350 completes CI conversion in < 2.5 s; Main Computer experiences 0% scheduling jitter. | Not Run |
| **TC-244** | Numerical accuracy of 4-band Chlorophyll Index map computation (Happy Path). Traces to L4-OBC-244. | 1. Feed 50 calibrated 4-band Lake Erie test image sets to CMD_DP_START_PROCESSING (0x10).<br>2. Compare to numpy reference. | DP emits MSG_DP_PROCESSING_DONE (0x72); all 50 output CI maps match numpy reference within delta < 0.001. | Not Run |
| **TC-245** | UART raw image block CRC-16 verification and 3x retry on corruption (Edge Case). Traces to L4-OBC-245, EC-51, EC-75. | 1. Stream raw blocks from Imager Adapter to DP over 3.0 Mbps UART.<br>2. Corrupt CRC on 2 transfers (EC-75). | Processor_FrameVerifier issues NACK, retries block fetch (succeeding on retry 2), and assembles clean frame. | Not Run |
| **TC-246** | Arithmetic divide-by-zero and overflow guard during CI calculation (Failure Condition). Traces to L4-OBC-246, EC-73. | 1. Inject synthetic multispectral frame with zero-denominator pixel band values (EC-73). | Processor_MathGuard catches divide-by-zero exception, logs warning, and stores raw uncompressed image safely. | Not Run |
| **TC-262** | Data Processor execution timeout abort and rail cut on hung pipeline (Failure Condition). Traces to L4-OBC-262. | 1. Start CI processing (0x10) and stall RP2350 main loop past maximum execution window. | Main Computer timer expires, sends CMD_DP_ABORT (0x11), cuts DP power rail (0x22), and logs timeout fault. | Not Run |

### Group 11: Fault Detection, Isolation, and Recovery (FDIR), Watchdog Supervision, and Safe Mode (L2-SYS-048, L2-SYS-059, L3-OBC-159–163, L3-OBC-166, L4-OBC-247–252, L4-OBC-254–255, L4-OBC-263, CON-10)

| ID | Description | Steps | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC-048** | Autonomous Safe Mode entry keeping spacecraft power-positive and commandable (Happy Path). Traces to L2-SYS-048. | 1. Inject critical EPS fault alert (0x51).<br>2. Verify Safe Mode state, ADCS Sun-Pointing (0x02), and commandability. | OBC enters Safe Mode in < 100 ms, sheds payload loads, points solar arrays at Sun, and accepts ground commands. | Not Run |
| **TC-059** | Radiation survivability via MRAM state recovery and NAND bad-block handling (Edge Case). Traces to L2-SYS-059, EC-67, EC-71. | 1. Inject simulated SEU bit-flip in config partition (EC-67) and NAND flash block (EC-71). | Bootloader recovers defaults from golden ROM (EC-67) and storage remaps bad block cleanly (EC-71). | Not Run |
| **TC-159** | Software exception, task hang, and memory corruption recovery (Failure Condition). Traces to L3-OBC-159, EC-65, EC-66. | 1. Inject null-pointer fault and task deadlock in background worker thread. | Exception handler and F' Svc::Health watchdog detect fault, isolate/restart task, and preserve mission state. | Not Run |
| **TC-160** | Internal communication bus fault isolation without affecting healthy subsystems (Edge Case). Traces to L3-OBC-160, EC-68. | 1. Induce CAN bus-off error on Imager branch (EC-68) while polling EPS and ADCS. | MainComp_CANSupervisor resets controller up to 3x and isolates faulted node; EPS/ADCS comms continue. | Not Run |
| **TC-161** | Autonomous and ground-commanded Safe Mode transitions (Happy Path). Traces to L3-OBC-161, EC-21. | 1. Trigger autonomous Safe Mode via SoC = 14% (< 15%, EC-21).<br>2. Reset and test commanded Safe/Emergency entry. | Both autonomous low-SoC trip and ground command transition spacecraft cleanly to Safe/Failsafe posture. | Not Run |
| **TC-162** | Safe Mode exit blocked until authenticated Ground Station command 0x03 arrives (Edge Case). Traces to L3-OBC-162. | 1. In Safe Mode, recharge battery SoC to 55% (> 40%).<br>2. Verify mode before and after sending command 0x03. | OBC remains latched in Safe Mode after recharge and exits to Checkout Mode only upon receiving authenticated 0x03. | Not Run |
| **TC-163** | Radiation shielding inspection for Main Computer, Data Processor, and Data Storage (Happy Path). Traces to L3-OBC-163. | 1. Inspect mechanical avionics enclosure and EnduroSat board shielding against orbital radiation analysis. | Shielding thickness and component placement satisfy mission total ionizing dose (TID) requirements. | Not Run |
| **TC-166** | Radiation-resistant reboot overwriting corrupted flight software from golden image (Failure Condition). Traces to L3-OBC-166, EC-67. | 1. Corrupt primary NOR Flash application CRC.<br>2. Trigger reboot and monitor MainComp_BootLoader (EC-67). | Bootloader detects CRC failure and overwrites/boots clean flight software from radiation-tolerant golden ROM. | Not Run |
| **TC-247** | FreeRTOS preemptive priority-based task scheduling verification (Happy Path). Traces to L4-OBC-247. | 1. Run low-priority storage/logging task.<br>2. Trigger high-priority ADCS control and fault alert tasks. | High-priority tasks immediately preempt background tasks with sub-millisecond context switch latency. | Not Run |
| **TC-248** | Zero dynamic heap memory allocation enforcement post-initialization (Happy Path). Traces to L4-OBC-248. | 1. Run cppcheck static analysis and FreeRTOS heap hook across full 10-mode mission simulation. | Zero calls to malloc/new or dynamic heap allocations occur after initialization (0 bytes allocated in flight). | Not Run |
| **TC-249** | Runtime RAM utilization > 95% background task suspension guard (Edge Case). Traces to L4-OBC-249, EC-65. | 1. Artificially inflate stack/buffer usage to 95.5% of SRAM capacity (EC-65).<br>2. Monitor task states. | MainComp_MemManager suspends lowest-priority background tasks immediately, preventing stack overflow. | Not Run |
| **TC-250** | Hardware watchdog timer reset at 500 ms upon software execution hang (Failure Condition). Traces to L4-OBC-250, EC-66. | 1. Stall FreeRTOS scheduler in an infinite interrupt loop stopping watchdog GPIO strobing (EC-66). | External hardware watchdog triggers hard processor reset at 500 ms +/- 50 ms and recovers system. | Not Run |
| **TC-251** | Golden image boot fallback after 3 consecutive failed primary boot attempts (Failure Condition). Traces to L4-OBC-251, EC-67. | 1. Corrupt primary flight software image CRC.<br>2. Observe 3 consecutive boot attempts by MainComp_BootLoader. | After 3 failed primary boot verifications, bootloader boots from write-protected golden fallback image and sets telemetry flag. | Not Run |
| **TC-252** | 3x internal bus transaction retry and local bus controller reset (Edge Case). Traces to L4-OBC-252, EC-03, EC-23, EC-68. | 1. Inject corrupted CAN frames from ADCS (EC-03) and EPS (EC-23) and a UART timeout (Peer Review #4). | Bus parser retries failed reads up to 3 times and resets local bus controller on timeout without system reboot. | Not Run |
| **TC-254** | Autonomous Safe Mode entry and load shedding on unrecoverable fault or SoC < 15% (Failure Condition). Traces to L4-OBC-254, EC-21. | 1. Drop battery SoC to 14% (0x51, EC-21).<br>2. Verify rail states and FSM mode. | Power_SoCSupervisor transitions OBC to Safe Mode, cuts Imager/DP/S-Band rails (0x22), and commands Sun-Pointing. | Not Run |
| **TC-255** | Authenticated Exit Safe Mode (0x03) clearing latched fault flags (Happy Path). Traces to L4-OBC-255. | 1. With SoC = 45% in Safe Mode, uplink authenticated command 0x03.<br>2. Read MRAM fault register. | Latched Safe Mode fault flags clear in MRAM and OBC transitions cleanly to Checkout Mode. | Not Run |
| **TC-263** | Sequential EPS power-rail node isolation when shared CAN bus stays locked after 3 resets (Failure Condition). Traces to L4-OBC-263, EC-68. | 1. Clamp CAN bus dominant via simulated latched Imager node.<br>2. Observe 3 CAN resets followed by rail cuts. | After 3 failed controller resets, OBC commands EPS (0x22) to sequentially disable non-essential rails, isolating faulted node. | Not Run |
| **TC-310** | Cross-subsystem fault isolation across CAN, gated UART, and EPS failover (Failure Condition). Traces to CON-10, ADR-004. | 1. Inject simultaneous Secondary Payload UART babbling fault and Imager CAN latch-up. | Dynamic UART gating isolates Secondary Payload and EPS rail cut isolates Imager; core OBC/ADCS/EPS operations continue unimpaired. | Not Run |

### Group 12: On-Orbit Reconfiguration, Umbilical Diagnostics, Physical Envelope, and Programmatic Compliance (L0-PRJ-004, L1-SCI-012, L1-MIS-015, L1-PRJ-021, L2-SYS-026–027, L2-SYS-044, L2-SYS-053, L3-OBC-164–165, L3-OBC-172, L3-OBC-175–176, L4-OBC-256, L4-OBC-264–268, CON-01–03, CON-05)

| ID | Description | Steps | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- |
| **TC-004** | Compliance audit across all external stakeholder and regulatory requirements (Happy Path). Traces to L0-PRJ-004. | 1. Audit FCC, NOAA, EAR/ITAR, and CubeSat Design Specification compliance matrices. | 100% of external regulatory and stakeholder constraints are satisfied and verified by inspection/test. | Not Run |
| **TC-012** | 1-year Lake Erie seasonal mission operational endurance analysis (Happy Path). Traces to L1-SCI-012. | 1. Evaluate orbital pass frequency, flash wear-leveling, and power budget over 365-day simulation. | System sustains continuous Lake Erie HAB imaging and downlink across all four seasonal quarters. | Not Run |
| **TC-015** | Single integrated 3U CubeSat flight element verification (Happy Path). Traces to L1-MIS-015. | 1. Inspect integrated HABSat-1 avionics, payload, ADCS, power, and comms architecture. | Single 3U CubeSat flight element performs all collection, CI processing, and downlink functions. | Not Run |
| **TC-021** | US EAR and ITAR export control and research security compliance (Happy Path). Traces to L1-PRJ-021. | 1. Inspect hardware BOM, open-source software stack, and public-domain cryptography. | Zero ITAR/EAR export-restricted algorithms or unauthorized foreign dependencies exist in flight stack. | Not Run |
| **TC-026** | 3U CubeSat mechanical form-factor compliance inspection (Happy Path). Traces to L2-SYS-026. | 1. Measure integrated spacecraft structure and PC/104 avionics stack against 3U CDS gauge. | Spacecraft conforms strictly to 3U CubeSat Design Specification external dimensions. | Not Run |
| **TC-027** | Total spacecraft mass <= 6,000 grams verification (Happy Path). Traces to L2-SYS-027. | 1. Weigh integrated spacecraft and sum subsystem mass budget allocations. | Total spacecraft mass remains well below the 6,000 g maximum 3U limit. | Not Run |
| **TC-044** | 2-year orbital system lifetime reliability and memory endurance analysis (Happy Path). Traces to L2-SYS-044. | 1. Calculate NAND Flash erase cycles, MRAM endurance, and watchdog recovery margins over 2 years. | Storage wear-leveling and radiation-tolerant MRAM exceed 2-year orbital lifetime requirements with > 2x margin. | Not Run |
| **TC-053** | External subsystem testing interfaces when spacecraft is fully integrated (Happy Path). Traces to L2-SYS-053. | 1. Connect bench diagnostic harness to external umbilical port on integrated stack. | Umbilical interface provides full telemetry readout and power/communication checkout access. | Not Run |
| **TC-164** | OBC Subsystem total mass <= 250 grams verification (Happy Path). Traces to L3-OBC-164. | 1. Weigh EnduroSat OBC Type I board, RP2350 Data Processor, and storage/connector hardware on precision scale. | Total OBC Subsystem mass measures <= 250 grams. | Not Run |
| **TC-165** | OBC Subsystem 95 mm x 95 mm x 25 mm PC/104 volume envelope inspection (Happy Path). Traces to L3-OBC-165. | 1. Measure assembled OBC PC/104 board stack with calipers. | All OBC elements fit within the 95 mm x 95 mm x 25 mm volume envelope. | Not Run |
| **TC-172** | Integrated ground diagnostic and software flashing umbilical verification (Happy Path). Traces to L3-OBC-172. | 1. Connect external umbilical to JP2/JP14 headers.<br>2. Run diagnostic poll and flash test image. | Umbilical supports both real-time diagnostic commands and firmware flashing without disassembly. | Not Run |
| **TC-175** | On-orbit telecommand reconfiguration of thresholds and algorithm coefficients (Happy Path). Traces to L3-OBC-175. | 1. Uplink parameter update command modifying Min SoC threshold from 20% to 25%.<br>2. Verify pass pre-check. | Parameter table updates in MRAM; pass sequencer immediately enforces the new 25% SoC threshold. | Not Run |
| **TC-176** | On-orbit flight software image upload, verification, and installation (Happy Path). Traces to L3-OBC-176. | 1. Uplink chunked flight software patch over UHF.<br>2. Verify signature/CRC and install image. | OBC stages binary in NVM, verifies signature and CRC, boots updated firmware, and confirms operation. | Not Run |
| **TC-256** | Automated off-target hardware-mocked SITL unit test suite >= 80% coverage (Happy Path). Traces to L4-OBC-256. | 1. Execute GTest / F' STest and PyTest hardware-mocked suite in GitHub Actions CI.<br>2. Check lcov report. | 100% of unit/integration tests pass with >= 80% statement coverage (achieving > 90% target) without physical hardware. | Not Run |
| **TC-264** | Non-volatile MRAM parameter table individual update and default restore (Edge Case). Traces to L4-OBC-264. | 1. Update 3 timeout parameters in MRAM via telecommand, then inject out-of-range parameter, then issue restore-defaults command. | Valid updates persist in MRAM; out-of-range value is rejected; restore command resets all parameters to factory defaults. | Not Run |
| **TC-265** | Chunked flight software binary staging and missing segment index reporting (Edge Case). Traces to L4-OBC-265. | 1. Uplink a 64-chunk software binary while intentionally dropping chunks #18 and #42. | OBC assembles received chunks in staging NVM and transmits NACK report listing missing segment indices #18 and #42. | Not Run |
| **TC-266** | Staged software bad signature rejection and 24-hour unconfirmed rollback to golden image (Failure Condition). Traces to L4-OBC-266, EC-67. | 1. Attempt install of staged image with invalid signature (rejected).<br>2. Install valid image but withhold ground confirmation for 24 hours. | Corrupted signature is rejected prior to install; unconfirmed new image automatically rolls back to golden image at 24.0 hours. | Not Run |
| **TC-267** | External wired serial diagnostic interface command injection and pre-launch check (Happy Path). Traces to L4-OBC-267. | 1. Connect serial console to JP2/JP14 diagnostic UART.<br>2. Inject checkout command and read pre-launch flags. | OBC streams real-time telemetry, executes diagnostic command, and confirms clean pre-launch state over wired serial link. | Not Run |
| **TC-268** | External SWD/JTAG umbilical reflashing of Main Computer and Data Processor (Happy Path). Traces to L4-OBC-268. | 1. Connect programmer to external umbilical SWD/JTAG lines on integrated stack.<br>2. Reflash STM32F407VG and RP2350. | Both Main Computer and Data Processor flash and verify cleanly over umbilical lines without mechanical disassembly. | Not Run |
| **TC-301** | Economic budget and existing EnduroSat OBC Type I hardware utilization audit (Happy Path). Traces to CON-01. | 1. Audit project hardware procurement ledger and avionics bill of materials. | Flight software deploys on existing club-owned EnduroSat OBC Type I and RP2350 hardware at $0 net hardware cost. | Not Run |
| **TC-302** | 100% open-source flight and ground software toolchain verification (Happy Path). Traces to CON-02. | 1. Inspect software licenses across FreeRTOS, NASA F', ARM GCC, CMake, GTest, Python, and SQLite. | All flight and ground tools use permissive open-source licenses (Apache 2.0, MIT, BSD, GPLv3 w/ exception) with zero proprietary software. | Not Run |
| **TC-303** | Aerospace industry Preliminary Design Review (PDR) artifact completeness check (Happy Path). Traces to CON-03. | 1. Verify L0–L4 requirements, D0–D2 diagrams, ADRs 001–004, 80-item edge-case catalog, and 182-case traceability matrix. | All PDR deliverables are complete, internally consistent, and approved for industry board review. | Not Run |
| **TC-305** | Aerospace software engineering practices enforcement (PR approvals, CI gates) (Failure Condition). Traces to CON-05. | 1. Attempt direct push to `main` branch and open a PR with a failing GTest unit test in GitHub repository. | Branch protection blocks direct push and blocks PR merge until unit tests pass and 1 peer approval is recorded. | Not Run |

---

## Test Environment

### Hardware, Software, Data, and Configuration Specifications

* **Hardware Setup:**
  * **Main Computer:** STM32F7 ARM Cortex-M7 Microcontroller Dev Board (128 MHz, 512 KB SRAM, 2 MB Internal Flash).
  * **Data Processor:** RP2350 Board running specialized matrix math operations.
  * **Non-Volatile Storage:** 1 GB SPI NAND Flash (Science Data Buffer) + 4 MB SPI MRAM (Configuration & Key Storage).
  * **Bus Interfaces:** Dual CAN 2.0B transceivers (1 Mbps), SPI buses (10 Mbps), UART debug interfaces.
  * **Test Instrumentation:** Saleae Logic Pro 16 Logic Analyzer, Keysight 200 MHz Digital Oscilloscope, Programmable DC Power Supply (Keysight E36313A).
* **Software Stack & Toolchains:**
  * **RTOS & Framework:** FreeRTOS + NASA JPL F' (F Prime) Flight Software Framework.
  * **Static Analysis & Testing:** cppcheck, Ruff, Pyrefly, GTest/GMock C++ Framework, Python 3.14+ PyTest Automation Harness.
  * **Ground Station Emulator:** Python-based ground station script connected to SQLite database for telemetry logging.
* **Seeded Test Data Sets:**
  * **Multispectral Test Images:** 50 synthetic 4-band image arrays (1280 x 960 resolution at 620 nm, 650 nm, 680 nm, 708 nm) representing varying algal bloom densities across Lake Erie.
  * **Orbital State Vectors:** NORAD Two-Line Element (TLE) sets representing a 500 km Sun-Synchronous Orbit (SSO).
  * **Cryptographic Test Vectors:** Pre-generated ASCON-AEAD128 keypairs, valid nonces, and mutated ciphertext packets for security testing.
* **Simulated Network & RF Link Conditions:**
  * **UHF Command Link:** FSK uplink with simulated noise injection.
  * **S-Band Downlink:** High-speed downlink stream with packet drop simulation.

### Environment Tier Definitions

1. **Development Environment (SITL):** Developer workstations running QEMU hardware emulators and native x86 GCC unit test binaries. Used for rapid code-build-test loops, static analysis, and algorithm unit testing.
2. **Staging Environment (HITL Bench):** Flat-sat bench top setup consisting of target STM32 microcontrollers, SPI NAND/MRAM boards, CAN bus analyzers, and signal generators. Used for integration, IPC, timing, and fault recovery testing.
3. **Pilot Environment (Integrated Spacecraft Stack):** Fully integrated PC/104 flight stack inside cleanroom enclosure, connected via RF attenuators to actual UHF/S-Band ground station transceivers. Used for final acceptance and flight simulation.

---

## Pass and Fail Criteria

### Individual Test Level Criteria

* **PASS Condition:** An individual test case is declared PASS if and only if all of the following conditions are met:
  1. The test execution completes without throwing unhandled exceptions, task deadlocks, or kernel panics.
  2. All expected output values, state transitions, telemetry flags, and returned error codes strictly match the defined Expected Result criteria.
  3. Execution timing parameters fall strictly within the thresholds defined in Section 3 (e.g. command validation latency < 50 ms, fault handling < 100 ms).
  4. Zero dynamic heap memory allocations occur during test execution post-initialization.
* **FAIL Condition:** A test case is declared FAIL if any assertion fails, output values exceed tolerances, timeouts occur, memory leaks are detected, unexpected reboots trigger, or incorrect command ACKs are returned.

### Overall Plan Level Criteria

* **Overall Plan PASS Threshold:** The Test Plan as a whole is declared SUCCESSFUL when:
  1. 100% of mandatory ('shall' / Must) L0–L4 requirements pass all corresponding unit, integration, and system test cases.
  2. Zero open Class 1 (Critical System Panic / Reboot) or Class 2 (Data Corruption / Loss) defects remain in the project bug tracker.
  3. Full compliance with regulatory safety constraints is demonstrated (100% pass on 45-minute post-launch RF inhibit).
  4. Formal review approval is granted by Project Advisor Dr. Hawkins and the UC CubeCats review board.
* **Overall Plan FAIL Threshold:** The Test Plan is declared FAILED if any mandatory requirement fails its test suite without an approved engineering waiver, or if unresolved critical defects remain.

---

## Table of Milestone, Test Activity, Owner, and Evidence

| Milestone & Target Date | Test Activity & Layer | Target Scope & Requirements | Owner | Verification Evidence Output |
| :--- | :--- | :--- | :--- | :--- |
| **Power Interaction Prototype Software**<br>(Jan 29, 2027) | Layer 1 & 2: SPI Polling, Time-to-Empty Alg, Watchdog Petting & EPS Fault Isolation Tests | L2-SYS-046, L2-SYS-048, L3-OBC-138, L4-OBC-222, Task 012–016 | Caden O'Leary | PyTest execution logs, oscilloscope trace of hardware watchdog pin strobing, SPI timing benchmarks. |
| **Comms Interaction Prototype Software**<br>(Feb 08, 2027) | Layer 1 & 2: ASCON-128 Decryption, Authentication Tag Check, UHF/S-Band Streaming & Replay Protection | L3-OBC-129, L3-OBC-130, L4-OBC-185–192, Task 007–011, 024 | Elmoataz Abdellah | Security test suite report, ASCON latency log, UART packet capture PCAP files. |
| **Payload Interaction Prototype Software**<br>(Mar 01, 2027) | Layer 1 & 2: Imager Adapter SPI Throughput, NAND Storage Buffer Management & Chlorophyll Index Computation | L1-SCI-008, L2-SYS-042, L4-OBC-244–246, Task 017–021 | Matthew Goldsberry & Seunghun Lee | Data Processor Chlorophyll Index accuracy report vs numpy reference, NAND wear-leveling log. |
| **ADCS Interaction Prototype Software**<br>(Mar 15, 2027) | Layer 2: TLE Forwarding, ECEF/LVLH Georeferencing, Ephemeris Queue & CAN Bus Mutex Tests | L1-SCI-010, L2-SYS-040, L4-OBC-218, L4-OBC-234–236, Task 006 | Elmoataz Abdellah | FreeRTOS IPC queue trace logs, CAN bus analyzer logic trace, ADCS mode transition matrix. |
| **Senior Design Expo & PDR**<br>(Spring 2027) | Layer 3 & 4: Autonomous 10-Mode Sequencer, Emergency Safe Mode Failover, HITL Ground Pass Demos | Complete L0–L4 Baseline (TC-001 through TC-252), Task 026 | Full Team (Matthew, Caden, Elmoataz, Seunghun, Kristen) | Automated System Test Suite execution summary PDF, Signed PDR Compliance Log, Advisor Sign-off Sheet. |

---

## Definition of Done

### Feature-Level Definition of Done Checklist

Before any individual flight software feature or task is marked Complete by the team, it must satisfy the following checklist:

- [ ] **Code Complete:** Feature implemented in C/C++ in accordance with CubeCats embedded coding standards.
- [ ] **Peer Reviewed:** Code pull request reviewed and approved by at least one other team member.
- [ ] **Unit Tests Passing:** Unit test cases written in GTest/PyTest and passing with >= 90% statement coverage.
- [ ] **Static Analysis Clean:** Zero warnings or errors returned by cppcheck static analysis.
- [ ] **Zero Heap Allocation:** Verified that no dynamic memory allocation (`malloc`, `new`) occurs post-initialization.
- [ ] **Traceability Linked:** Feature mapped to explicit Requirement ID (`L3-OBC-###` / `L4-OBC-###`) in code header.
- [ ] **Documentation Updated:** API comments and interface contracts documented.

### Project-Level Definition of Done Checklist

Before the overall HABSat-1 Flight Software Project is declared Complete for senior design delivery, the project must satisfy the following checklist:

- [ ] **100% Mandatory Requirement Verification:** All mandatory ('shall' / Must) L3–L4 requirements verified through passing test, demonstration, or analysis logs.
- [ ] **Prototype Software Milestones Complete:** All 4 prototype milestone deliverables (Power, Comms, Payload, ADCS) tested, demonstrated, and signed off.
- [ ] **End-to-End Pipeline Validated:** Autonomous pass execution and ground station telemetry ingestion demonstrated in pilot HITL environment.
- [ ] **Zero Open Critical Defects:** Zero unresolved Class 1 (Critical) or Class 2 (High) issues in the bug tracker.
- [ ] **Formal Sign-Off:** Signed acceptance obtained from Project Advisor Dr. Hawkins and UC CubeCats leadership.
