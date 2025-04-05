# microbit-project

  
Table of Content

1.0	Introduction -------------------------------------------------------------------------------- 2
2.0 System Design ------------------------------------------------------------------------------ 2
3.0 Implementation ---------------------------------------------------------------------------- 3
	3.1 Prerequisites ----------------------------------------------------------------------- 3
	3.2 Radio Configuration ------------------------------------------------------------- 3
	3.3 Sender Workflow ----------------------------------------------------------------- 3
	3.4 Receiver Workflow --------------------------------------------------------------- 3
4.0 Conclusion ---------------------------------------------------------------------------------- 4
5.0 References ---------------------------------------------------------------------------------- 4 
1.0 Introduction
Micro:Bit devices are commonly used in IoT and educational settings, making secure communication essential to prevent unauthorized access and ensure data integrity. This project implements a lightweight encryption and authentication system to protect command communication between two Micro:Bit devices. It utilizes AES encryption and cryptographic hashing (including MD5 and a unique identifier) to provide confidentiality, integrity, and authentication. The protocol also incorporates random salts to enhance security while remaining suitable for constrained environments, enabling secure command transmission and execution between a transmitter and receiver.
 
Figure 1: Project Report Details
The transmitter encrypts and sends commands based on user input, while the receiver decrypts and executes the commands securely.
2.0 System Design
Commands are encrypted utilizing the Advanced Encryption Standard (AES). The encrypted commands, along with randomly generated salts, are transmitted to the recipient for the purposes of decryption and subsequent execution.
  
Figure 2: System Design Architecture
The receiver interprets commands to display environmental data or control external LEDs.
3.0 Implementation
3.1 Prerequisites
The repository for codal-microbit-v2 was cloned. Furthermore, md5.h, md5.cpp, sha256.h, and sha256.cpp were added to the libraries/codal-microbit-v2 directory. 
3.2 Radio Configuration
The microbitConfig.h file was modified to increase the maximum packet size as follows:  
#define MICROBIT_RADIO_MAX_PACKET_SIZE 240
This helps in accommodating more message bandwidth over the transmission line.
3.3 Sender Workflow
Press Button A to increment the counter and show the updated count on the LED matrix. Press Button B to generate a random salt, derive the Data Protection Key (DPK) using the salt and shared secret, encrypt the counter value with AES, transmit the encrypted command and salt via radio, and display "SENT" on the LED matrix. Button A increment is initialized at Zero once the message is sent over the radio. 
3.4	Receiver Workflow
It receives the encrypted command and the salt through the radio. It then regenerates the DPK using the received salt and the shared secret, thereafter, it decrypts using AES. The Decrypted message does one of the following: 
1.	Display the temperature on the LED matrix. If the temperature is too hot, the fan cools it down.
 
Figure 1: Working Fan
2. Display the accelerometer data. 
 
Figure 2: Accelerometer counting the steps
3. Control external LEDs in a traffic-light sequence. 
 
Figure 3: Traffic Light
If the command is invalid, display an error message.
Logs were monitored using the screen command. 
screen /dev/ttyACM0 115200


4.0 Conclusion
This project highlights secure command communication for Micro:bit devices through lightweight cryptographic techniques. The combination of MD5, SHA256, and AES offers robust security while effectively addressing the Micro: bit's resource constraints. By encrypting commands and verifying their integrity, this system presents a practical solution for secure IoT communication.


5.0 References
