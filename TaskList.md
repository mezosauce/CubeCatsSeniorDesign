
1. Design the static memory buffer allocation scheme for the pyld_data and imgr_data queues on the Main Computer. (Matthew Goldsberry)

2. Integrate an On-Orbit Flight Software Reprogrammability if Main Computer’s main mission operations ever corrupts on Main Computer (Seunghun Lee).

3. Develop the core active_task chlorophyll index computation algorithm for the Data Processor module. (Matthew Goldsberry)

4. Document the API contract and error handling responses for passing health_status from the Data Processor to the Main Computer. (Matthew Goldsberry)

5. Validate the inter-component CAN bus communication latency between the Data Processor and the Main Computer. (Matthew Goldsberry)

6. Research the I2C mutex locks needed for the ADCS Computer to prevent bus collisions during attitude sensor reads. (Elmoataz Abdellah)

7. Specify the exact 12-byte packet structure for sending adcs_data (including pos_x, pos_y, and pos_z) from the ADCS Computer to the Main Computer. (Elmoataz Abdellah)

8. Simulate a setting for the development environment to run isolated unit tests on Main Computer’s communication with other subsystem components (Elmoataz Abdellah).


9. Develop the F Prime Svc::TlmChan configuration to channelize the vel_x, vel_y, and vel_z attributes within the ADCS Computer. (Elmoataz Abdellah)

10. Refine the faults handling logic for the ADCS Computer to correctly flag sensor dropouts to the Main Computer without triggering a full system reset. (Elmoataz Abdellah)

11. Test the command ingestion pipeline routing goal_pos_y and goal_pos_z targets from the Main Computer to the ADCS Computer. (Elmoataz Abdellah)

12. Investigate the SPI polling rate required for the Main Computer to accurately read the Power Computer's charge_percentage and voltage attributes. (Caden O'Leary)

13. Design the time_to_empty estimation algorithm to run iteratively on the Power Computer. (Caden O'Leary)

14. Document the state transitions and recovery steps for the faults attribute within the Power Computer module. (Caden O'Leary)

15. Develop the hardware watchdog petting sequence between the Power Computer and the Main Computer's health_status buffer. (Caden O'Leary)

16. Validate the power subsystem's fault isolation logic, ensuring the Power Computer properly updates its time_stamp during transient voltage spikes. (Caden O'Leary)

17. Research the maximum SPI bus throughput for writing truth_imgr_data from the Imager Adapter to the Main Computer. (Seunghun Lee)

18. Specify the byte alignment and frame dimensions for the multi_imgr_data frames outputted by the Imager Adapter. (Seunghun Lee)

19. Design the circular buffer mechanism to accurately track packets_processed inside the Data Storage module. (Seunghun Lee)

20. Develop the file chunking and active_mode flagging logic for the Data Storage component to prepare files for downlink. (Seunghun Lee)

21. Test the temp and health_status reporting mechanisms of the Data Storage unit under simulated high-I/O read/write loads. (Seunghun Lee)

22. Obtain the required SQLite ORM libraries and setup the ground station database to receive pwr_data telemetry from the Main Computer. (Elmoataz Abdellah)

23. Specify the JSON schemas for the Ground Station API to exactly match the adcs_data and imgr_data structures buffered on the Main Computer. (Kristen Griessman)

24. Ensure security through Encryption, Decryption, and Authentication of packets by the Main Computer to and from the Ground Station. (Elmoatatz Abdellah)

25. Refine the Ground Station packet decoding logic to handle fragmented pyld_data transmissions stored in the Data Storage module. (Caden O’leary)

26. Validate the end-to-end data pipeline from the Main Computer's buffer to the Ground Station's database during a simulated pass execution. (Kristen Griessman)

27. Test the inter-process communication serialization between the Main Computer and Data Processor modules under maximum telemetry load. (Matthew Goldsberry)
