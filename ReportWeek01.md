<h1 align="center">Week 01 Report</h1>

### *Intern: Do Thanh Trung*

### **1. Drone motor and ESC**  
**1.1. Select motor**  
Things to consider when choosing drone motors:  
1. Weight of your drone  
2. Efficiency  
3. Power  
4. Torque

Types of motors:
There are 2 types of motors used in drones: brushed and brushless motors.
<div align="center">
<img src = 'https://dronenodes.com/wp-content/uploads/2018/10/brushless-motor-vs-brushed-motor.png' width="80%" height="80%">
</div>

| Type           | Definition  | Application | Lifespan | Energy saving |
| -----------    | ----------- | ----------- | -------- | ------------- |
| Brushed DC motor| Brushed DC motors possess a rotating armature that works like a electromagnet . A rotary switch is connected that helps to reverse current direction for every half cycle so that poles can be pushed or pulled against permanent magnets connected outside motor.       | Commonly used for drones. | It can serve users up to 1000 hours | Maintenance for carbon crushes to ensure proper energy consumption and satisfactory operation 
| Brushless DC motor | 	Brushless DC Motors do not possess brushes, they just have a permanent magnet and it switched with electronic polarity changes. Its movements can be controlled via a dedicated electronic controller and speed feedback mechanism.        | Commonly used for drones that demand higher rotation speeds to manage flights. | work effectively up to more than 1000 hours | Brusheless motors are highly energy efficient as compared to brushed ones.

>If the motor is expected to be used for very less time, it is recommended to connect brushed DC motor as it will provide sufficient output with cost effectiveness. But in case if you need motors continuously or when your device is going to work on higher power rating then brushless motor will be best idea for long hour flights.

- BLDC motor:  
A BLDC motor consist of two main parts, a stator and a rotor.  
<div align='center'>
<img src = 'https://howtomechatronics.com/wp-content/uploads/2019/02/Brushless-motor-main-parts-a-stator-and-a-rotor.png?ezimgfmt=rs:352x270/rscb2/ng:webp/ngcb2'>
</div>

<center> Brushless DC Motor Working Principle </center>
<div align = 'center'>
<img src='https://sklc-tinymce-2021.s3.amazonaws.com/comp/2021/03/mceclip11_1614687945.gif' width="50%" height="50%" >
</div>

**1.2. Electronic Speed Controller(ESC):**  
An ESC controls the brushless motor movement or speed by activating the appropriate MOSFETs to create the rotating magnetic field so that the motor rotates.  
The battery supplies direct current, while the brushless motor accepts three-phase alternating current.
<div align = 'center'>
<img src = 'https://i.dronemanya.com/%D1%81%D1%85%D0%B5%D0%BC%D0%B0-%D0%BF%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D1%8F-%D1%80%D0%B5%D0%B3%D1%83%D0%BB%D1%8F%D1%82%D0%BE%D1%80%D0%BE%D0%B2-%D0%BD%D0%B0%D0%BF%D1%80%D1%8F%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F-%D0%BA-%D0%91%D0%9A-%D0%BC%D0%BE%D1%82%D0%BE%D1%80%D0%B0%D0%BC-a932f.jpeg' > 
</div>

### **2. ESC Protocols:**  
      
ESC Protocols is the “language” that the flight controllers and ESC use to communicate, one of the most basic task is to tell how fast the motor should be spinning.
<br/>The Oneshot, Multishot and Dshot are the ESC calibration protocols.This protocol allows connecting Electronic speed controllers (ESC) to flight controller.  
<br/>**Analog PWM**  
0% duty cycle means STOP and 100% duty cycle means FULL POWER.

<br/>**Standard PWM**  
If pulse length is 1ms then STOP and when pulse length is 2ms then FULL POWER.  
The maximum frequency: 500Hz.  
The signal delay is 2ms.

<p align = 'center'> <b>Problem with PWM </b></p> 

- Unsynced output  
- Limited updated rate (frequency)  

<div align='center'>
<img src='image/PWM_problem.png' alt = 'PWM_problem'>
</div>

<br/>**Oneshot**  
- Oneshot125:  
Combination of SyncPWM and FastPWM
>>- SyncPWM: the exact moment the PID loop output a new value
>>- FastPWM: Standard PWM is speed up 8x, new pulse length is 125-250µs, refresh rate up to 4 kHz
- Oneshot42:  
Oneshot42 is 3 times faster than Oneshot125 with a maximum frequency of 12 kHz, signal delay of 42µs.

<br/>**Multishot**  
This is the fastest ESC protocol among all the above with a maximum frequency of 32 kHz. It is 10 times faster than Oneshot125. This is not a widely supported protocol because of a limited number of Multishot ESCs..

<br/>**Dshot (Digitalshot)**  
Standard PWM, Oneshot125, Oneshot42, and Multishot these are all analog signals. They all rely on the length of the electrical pulse to determine the value being sent.  

The Dshot is itself a digital signal so it’s exciting to know that ESC calibration will no longer be necessary. Because of the nature of the digital signal, which is one’s and zero’s, it will also be much more resistant to electrical noise.  

A DShot data packet consists of a total of 16 bits: 11 bits for throttle value (211 = 2048 steps), 1 bit for telemetry request and 4 bit for CRC checksum (cyclic redundancy check).

There are 4 different Dshot protocol types:
1. DShot1200 ESC - 1200Kbits/Sec.  
2. DShot600 ESC - 600Kbits/Sec.  
3. DShot300 ESC - 300Kbits/Sec.  
4. DShot150 ESC - 150Kbits/Sec.    

<div align='center'>
<img src='https://oscarliang.com/ctt/uploads/2016/11/esc-protocol-speed-comparison-hz.jpg' alt = 'Speed Comparison'>
</div>

### **3. PID control**

