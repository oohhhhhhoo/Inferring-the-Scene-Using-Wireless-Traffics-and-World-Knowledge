# Project Proposal

## 1. Motivation & Objective

With the rise of smart home IoT devices and low-cost wireless sensors, privacy leakage has become a significant concern. In this project, we aim to design an attack methodology that can infer human movement within a specific room by analyzing the wireless traffic from camera sensors combined with world knowledge, thereby demonstrating the serious privacy threats these wireless sensors pose to users.

## 2. State of the Art & Its Limitations

In order to figure out the risk of privacy leakage in IoT devices, there are many essays try to imitate the technological means that attackers can use to obtain the user information.
### 2.1 RF-based Localization and Tracking
In a Wi-Fi environment, it is possible to achieve coarse-grained localization of signal sources using RF receiving devices, either by actively sensing the location of entities in the area with signal transmitters or by passively sniffing RF signals to infer the position of objects. However, this kind of research can not be used in analyzing the user behavior.
### 2.2 Wireless Signal-based Human Activity Recognition
WiFi received signal strength indicator (RSSI) and Channel State Information(CSI)
has been widely used in human activity recognition combined with machine learning models. But these approaches may require an extra device to capture RSSI or CSI signals and they are trained based on a specific environment. 
### 2.3 User Behavior Analysis in IoT Devices
Some researchers access sensor data, such as app usage history or movement patterns, to analyze user behavior. However, these methods are limited because attackers cannot obtain information from encoded data. As a result, other researchers have attempted to analyze user behavior from encrypted traffic in smart home scenarios. They use a set of simple sensors, whose patterns are identified, and combine them to infer user activity. However, higher-level sensors, such as cameras, are also commonly used in users’ homes, which may offer more accurate insights.

## 3. Novelty & Rationale
### 3.1 Wi-Fi Packet-Based Approach
In our project, our method is based on how the transmission of Wi-Fi packets changes in response to the images captured by the camera sensor, which simplifies the detection process. Compared to RSSI- and CSI-based methods, detecting Wi-Fi packets requires no additional receiver other than a computer to capture the Wi-Fi traffic. According to the 802.11 protocol, we can filter packets transmitting video information, allowing us to analyze specific characteristics such as packet length and transmission frequency.


### 3.2 H.264 Camera Transmission Protocol
We use a camera as our detection sensor because it is the most commonly used sensor in cases of privacy concerns, and it exhibits a predictable pattern when transmitting data. H.264 is a widely used video compression standard that reduces file size while maintaining high video quality through techniques like motion compensation and transformation coding. As a result, the transmission rate varies depending on the video type, including static and dynamic scenarios.


### 3.3 No Wi-Fi Access Required
In a real-world scenario, an attacker cannot be guaranteed Wi-Fi access. Therefore, our project will test our method using an encrypted Wi-Fi network. We will use a laptop as a sniffer to capture Wi-Fi traffic transmitted by the camera to the router.


### 3.4 Leveraging World Knowledge
The differences in packets between different scenarios can be very subtle, so leveraging the world knowledge embedded in large language models can be a rational choice.



## 4. Potential Impact

This project captures traffic packets between cameras and routers to simulate user privacy leakage. It highlights the potential risks associated with current IoT devices and could support future efforts by manufacturers and researchers to develop stronger privacy protection technologies.
Data collected from cameras in this project can be combined with data from other sensors. Using neural networks and similar methods, this approach enables more detailed insights into user behaviors.



## 5. Challenges

The main challenges lie in identifying the correlation between changing scenarios and the variation in Wi-Fi packet characteristics. According to the H.264 protocol, the camera transmits an I-frame as the keyframe, followed by several P-frames and B-frames.
I-frames contain complete image data.\
A P-frame only includes data about changes from the previous I-frame or P-frame. It uses motion compensation to predict content based on the preceding frame. P-frames are smaller than I-frames because they only store the differences (or residuals) between frames.\
A B-frame is more complex, using both previous and future frames (either I or P) to predict its content. It leverages both past and future frame information to compress video data more efficiently. B-frames are typically smaller than both I- and P-frames.\
The camera automatically adjusts the ratio between I-frames and PB-frames to maintain a balance between high compression and video quality. Therefore, it is crucial for us to identify the signal when there is an abrupt change in video content or when an object is in constant motion.\
Although we know the camera uses H.264, the compression process is encrypted, making it act like a black box, preventing us from determining the exact compression algorithm or recovering the original data. Therefore, we must rely on extracting information and discover the transmission pattern from the characteristics of the Wi-Fi packets.




