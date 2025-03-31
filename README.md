<details>
<summary> <h1> <ins> Task - 1 Documentation </ins> </h1> </summary>
<br>

<details>
<summary> <h2> <ins> Objective: </ins> </h2> </summary>
<br>

To understand and document the provided Verilog code, create the necessary PCF file, and integrate the design with the VSDSquadron FPGA Mini board using the provided datasheet.
</details>
  
<details>
<summary> <h2> <ins> Step 1 - Understanding the Verilog code: </ins> </h2> </summary>
<br>
  
The purpose of the provided Verilog module is to control an RGB LED (<ins>R</ins>ed <ins>G</ins>reen <ins>B</ins>lue - <ins>L</ins>ight <ins>E</ins>mitting <ins>D</ins>iode) using an internal hardware oscillator and a frequency counter.
### Module Declaration:
- led_red - Output - Red LED Output
- led_green - Output - Green LED Output
- led_blue - Output - Blue LED Otput
- hw_clk - Input - Hardware Clock Input
- testwire - Output - Test Signal or Wire
### Internal Oscillator:
This instantiates a high-frequency oscillator (SB_HFOSC) with a division factor of 2 (CLKHF_DIV ("0b10")). The oscillator is powered up (CLKHFPU(1'b1)) and enabled (CLKHFEN(1'b1)), producing a clock signal on int_osc.
### RGB Driver Instantiation:
This instantiates an RGB driver (SB_RGBA_DRV) that controls the RGB LED. The RGBLEDEN signal enables the LED driver. The RGB0PWM, RGB1PWM, and RGB2PWM signals control the pulse-width modulation (PWM) for the red, green, and blue channels, respectively. In this case, the blue channel is enabled, while the red and green channels are set to off.
### RGB Driver Parameters:
These parameters set the current levels for each color channel of the RGB LED. Each channel is set to a low current level.
### Internal Signals:
int_osc: A wire that will carry the output of the internal oscillator.
frequency_counter_i: A 28-bit register used to count clock cycles.
### Frequency Counter:
This always block increments the frequency_counter_i on the rising edge of the int_osc signal. This effectively counts the number of clock cycles from the internal oscillator.
### Test Wire Assignment:
The testwire is assigned the value of the 6th bit of the frequency_counter_i, which can be used for debugging or monitoring the counter's state.
</details>
  
<details>
<summary> <h2> <ins> Step 2 - Creating a PCF File: </ins> </h2> </summary>
<br>
  
