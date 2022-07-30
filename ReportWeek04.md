<h1 align="center">Week 04 Report</h1>

## *Intern: Do Thanh Trung*
### **Target**
- Tracking algorithms
- Application of Kalman Filter in object tracking
- Demo

> ### **Tracking algorithms**  
   ### **1. Overview**    
- Object tracking is an application of deep learning where the program takes an initial set of object detections and develops a unique identification for each of the initial detections and then tracks the detected objects as they move around frames in a video.
- In other words, object tracking is the task of automatically identifying objects in a video and interpreting them as a set of trajectories with high accuracy.
<div align='center'>
    <img src = "image\car_tracking.gif" width="80%">

*Car tracking*
</div>

The difference between detecting an object and tracking:  

- **Tracking is faster than detection**: While the pre-trained classifier needs to detect an object at every frame of the video (which leads to potentially high computational loads), to utilize an object tracker we specify the bounding box of an object once and based on the data on its position, speed, and direction, the tracking process goes faster.
- **Tracking is more stable**: In cases where the tracked object is partially overlapped by another object, the detection algorithm may “lose” it, while the tracking algorithms are more robust to partial occlusion.
<div align='center'>
    <img src = "image\Object-Tracking-during-and-after-Occlusion.png">

*Object Tracking during and after Occlusion*
</div>

- **Tracking provides more information**: If we are not interested in the belonging of an object to a specific class, the tracking algorithm allows us to track the movement path of a specific object, while the detection algorithm cannot.
<div align='center'>
    <img src = "https://viso.ai/wp-content/uploads/2021/07/multiple-object-tracking.jpg" width="70%">

*Detection Algorithm vs Tracking Algorithm*
</div>

### **2. Levels of Object Tracking**  
Object tracking can be defined by two levels:

- Single Object Tracking(SOT)
- Multiple Object Tracking(MOT): it aims to track objects of multiple classes. 

### **3. Popular Object Tracking Algorithms**
- **OpenCV Object Tracking**  
    - OpenCV object tracking is a popular method because OpenCV has so many algorithms built-in that are specifically optimized for the needs and objectives of object or motion tracking.  
    - Specific Open CV object trackers include the BOOSTING, MIL, KCF, CSRT, MedianFlow, TLD, MOSSE, and GOTURN trackers. Each of these trackers is best for different goals. For example, CSRT is best when the user requires a higher object tracking accuracy and can tolerate slower FPS throughput.  
    
    >#### **BOOSTING Tracker**
    This method is based on the online version of the AdaBoost algorithm - the algorithm increases the weights of incorrectly classified objects, which allows a weak classifier to “focus” on their detection.
    - *Pros*: an object is tracked quite accurately, even though the algorithm is already outdated.
    - *Cons*: relatively low speed, strong susceptibility to noise and obstacles, and the inability to stop tracking when the object is lost.
    <div align='center'>
    <img src = "https://broutonlab.com/ghost/content/images/2021/11/BOOSTING-1.gif" width=70%>

    *BOOSTING tracker results*
    </div>

    >#### **MIL (Multiple Instance Learning) Tracker**
    This algorithm has the same approach as BOOSTING, however, instead of guessing where the tracked object is in the next frame, an approach is used in which several potentially positive objects, called a “bag”, are selected around a positive definite object. A positive “bag” contains at least one positive result.
    - *Pros*: more robust to noise, shows fairly good accuracy.
    - *Cons*: relatively low speed and the impossibility of stopping tracking when the object is lost.
    <div align='center'>
    <img src = "https://broutonlab.com/ghost/content/images/2021/11/MIL-1.gif" width=70%>

    *MIL tracker results*
    </div>

    >#### **KCF (Kernelized Correlation Filters) Tracker**
    Is a combination of two algorithms: BOOSTING and MIL. The concept of the method is that a set of images from a “bag” obtained by the MIL method has many overlapping areas. Correlation filtering applied to these areas makes it possible to track the movement of an object with high accuracy and to predict its further position.
    - *Pros*: sufficiently high speed and accuracy, stops tracking when the tracked object is lost.
    - *Cons*: inability to continue tracking after the loss of the object.
    <div align='center'>
    <img src = "https://broutonlab.com/ghost/content/images/2021/11/KCF-1.gif" width=70%>

    *KCF tracker results*
    </div>

    >#### **TLD (Tracking Learning Detection) Tracker**
    This method allows you to decompose the task of tracking an object into three processes: tracking, learning and detecting. The tracker (based on the MedianFlow tracker) tracks the object, while the detector localizes external signs and corrects the tracker if necessary. The learning part evaluates detection errors and prevents them in the future by recognizing missed or false detections.
    - *Pros*: shows relatively good results in terms of resistance to object scaling and overlapping by other objects.
    - *Cons*: rather unpredictable behavior, there is the instability of detection and tracking, constant loss of an object, tracking similar objects instead of the selected one.
    <div align='center'>
    <img src = "https://broutonlab.com/ghost/content/images/2021/11/TLD-1.gif" width=70%>

    *TLD tracker results*
    </div>

    >#### **MedianFlow Tracker**
    This algorithm is based on the Lucas-Kanade method. The algorithm tracks the movement of the object in the forward and backward directions in time and estimates the error of these trajectories, which allows the tracker to predict the further position of the object in real-time.
    - *Pros*: sufficiently high speed and tracking accuracy, if the object isn’t overlapped by other objects and the speed of its movement is not too high. The algorithm quite accurately determines the loss of the object.
    - *Cons*: high probability of object loss at high speed of its movement.
    <div align='center'>
    <img src = "https://broutonlab.com/ghost/content/images/2021/11/TLD-1.gif" width=70%>

    *MedianFlow tracker results*
    </div>

    >#### **MOSSE (Minimum Output Sum of Squared Error) tracker**
    This algorithm is based on the calculation of adaptive correlations in Fourier space. The filter minimizes the sum of squared errors between the actual correlation output and the predicted correlation output. This tracker is robust to changes in lighting, scale, pose, and non-rigid deformations of the object.
    - *Pros*: very high tracking speed, more successful in continuing tracking the object if it was lost.
    - *Cons*: high likelihood of continuing tracking if the subject is lost and does not appear in the frame.
    <div align='center'>
    <img src = "https://broutonlab.com/ghost/content/images/2021/11/MOSSE-1.gif" width=70%>

    *MOSSE tracker results*
    </div>

    >#### **CSRT (Discriminative Correlation Filter with Channel and Spatial Reliability) tracker**
    This algorithm uses spatial reliability maps for adjusting the filter support to the part of the selected region from the frame for tracking, which gives an ability to increase the search area and track non-rectangular objects. Reliability indices reflect the quality of the studied filters by channel and are used as weights for localization. Thus, using HoGs and Colornames as feature sets, the algorithm performs relatively well.
    - *Pros*: among the previous algorithms it shows comparatively better accuracy, resistance to overlapping by other objects.
    - *Cons*: sufficiently low speed, an unstable operation when the object is lost.
    <div align='center'>
    <img src = "https://broutonlab.com/ghost/content/images/2021/11/CSRT-1.gif" width=70%>

    *CSRT tracker results*
    </div>