## 6. Requirements for Success

### 6.1 Detect Motion Changes in User Behavior
Our model must first accurately detect sudden motion changes in user behavior. This includes identifying transitions such as moving from static to active states, shifting from a slow pace to a faster one, and changing from small-range movements (e.g., hand gestures) to large-range movements (e.g., walking).

### 6.2 The intensity of the movement: Velocity and Range
After detecting a change in the user's movement behavior, the system further utilizes neural networks and large language models (LLMs) to conduct an in-depth analysis of the updated movement information, including details such as movement speed and range. Through neural networks, the model can more accurately assess variations in the user's speed following a change in movement state, such as a shift from slow to fast motion or from a static to an active state. Additionally, the model can analyze changes in movement range, for example, transitioning from small hand movements to larger-scale actions like walking. This detailed analysis provides a more precise understanding of the user’s behavioral patterns and state changes, enhancing the capabilities of future intelligent applications.


## 7. Metrics of Success

To evaluate the model's performance, we will employ traditional machine learning metrics, focusing on four key aspects: accuracy, precision, recall, and confidence.
* ***Accuracy***: This metric reflects the overall effectiveness of the model by measuring the proportion of correct predictions out of all predictions made. High accuracy indicates that the model consistently makes correct classifications, providing a reliable overview of its general performance across the dataset.
* ***Precision***: Precision assesses the model’s ability to correctly identify positive instances among the instances it has classified as positive. It is especially crucial in scenarios where false positives (incorrectly labeling an instance as positive) have significant consequences. A high precision score demonstrates that the model is effective at minimizing false positives.
* ***Recall***: Also known as sensitivity or true positive rate, recall measures the model’s capacity to identify all relevant instances within the dataset. It evaluates the proportion of actual positives that the model successfully detects. High recall is essential when it is critical to capture all positive cases, as it reduces the risk of missing any relevant instance.
  
By systematically evaluating the model using these metrics, we can gain a comprehensive understanding of its strengths and areas for improvement, ensuring that it meets the necessary performance standards for accurate, dependable predictions.


## 8. Execution Plan

***1.*** Identify the correlation between traffic packet flow and the target’s movement, confirming the differences in packet flow patterns across various movement modes.\
***2.*** Extract IPB-related information from the traffic flow data and analyze the relationship between the target’s movements and the IPB data.\
***3.*** Train a large language model (LLM) to take traffic flow data over a specific time period as input and output the transition times between different movement modes of the target, along with detailed movement information for each mode.



## 9. Related Work

### 9.a. Papers
Some works[2] and [3] use encrypted trafffc to analyze user behavior in smart home scenarios. And the work[1] identify a new end-to-end attack surface using IoTBeholder, a system that performs device localization, classiffcation, and user activity identiffcation, which can predict the user behavior by generating a branch of sensors’ information from traffic package.

### 9.b. Datasets

TBD
### 9.c. Software

Wireshark[4]\
Macbook wifi sniffer[5]\
Pytorch

## 10. References

1. Zou, Qingsong, et al. "Iotbeholder: A privacy snooping attack on user habitual behaviors from smart home wi-fi traffic." Proceedings of the ACM on Interactive, Mobile, Wearable and Ubiquitous Technologies 7.1 (2023): 1-26.
2. Rahmadi Trimananda, Janus Varmarken, Athina Markopoulou, and Brian Demsky. 2020. Packet-Level Signatures for Smart Home Devices. In Proceedings of 27th Annual Network and Distributed System Security Symposium, NDSS 2020, San Diego, California, USA, February 23-26, 2020. 
3. Ignacio Sanchez, Riccardo Satta, Igor Nai Fovino, Gianmarco Baldini, Gary Steri, David Shaw, and Andrea Ciardulli. 2014. Privacy leakages in Smart Home wireless technologies. In International Carnahan Conference on Security Technology, ICCST 2014, Rome, Italy, October 13-16, 2014. 1–6.
4. “Wireshark · Go Deep.” Wireshark, www.wireshark.org.
5. “Recording a Wi-Fi Packet Trace, Apple Developer Documentation.” Apple Developer Documentation, 2024, developer.apple.com/documentation/network/recording-a-wi-fi-packet-trace.
‌



