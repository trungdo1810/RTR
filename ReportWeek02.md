<h1 align="center">Week 02 Report</h1>

### *Intern: Do Thanh Trung*
**1. Sensors in drone**  
- **Gyroscope**: Gyro sensors, this sensor is used to provide angular motion to the drone. 3-axis gyroscope provides angular velocity in 3 axes.  
<div align='center'>
<img src = 'https://upload.wikimedia.org/wikipedia/commons/thumb/d/d5/Gyroscope_operation.gif/220px-Gyroscope_operation.gif'>
<img src = 'https://www.digikey.com/-/media/Images/Article%20Library/TechZone%20Articles/2018/January/Apply%20Sensor%20Fusion%20to%20Accelerometers%20and%20Gyroscopes/article-2018january-apply-sensor-fusion-fig6.jpg?ts=d350ad10-07ec-4e70-b139-f0805c5061be&la=en-US' >

*Gyroscope* 
</div>

- **Accelerometer**: accelerometer provides linear acceleration in 3 axes.
<div align='center'>
<img src = 'https://www.digikey.com/-/media/Images/Article%20Library/TechZone%20Articles/2018/January/Apply%20Sensor%20Fusion%20to%20Accelerometers%20and%20Gyroscopes/article-2018january-apply-sensor-fusion-fig5.jpg?ts=f896f05a-fd6f-482f-8309-1749271899e1&la=en-US'>

*Accelerometer* 
</div>

- **Barometer**: Barometers are sensors that measure air pressure. In drones, this air pressure information is used to determine the drone’s altitude.
- **Rangefinder**: There are different types of rangefinders found in drones but all of them perform a simple task: to determine how far away from the ground the drone is
- **GPS and other satellite positioning systems**: This drone sensor type uses satellite launched around the Earth to determine specific geographic locations.
- **Magnetometer**: In cases where determining the drone’s heading using only GPS location is not appropriate, a drone needs to have a magnetometer. A magnetometer measures the strength and direction of a magnetic field. Using this principle, a drone can always determine the direction of the magnetic North and adjust its trajectory accordingly.
- **Distance Sensor**: These type of sensors are used to sense the obstacles. The distance sensors are based on ultrasonic, laser or LIDAR.
- **Optical Flow Sensor, Beacons, Wheel Encoders, Visual Odometry...**

>Sensor Fusion Approach 

When used independently from each other, the raw readings from the accelerometer and gyro are not reliable. The gyro measures angular rotations and, unlike the accelerometer, is hardly affected by external forces. However, the gyro tends to drift from its mean value in the long run. Sensor fusion combines the sensor data from different sources to reduce their uncertainty and improve the overall quality of any individual series of readings.  
- Inertial navigation system (INS): includes gyro, magnetometer, accelerometer, and GPS. It will fuse all those sensors together to give a robust navigation output.  
- Inertial Measurement Unit (IMU): gyro, accelerometer, and magnetometer. IMU just outputs raw data without navigation.
- Attitude Heading Reference System (AHRS): An IMU + GPS. It doesn't include a Kalman filter, so AHRS would be a good fit for people that already have a custom filter or want more sensor data.

**2. Kalman filter** 

Kalman filtering is an algorithm that provides estimates of some unknown variables given the measurements observed over time. Kalman filters have been demonstrating its usefulness in various applications. Kalman filters have relatively simple form and require small computational power. However, it is still not easy for people who are not familiar with estimation theory to understand and implement the Kalman filters.


Ardupilot uses digital signal processing filters in its INS:
Extended Kalman filter (EKF) and Discrete Cosine Matrix (DCM)

DCM was the first method used by Ardupilot. Currently, EKF3(version3) is the primary filter and predictor.
DCM directly uses GPS updates, EKF is a predictive filter anf fuses multiple sensor sources

INNOVATION
The EKF constantly makes predictions of position/velocity/attitude based on past input and compares them to present measurements. Is the prediction is different than measured, an INNOVATION occurs. If the difference is not too great, the measurement is used, on weighted basis. Large innovation for too long will cause the EKF to reject the sensor or declare that its "lost" 

Lane Switch and Fallback to DCM
If the innovations are too great for too long, the EKF will switch to a redundant sensor, if available, or ultimately fall back to using DCM(Plane/Rover only) which allows "dead reckoning" even without a GPS. The EKF provides greater accuracy and eliminates noise and the effect of turbulence on position and attitude estimates and it provides compensation for acceleration during turns to the AHRS to provide accurate attitude information. It will even "learn" compass offsets and IMU biases if slightly different than original calibration