It is noticed that the pin assignment in the pcf file given in the repository is different from the pin assignment in datasheet.
### Pin assignments mentioned in the given repository:
- led_red = Pin 39
- led_blue = Pin 40
- led_green = Pin 41
- hw_clk = Pin 20
- testwire = Pin 17
### Corrected Pin Assignment:
- led_red = Pin 39
- led_green = Pin 40
- led_blue = Pin 41
- hw_clk = Pin 20
- testwire = Pin 17
### Pin Mapping:
![image](https://github.com/user-attachments/assets/f221ac4b-996b-4af2-8d8c-da28a6f13616)
</details>

<details>
<summary> <h2> <ins> Step 3 - Integrating with the VSDSquadron FPGA Mini Board: </ins> </h2> </summary>
<br>
  
- First I connected the board to the computer through an USB Cable.
- Then I created 3 folders named red_led, green_led, blue_led for glowing Red, Green, Blue LED respectively. In each of these folders, I included Makefiles, top.v code and .pcf files named as 'Pin_assignments.pcf'.
- Then I opened terminal and coded as below.
  
 ### <ins> Code for Glowing Red LED: </ins>
  ![red 1](https://github.com/user-attachments/assets/6e17810d-4594-492a-b783-2320578594b5)
  ![red 2](https://github.com/user-attachments/assets/cd41e617-1238-4011-bb76-d9a33ba12680)
 <ins> As expected, Red LED started glowing as below: </ins>
  
  ![Red output](https://github.com/user-attachments/assets/75c73a8d-71ab-4162-9d15-331e8975f59a)

### <ins> Code for Glowing Green LED: </ins>
  ![green 1](https://github.com/user-attachments/assets/fe0f391a-7ca0-4ee1-a25b-dcc4f10c8087)
  ![green 2](https://github.com/user-attachments/assets/67b79cd0-4580-496c-b7d7-d70997914e4f)
<ins> As expected, Green LED started glowing as below: </ins>
  
  ![Green output](https://github.com/user-attachments/assets/97f215ee-ec1d-40be-8c28-971bdeb95f15)

### <ins> Code for Glowing Blue LED: </ins>
  ![blue 1](https://github.com/user-attachments/assets/231ef76b-ea3a-481a-a89d-ddf08c6adb7c)
  ![blue 2](https://github.com/user-attachments/assets/d489ee0c-7282-47f1-b731-89f46a2c9b9e)

<ins> As expected, Blue LED started glowing as below: </ins>
  
  ![Blue output](https://github.com/user-attachments/assets/f358ed8f-064b-4d53-8ff5-148c7d32b106)
</details>

<details>
<summary> <h2> <ins> My Understandings: </ins> </h2> </summary>
<br>
  
While doing this task, I learnt how commands like 'make clean', 'make build' and 'sudo make fash' run. First when we enter 'make clean' command, the previous code which we have executed will erase from the Memory. The 'make build' command will convert the verilog code into series of binaries and creates a netlist. The 'sudo make flash' command flashes the data to the external RAM and executes the program.
</details>

<details>
<summary> <h2> <ins> Challenges Faced and Implemented Solutions: </ins> </h2> </summary>
<br>
  
- The main challenge which I faced was connecting the Board to the Virtual Machine. At last, I solved the problem by installing the Virtual box extension and by 
 reinstalling Virtual Box.
- I found it a little dificult to understand the code and the function of commands like 'make clean','make build' and 'sudo make flash'. I resolved this problem with the help of my parents and a website named 'Blackbox.ai'.
-  The first time when I was trying to make the blue led glow, I didn't know what are the files needed to include in a folder to execute the program. Then I observed the files which was present in the 'blink_led' folder and included the files which are necessary in a new folder and named it as blue_led. I followed the same steps for glowing red and green led also.
</details>
</details>

<details>
<summary> <h1> <ins> Task - 2 Documentation </ins> </h1> </summary>
<br>

<details>
<summary> <h2> <ins> Objective: </ins> </h2> </summary>
<br>

Implement a UART loopback mechanism where transmitted data is immediately received back, facilitating testing of UART functionality.
</details>
  
<details>
<summary> <h2> <ins> Study the Existing Code: </ins> </h2> </summary>
<br>
  
## Explaination of uart_trx code:
This code describes a simple UART (Universal Asynchronous Receiver-Transmitter) transmitter module in Verilog, which is designed to send 8-bit data with no parity and one stop bit (8N1 format).
### Module Declaration:
Module Name: uart_tx_8n1 indicates that this is a UART transmitter module.
Inputs:
- clk: The clock signal used to synchronize the transmission.
- txbyte: The 8-bit data byte to be transmitted.
- senddata: A signal that triggers the transmission when asserted (set to 1).
Outputs:
- txdone: A signal that indicates when the transmission of the byte is complete.
- tx: The actual transmission line where the data is sent.
### Parameters:
These parameters define the different states of the state machine used in the UART transmission process:
- STATE_IDLE: The idle state where the transmitter is not sending data.
- STATE_STARTTX: The state where the start bit is being sent.
- STATE_TXING: The state where the data bits are being sent.
- STATE_TXDONE: The state indicating that the transmission is complete.
### State Variables:
- state: Holds the current state of the state machine.
- buf_tx: A buffer to hold the byte to be transmitted.
- bits_sent: A counter to keep track of how many bits have been sent.
- txbit: The current value of the transmission line (starts high).
- txdone: Indicates whether the transmission is complete.
### Wiring:
This line connects the txbit register to the tx output wire, so whatever value txbit holds will be sent out on the tx line.
### Always Block:
This block is triggered on the rising edge of the clock signal, meaning that all operations inside this block will occur synchronously with the clock.
### State Machine Logic:
- #### Start Sending:
If senddata is asserted and the state is STATE_IDLE, the module transitions to STATE_STARTTX, loads the byte to be transmitted into buf_tx, and resets txdone.
- #### Idle State:
In the idle state, the txbit is set high (indicating the line is idle).
- #### Start Bit Transmission:
When in the STATE_STARTTX, the txbit is set low to indicate the start of transmission, and the state transitions to STATE_TXING.
- #### Data Bit Transmission:
In the STATE_TXING, the least significant bit of buf_tx is sent out on tx, the buffer is shifted right to prepare the next bit, and the bits_sent counter is incremented.
- #### Stop Bit Transmission:
After sending 8 data bits, the stop bit (high) is transmitted, signaling the end of the data frame.
## Explaination of top.v code:
The provided Verilog code describes a hardware module named top, which integrates several functionalities including UART transmission, RGB LED control, and clock generation. Below is a detailed explanation of the code:
### Module Declaration:
The top module has four output wires for controlling RGB LEDs and one output for UART transmission. It also has one input for the hardware clock.
### Internal Signals:
- int_osc is a wire that will receive the output from an internal oscillator.
- frequency_counter_i is a 28-bit register used to keep track of the frequency for LED control and UART transmission.
### Clock Generation for 9600 Hz:
- clk_9600 is a register that will toggle to create a 9600 Hz clock signal.
- cntr_9600 is a counter that increments with each clock cycle to help generate the 9600 Hz clock.
- period_9600 is a constant that defines how many cycles of the internal oscillator are needed to create a 9600 Hz clock.
### UART Transmission:
This line instantiates a UART transmission module named DanUART. It uses the 9600 Hz clock (clk_9600), sends the byte "D", and triggers transmission based on the 25th bit of frequency_counter_i.
### Internal Oscillator:
This instantiates a high-frequency oscillator (SB_HFOSC) that generates a clock signal (int_osc). The parameters configure the oscillator to be enabled and powered.
### Frequency Counter and Clock Generation Logic:
- This always block is triggered on the rising edge of the internal oscillator clock (int_osc).
- It increments the frequency_counter_i and the cntr_9600.
- When cntr_9600 reaches the defined period_9600, it toggles the clk_9600 signal and resets the counter.
### RGB LED Driver:
- This instantiates an RGB LED driver (SB_RGBA_DRV) that controls the color of the RGB LEDs based on the bits of frequency_counter_i.
- The PWM signals for each color (red, green, blue) are derived from combinations of bits from frequency_counter_i.
### RGB Driver Current Configuration:
These lines set the current levels for each of the RGB channels to a specific value, ensuring that the LEDs operate within safe limits.
</details>

<details>
<summary> <h2> <ins> Design Documentation: </ins> </h2> </summary>
<br>
  
### Block Diagram:
![Block Diagram](https://github.com/user-attachments/assets/59ff96a4-ae40-4e7a-824f-3de0c6cdba20)
### Circuit Diagram:
![Circuit diagram](https://github.com/user-attachments/assets/7fb25ab7-9a5d-4bd4-9971-81ab403579f9)
</details>

<details>
<summary> <h2> <ins> Testing and Verification: </ins> </h2> </summary>
<br>
  
### - Photo
![Output](https://github.com/user-attachments/assets/cf125dfd-0a91-478c-936e-c45fe26d0d63)
### - Video
https://github.com/user-attachments/assets/b0973070-cec0-4b05-a292-ee91c37f0d13
</details>
</details>

<details>
<summary> <h1> <ins> Task - 3 Documentation </ins> </h1> </summary>
<br>

<details>
<summary> <h2> <ins> Objective: </ins> </h2> </summary>
<br>

To develop a UART transmitter module capable of sending serial data from the FPGA to an external device.
</details>

<details>
<summary> <h2> <ins> Study the Existing Code: </ins> </h2> </summary>
<br>
  
## Explaination of top.v code:
This code is a Verilog module for a digital design that includes a UART transmitter and an RGB LED driver.
### Module Declaration:
The top module has the following ports:
Outputs:
- led_red, led_blue, led_green: These are the outputs for the RGB LED.
- uarttx: This is the UART transmission pin.
Input:
- hw_clk: This is the hardware clock input.
### Internal Signals:
- int_osc: A wire that will be used to connect to an internal oscillator.
- frequency_counter_i: A 28-bit register used to count clock cycles for generating different frequencies.
### Clock Generation:
- clk_9600: A register that will hold the generated 9600 Hz clock signal.
- cntr_9600: A 32-bit counter used to count clock cycles to generate the 9600 Hz clock.
- period_9600: A parameter that defines the number of clock cycles needed to toggle clk_9600 to achieve a frequency of 9600 Hz.
### UART Transmission:
This line instantiates a UART transmitter module named DanUART. It takes the 9600 Hz clock (clk_9600), sends the byte "D", and uses the 25th bit of frequency_counter_i to determine when to send the data. The transmitted data is output on the uarttx pin.
### Internal Oscillator:
This instantiates a high-frequency oscillator (SB_HFOSC) that generates a clock signal (int_osc). The parameters configure the oscillator to be powered on and enabled.
### Frequency Counter and Clock Division:
This always block is triggered on the rising edge of the internal oscillator clock (int_osc). It increments the frequency_counter_i and the cntr_9600. When cntr_9600 reaches the defined period_9600, it toggles the clk_9600 signal and resets the counter.
### RGB LED Driver:
- This section instantiates an RGB LED driver (SB_RGBA_DRV) that controls the color of the LED based on the PWM signals generated from the frequency_counter_i. The PWM signals are derived from specific bits of the counter, allowing for different colors to be displayed on the RGB LED.
- The CURREN signal enables the current for the RGB driver, and the defparam statements set the current levels for each color channel.
## Explaination of uart_trx code:
This code describes a simple UART (Universal Asynchronous Receiver-Transmitter) transmitter module in Verilog, which is designed to send 8-bit data with no parity and one stop bit (8N1 format).
### Module Declaration:
Module Name: uart_tx_8n1 indicates that this is a UART transmitter module.
Inputs:
- clk: The clock signal used to synchronize the transmission.
- txbyte: The 8-bit data byte to be transmitted.
- senddata: A signal that triggers the transmission when asserted (set to 1).
Outputs:
- txdone: A signal that indicates when the transmission of the byte is complete.
- tx: The actual transmission line where the data is sent.
### Parameters:
These parameters define the different states of the state machine used in the UART transmission process:
- STATE_IDLE: The idle state where the transmitter is not sending data.
- STATE_STARTTX: The state where the start bit is being sent.
- STATE_TXING: The state where the data bits are being sent.
- STATE_TXDONE: The state indicating that the transmission is complete.
### State Variables:
- state: Holds the current state of the state machine.
- buf_tx: A buffer to hold the byte to be transmitted.
- bits_sent: A counter to keep track of how many bits have been sent.
- txbit: The current value of the transmission line (starts high).
- txdone: Indicates whether the transmission is complete.
### Wiring:
This line connects the txbit register to the tx output wire, so whatever value txbit holds will be sent out on the tx line.
### Always Block:
This block is triggered on the rising edge of the clock signal, meaning that all operations inside this block will occur synchronously with the clock.
### State Machine Logic:
- #### Start Sending:
If senddata is asserted and the state is STATE_IDLE, the module transitions to STATE_STARTTX, loads the byte to be transmitted into buf_tx, and resets txdone.
- #### Idle State:
In the idle state, the txbit is set high (indicating the line is idle).
- #### Start Bit Transmission:
When in the STATE_STARTTX, the txbit is set low to indicate the start of transmission, and the state transitions to STATE_TXING.
- #### Data Bit Transmission:
In the STATE_TXING, the least significant bit of buf_tx is sent out on tx, the buffer is shifted right to prepare the next bit, and the bits_sent counter is incremented.
- #### Stop Bit Transmission:
After sending 8 data bits, the stop bit (high) is transmitted, signaling the end of the data frame.
</details>

<details>
<summary> <h2> <ins> Design Documentation: </ins> </h2> </summary>
<br>

### Block Diagram:
![Block Diagram](https://github.com/user-attachments/assets/56588d00-9448-4460-8e89-c5ebeb5eed6b)
### Circuit Diagram:
![Circuit Diagram](https://github.com/user-attachments/assets/0f4680f9-4d9b-4ff3-a759-0d8b4482c4ff)
</details>
