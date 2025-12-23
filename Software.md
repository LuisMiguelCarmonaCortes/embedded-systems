# EMBEDDED SYSTEMS PROJECTS

## Software Tools

### OsciloPython – Low-Cost PC-Based Oscilloscope Using a Microcontroller

**OsciloPython** is a low-cost, PC-based oscilloscope designed for embedded electronics experimentation and basic signal analysis. The main goal of the project is to provide oscilloscope-like functionality using minimal hardware resources: a microcontroller with an internal Analog-to-Digital Converter (ADC) and a personal computer running Python.

In its current implementation, the system uses an **Arduino Micro** as the data acquisition unit and a **PC running a Python script** for data processing and real-time visualization.

#### System Architecture Overview

The project is divided into two main components:

- **Embedded firmware (C language)** running on the microcontroller  
- **Host-side software (Python)** running on the PC  

These two components communicate through a **UART serial interface**, making the system simple, portable, and compatible with multiple operating systems.

![System block diagram](/Blog/Images/esquema.jpg)

#### Microcontroller Side (Data Acquisition)

On the embedded side, the Arduino Micro is responsible for **sampling analog signals** using its internal ADC.

Key characteristics of the acquisition system include:

- **ADC resolution:** 10-bit (0–1023), native to the Arduino ADC  
- **Sampling method:** Polling-based acquisition  
- **Number of channels:** Up to **four independent ADC channels**  
- **Input signals:** External analog signals connected directly to ADC pins  

Each analog input voltage is converted into a digital value by the ADC. The sampled values are then formatted into a single data frame and transmitted to the PC via **UART0**.

The data is sent as a **serialized stream**, where each channel value is separated using a **semicolon (`;`) delimiter**.

This simple and human-readable protocol allows the PC software to easily parse and assign each value to its corresponding channel.

![ADC data flow](/Blog/Images/esquema.jpg)

#### PC Side (Data Reception and Visualization)

On the PC, a Python script handles serial communication, data parsing, and signal visualization.

The script performs the following tasks:

- Initializes the serial port connected to the Arduino Micro  
- Configures the communication parameters:
  - Baud rate (defined in the script)
  - 8 data bits
  - No parity
  - 1 stop bit (8N1)
- Continuously receives the incoming UART data stream  

The application is built using the following Python libraries:

- **pyserial** for serial communication  
- **numpy** for numerical data processing  
- **matplotlib** for real-time signal plotting  

Once the data is received:

- The stream is parsed using the `;` separator  
- Each value is mapped to its corresponding ADC channel  
- The signals are plotted in real time  

#### Signal Processing and Visualization Features

The Python-based visualization system provides several useful features:

- **Channel enable/disable:** Individual ADC channels can be hidden or removed from the plot  
- **Scalable axes:**
  - X-axis scaling for time expansion or compression  
  - Y-axis scaling for voltage zoom  
- **Differential measurements:** Signals can be subtracted from each other to visualize differential waveforms  
- **Multi-channel display:** All active channels can be displayed simultaneously for comparison  

These features make OsciloPython a flexible tool for debugging and analyzing low-frequency analog signals in embedded systems.

#### Project Purpose

OsciloPython is not intended to replace professional laboratory oscilloscopes, but rather to serve as:

- A learning tool for **embedded systems, ADC operation**, and **serial communication**  
- A practical example of **PC–microcontroller data acquisition and integration**  
- A low-cost alternative for basic signal visualization when laboratory equipment is unavailable  

The Python application is **cross-platform** and can run on both **Windows and Linux**, provided that Python and the required libraries are installed.

#### Future Improvements
Several improvements can be implemented to extend the capabilities of this project. A faster ADC or an ADC with higher resolution could be used to increase the sampling rate and measurement precision. 

On the PC side, additional features such as data logging, cloud-based storage, or a more user-friendly graphical interface could be implemented to enhance usability and post-processing capabilities.

[Back](index.md){: style="float: right;" }