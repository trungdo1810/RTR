<h1 align="center">Week 1 Report</h1>

### *Thực tập sinh: Đỗ Thành Trung*

1. Drone motor and ESC  
    1.1. Select motor  
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

If the motor is expected to be used for very less time, it is recommended to connect brushed DC motor as it will provide sufficient output with cost effectiveness. But in case if you need motors continuously or when your device is going to work on higher power rating then brushless motor will be best idea for long hour flights.

- BLDC motor:  
A BLDC motor consist of two main parts, a stator and a rotor.  
<div align='center'>
<img src = 'https://howtomechatronics.com/wp-content/uploads/2019/02/Brushless-motor-main-parts-a-stator-and-a-rotor.png?ezimgfmt=rs:352x270/rscb2/ng:webp/ngcb2'>
</div>

<center> Brushless DC Motor Working Principle </center>
<div align = 'center'>
<img src='https://sklc-tinymce-2021.s3.amazonaws.com/comp/2021/03/mceclip11_1614687945.gif' width="50%" height="50%" >
</div>

>> Hall sensor  
    Hall sensor provides the information to synchronize stator armature excitation with rotor position. Since the commutation of BLDC motor is controlled electronically, the stator windings should be energized in sequence in order to rotate the motor. Before energizing a particular stator winding, acknowledgment of rotor position is necessary. So the Hall Effect sensor embedded in stator senses the rotor position.



1.2. ESC:

Bộ điều khiển tốc độ(ESC) có nhiệm vụ là truyền năng lượng từ pin đến động cơ không chổi than. Nhu cầu sử dụng chúng nảy sinh do một số tính năng của động cơ BLDC. Tóm lại, pin cung cấp dòng điện một chiều, trong khi động cơ không chổi than chấp nhận dòng điện xoay chiều ba pha.
![ESC](https://i.dronemanya.com/%D1%81%D1%85%D0%B5%D0%BC%D0%B0-%D0%BF%D0%BE%D0%B4%D0%BA%D0%BB%D1%8E%D1%87%D0%B5%D0%BD%D0%B8%D1%8F-%D1%80%D0%B5%D0%B3%D1%83%D0%BB%D1%8F%D1%82%D0%BE%D1%80%D0%BE%D0%B2-%D0%BD%D0%B0%D0%BF%D1%80%D1%8F%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F-%D0%BA-%D0%91%D0%9A-%D0%BC%D0%BE%D1%82%D0%BE%D1%80%D0%B0%D0%BC-a932f.jpeg) 

2. ESC Protocols:
        
    Giao thức hiệu chuẩn ESC là “ngôn ngữ” mà bộ điều khiển chuyến bay và ESC sử dụng để giao tiếp, một trong những nhiệm vụ cơ bản nhất là cho biết động cơ quay nhanh như thế nào. 
    <br/>Oneshot, Multishot và Dshot là các giao thức hiệu chuẩn ESC. Giao thức này cho phép kết nối Bộ điều khiển tốc độ điện tử (ESC) với bộ điều khiển bay.  
    <br/>**Analog PWM**  
    0% duty cycle thì STOP and 100% duty cycle thì FULL POWER.

    <br/>**Standard PWM**  
    Nếu độ dài xung là 1ms thì STOP và khi độ dài xung là 2ms thì FULL POWER. Do đó tần số tối đa là 500Hz

    ![PWM_problem](image/PWM_pr.png)
    <br/>**Oneshot**
    - Oneshot125:  
    Kết hợp của SyncPWM và FastPWM
    >>- SyncPWM: thời điểm chính xác khi PID loop xuất ra output và không bị "trôi" tín hiệu.  
    >>- FastPWM: Standard PWM được tăng tốc lên 8 lần, nghĩa là độ dài xung mới là 125-250µs, tần số tối đa là 4 kHz
    - Oneshot42:  
    Nhanh hơn 3 lần so với Oneshot125 với tần số tối đa là 12 kHz và độ trễ tín hiệu là 42µs.

    <br/>**Multishot**  
    Đây là giao thức ESC nhanh nhất trong số tất cả các giao thức trên với tần số tối đa là 32 kHz. Nó nhanh hơn 10 lần so với Oneshot125. Đây không phải là một giao thức được hỗ trợ rộng rãi vì một số ESC Multishot có hạn.

    <br/>**Dshot**  
    Standard PWM, Oneshot125, Oneshot42 và Multishot, tất cả đều là tín hiệu analog. Tất cả đều dựa vào độ dài của xung điện để xác định giá trị được gửi đi.

    Dshot là một tín hiệu digital nên việc hiệu chuẩn ESC sẽ không còn cần thiết nữa. Do bản chất của tín hiệu kỹ thuật số là tín hiệu số một và số không, nên tín hiệu này cũng sẽ có khả năng chống nhiễu điện cao hơn nhiều.

    Các loại giao thức Dshot:
    1. DShot1200 ESC - 1200Kbits/Sec.  
    2. DShot600 ESC – 600Kbits/Sec.  
    3. DShot300 ESC – 300Kbits/Sec.  
    4. DShot150 ESC – 150Kbits/Sec.    

    ![Speed Comparison](https://oscarliang.com/ctt/uploads/2016/11/esc-protocol-speed-comparison-hz.jpg)
3. PID control

