![images](https://github.com/user-attachments/assets/a6e22a90-a895-4119-9775-e3375795449f)
# VSDSquadron-FPGA-Mini
## Task - 2 ##
**Step -1 Study the Existing Code**

The files given to us can be accessed from here- https://github.com/thesourcerer8/VSDSquadron_FM/tree/main/uart_loopback

Overview

The uart_loopback project in the VSDSquadron_FM repository implements a UART (Universal Asynchronous Receiver-Transmitter) loopback system. The loopback mechanism sends received data back to the transmitter without modification.

This functionality is implemented in two main Verilog files:

*top.v* - The top-level module integrating UART communication, clock management, and RGB LED status indicators.

 *uart_trx.v* - The UART transmitter and receiver module that handles serial communication.

**Understanding Loopback in top.v**

1. Module Declaration

   The top module defines inputs and outputs for UART and LED indicators. The main signals involved are - the system clock, active-low reset, UART receive and transmit pins, and an RGB      LED output for status indication.

2. Internal Oscillator and Clock Management

    An internal oscillator generates a stable clock signal used for UART operations. A frequency divider reduces the high-frequency clock to a lower frequency suitable for serial             communication.

3. UART Loopback Logic

    The core loopback functionality is implemented using an instance of the UART transmitter and receiver module. The received data is directly assigned as the transmit data, ensuring        that any data received is immediately sent back. Transmission is triggered whenever new data is received, completing the loopback process.

4. Visual Feedback with RGB LED

   The first three bits of the received UART data control an RGB LED. This provides a visual indication of incoming data, helping to verify UART activity.

**Understanding uart_trx.v (UART Transmission & Reception)**

1. UART Transmitter

   The transmitter takes parallel data and converts it into a serial data stream. It includes a start bit, 8-bit data, and a stop bit. A shift register is used to send one bit at a time.

2. UART Receiver

   The receiver detects the start bit and shifts in the incoming serial data. Once all bits are received, the data is stored and marked as available for processing. This allows the          received data to be looped back to the transmitter.

   **Conclusion**
  
   The loopback mechanism ensures that any data sent to the FPGA via UART is echoed back to the sender. Additionally, the first three bits of received data are displayed on an RGB LED       for visual confirmation.

  **Step -2 Visual Desription**
  
   A block diagram illustrating the UART loopback architecture
   
   ![Image](https://github.com/user-attachments/assets/7bf3f3f8-b1bf-4c3d-a794-7cf7822c7e11)

   The key components of the block diagram are -
   
1. Clock – Generates a system clock signal for synchronization.
  
2. UART Receiver – Receives serial data (RX) and converts it into parallel format.

3. Loopback Block – Directly connects the received data to the transmitter, ensuring the same data is sent back.

4. UART Transmitter – Converts parallel data back into serial format and transmits it (TX).

5. RGB LED – Displays the first three bits of the received data as a visual indication of UART activity.

6. Arrows – Indicate the direction of data flow from RX to Receiver, through the Loopback Block, to the Transmitter, and out as TX. The LED is connected to the Receiver for visual feedback.
   
   
   
