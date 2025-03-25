<details>
<summary> <h1> Task - 1 Documentation </h1> </summary>
<br>
  
## <ins> Step 1 - Understanding the Verilog code: </ins>
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

## <ins> Step 2 - Creating a PCF File: </ins>
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

## <ins> Step 3: Integrating with the VSDSquadron FPGA Mini Board: </ins>
### Integration steps:
- First I connected the board to the computer through an USB Cable.
- Then I created 3 folders named red_led, green_led, blue_led for glowing Red, Green, Blue LED respectively. In each of these folders, I included Makefiles, top.v code and .pcf files named as 'Pin_assignments.pcf'.
- Then I opened terminal and coded as below.
  
 <ins> Code for Glowing Red LED: </ins>
  ![red 1](https://github.com/user-attachments/assets/6e17810d-4594-492a-b783-2320578594b5)
  ![red 2](https://github.com/user-attachments/assets/cd41e617-1238-4011-bb76-d9a33ba12680)
 <ins> As expected, Red LED started glowing as below: </ins>
  
  ![Red output](https://github.com/user-attachments/assets/75c73a8d-71ab-4162-9d15-331e8975f59a)

<ins> Code for Glowing Green LED: </ins>
  ![green 1](https://github.com/user-attachments/assets/fe0f391a-7ca0-4ee1-a25b-dcc4f10c8087)
  ![green 2](https://github.com/user-attachments/assets/67b79cd0-4580-496c-b7d7-d70997914e4f)
<ins> As expected, Green LED started glowing as below: </ins>
  
  ![Green output](https://github.com/user-attachments/assets/97f215ee-ec1d-40be-8c28-971bdeb95f15)

<ins> Code for Glowing Blue LED: </ins>
  ![blue 1](https://github.com/user-attachments/assets/231ef76b-ea3a-481a-a89d-ddf08c6adb7c)
  ![blue 2](https://github.com/user-attachments/assets/d489ee0c-7282-47f1-b731-89f46a2c9b9e)

<ins> As expected, Blue LED started glowing as below: </ins>
  
  ![Blue output](https://github.com/user-attachments/assets/f358ed8f-064b-4d53-8ff5-148c7d32b106)
## <ins> My Understandings: </ins>
While doing this task, I learnt how commands like 'make clean', 'make build' and 'sudo make fash' run. First when we enter 'make clean' command, the previous code which we have executed will erase from the Memory. The 'make build' command will convert the verilog code into series of binaries and creates a netlist. The 'sudo make flash' command flashes the data to the external RAM and executes the program.
## <ins> Challenges Faced and Implemented Solutions: </ins>
- The main challenge which I faced was connecting the Board to the Virtual Machine. At last, I solved the problem by installing the Virtual box extension and by 
 reinstalling Virtual Box.
- I found it a little dificult to understand the code and the function of commands like 'make clean','make build' and 'sudo make flash'. I resolved this problem with the help of my parents and a website named 'Blackbox.ai'.
-  The first time when I was trying to make the blue led glow, I didn't know what are the files needed to include in a folder to execute the program. Then I observed the files which was present in the 'blink_led' folder and included the files which are necessary in a new folder and named it as blue_led. I followed the same steps for glowing red and green led also.
</details>
