
1. Design the static memory buffer allocation scheme for the pyld_data and imgr_data queues on the Main Computer. (Matthew Goldsberry)

2. Develop the core active_task chlorophyll index computation algorithm for the Data Processor module. (Matthew Goldsberry)

3. Document the API contract and error handling responses for passing health_status from the Data Processor to the Main Computer. (Matthew Goldsberry)

4. Validate the inter-component CAN bus communication latency between the Data Processor and the Main Computer. (Matthew Goldsberry)

5. Research the I2C mutex locks needed for the ADCS Computer to prevent bus collisions during attitude sensor reads. (Elmoataz Abdellah)

6. Specify the exact 12-byte packet structure for sending adcs_data (including pos_x, pos_y, and pos_z) from the ADCS Computer to the Main Computer. (Elmoataz Abdellah)

7. Develop the F Prime Svc::TlmChan configuration to channelize the vel_x, vel_y, and vel_z attributes within the ADCS Computer. (Elmoataz Abdellah)

8. Refine the faults handling logic for the ADCS Computer to correctly flag sensor dropouts to the Main Computer without triggering a full system reset. (Elmoataz Abdellah)

9. Test the command ingestion pipeline routing goal_pos_y and goal_pos_z targets from the Main Computer to the ADCS Computer. (Elmoataz Abdellah)

10. Investigate the SPI polling rate required for the Main Computer to accurately read the Power Computer's charge_percentage and voltage attributes. (Caden O'Leary)

11. Design the time_to_empty estimation algorithm to run iteratively on the Power Computer. (Caden O'Leary)

12. Document the state transitions and recovery steps for the faults attribute within the Power Computer module. (Caden O'Leary)

13. Develop the hardware watchdog petting sequence between the Power Computer and the Main Computer's health_status buffer. (Caden O'Leary)

14. Validate the power subsystem's fault isolation logic, ensuring the Power Computer properly updates its time_stamp during transient voltage spikes. (Caden O'Leary)

15. Research the maximum SPI bus throughput for writing truth_imgr_data from the Imager Adapter to the Main Computer. (Seunghun Lee)

16. Specify the byte alignment and frame dimensions for the multi_imgr_data frames outputted by the Imager Adapter. (Seunghun Lee)

17. Design the circular buffer mechanism to accurately track packets_processed inside the Data Storage module. (Seunghun Lee)

18. Develop the file chunking and active_mode flagging logic for the Data Storage component to prepare files for downlink. (Seunghun Lee)

19. Test the temp and health_status reporting mechanisms of the Data Storage unit under simulated high-I/O read/write loads. (Seunghun Lee)

20. Obtain the required SQLite ORM libraries and setup the ground station database to receive pwr_data telemetry from the Main Computer. (Elmoataz Abdellah)

21. Specify the JSON schemas for the Ground Station API to exactly match the adcs_data and imgr_data structures buffered on the Main Computer. (Kristen Griessman)

22. Develop the React front-end dashboard to actively poll and display the health_status of the Main Computer and Power Computer. (Elmoatatz Abdellah)

23. Refine the Ground Station packet decoding logic to handle fragmented pyld_data transmissions stored in the Data Storage module. (Caden O’leary)

24. Validate the end-to-end data pipeline from the Main Computer's buffer to the Ground Station's database during a simulated pass execution. (Kristen Griessman)

25. Test the inter-process communication serialization between the Main Computer and Data Processor modules under maximum telemetry load. (Matthew Goldsberry)