- **DeepSORT**

    - DeepSORT is one of the most popular object tracking algorithms. It is an extension to Simple Online Real-time Tracker or SORT, which is an online-based tracking algorithm.  
    - SORT is an algorithm that uses the Kalman filter for estimating the location of the object given the previous location of the same. The Kalman filter is very effective against the occlusions.  

    - SORT comprises of three components:  
        - Detection: Detecting the object of interest in the initial stage i.  
        - Estimation: Predicting the future location i+1 of the object from the initial stage using the Kalman filter. It is worth noting that the Kalman filter just approximates the object’s new location, which needs to be optimized.  
        - Association: As the Kalman filter estimates the future location of the object i+1, it needs to be optimized using the correct position. This is usually done by detecting the position of the object in that position i+1. The problem is solved optimally using the Hungarian algorithm.
- **MDNet**
    - Multi-Domain Net is a type of object tracking algorithm which leverages large-scale data for training. Its objective is to learn vast variations and spatial relationships.  
    MDNet is trained to learn the shared representation of targets from multiple annotated videos, meaning it takes multiple annotated videos belonging to different domains. 

    - MDNet consists of pretraining and online visual tracking:
        - Pretraining: In pretraining, the network is required to learn multi-domain representation. To achieve this, the algorithm is trained on multiple annotated videos to learn representation and spatial features. 

        - Online visual tracking: Once pre-training is done, the domain-specific layers are remove,d and the network is only left with shared layers, which consist of learned representations. During the inference, a binary classification layer is added, which is trained or fine-tuned online. 
<div align='center'>
<img src = "https://assets-global.website-files.com/5d7b77b063a9066d83e1209c/61932b0ce47406badf2a6223_uCZ5q8x3JSxWn2xmCR1RWKKXU2qi1CTrnlIS2NWSnQQlXK7b1JvYkUmmuGedcxQ38ZvwmeEmbrCtlUbhXjQM4JOSRZyesl9sXu4pho8DoO8gwkCxramX5w9nDIJtouNJfvqGyHhH.png" width=70%>

*MDNet*
</div>
- **SiamMask**
    - SiamMask aims to improve the offline training procedure of the fully-convolutional Siamese network. Siamese networks take in two inputs: a cropped image and a larger search image to obtain a dense spatial feature representation. 

    - The Siamese network yields one output. It measures the similarity of two input images and determines whether or not the same objects exist in the two images. This framework is very efficient for object tracking by augmenting their loss with a binary segmentation task. 