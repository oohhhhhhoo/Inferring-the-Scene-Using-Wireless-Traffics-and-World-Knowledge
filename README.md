# Inferring-the-Scene-Using-Wireless-Traffics-and-World-Knowledge
## Goal: use traffic info from sensors to indicate some of human activities
1. If FOSCAM camera can infer the number of people in a single room.
### Steps
1. Identify the connection between packets traffic for camera and human motion
   ![image](https://github.com/user-attachments/assets/1198b501-2a46-45af-a3b0-5a7d8f57b7e6)
  Test for total 40s swithcing between static and move for every 10s.
2. Identify the FOSCAM camera use IPB method(H.264) to send messages
   R4 Manuals: https://www.foscam.com/Uploads/usermanual/2020-05-29/User%20Manual%20for%20R2%20R4%20User%20Manual%20V2.5_English.pdf
   ![image](https://github.com/user-attachments/assets/a76f29a3-2201-4104-aa8c-b9351a8fe09e)
   ![image](https://github.com/user-attachments/assets/fb24b5d0-c716-4e6e-a067-4bae05302b61)
3. Clearify how FOSCAM transport H.264 in traffic package.
4. Find what kind of info from FOSCAM can be used to infer the number of people in the room. Begin it in a small sofa and two working people.
## Essays:
1. https://www.usenix.org/conference/usenixsecurity21/presentation/singh
  · H.264 Image Compression-Using 3 key frame-types
2. https://www.usenix.org/conference/usenixsecurity22/presentation/sharma-rahul
3. https://dl.acm.org/doi/abs/10.1145/3580890

## knowledge
### 802.11b
1. https://www.cnblogs.com/rougungun/p/14340489.html

### H.264 IPB frames
1. I frames(Intra-coded picture) hold complete image information
2. P frames(Predicted picture) only contain changes in the image from previous frames
3. B frames(Bi-directionally predicted pictures) can construct the image from wither direction using either changes from the I or P frames before them, changes from I and P frames after them, or interpolation between the I/P frames before and after them.

### test result
1. keep static for first 20s, then moving object for 20s, without motion detection
   <img width="1678" alt="image" src="https://github.com/user-attachments/assets/a19e45c2-c7a9-4787-879b-d80f5f6d4b10">
2. keep static for first 20s, then moving object for 20s, with motion detection
<img width="1678" alt="image" src="https://github.com/user-attachments/assets/6ce04627-a3f7-4d68-b56a-3dbd7b4a21db">
3. remain silent for 20s, sending control signal for 20s
   <img width="1678" alt="image" src="https://github.com/user-attachments/assets/13899a1c-eb1c-46ad-ab2c-bcd4cc1a66f0">


