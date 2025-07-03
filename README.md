# PROPOSED CONCEPT
The principle of operation of the developed system can be divided into sequential blocks:
1. The system receives a video stream from a camera or a saved file and processes it frame by frame: each image is transmitted further to the fall detection module.
2. Fall detection detects a person in each frame and determines whether his pose is classified as "fall" or "normal".
3. Timer - performs decision-making logic based on several consecutive frames. When a fall is detected, a timer is started that tracks the duration of the fall. If the person gets up - the timer is canceled. If the timer reaches the specified time, the fall is considered dangerous and the next final block is activated.
4. Alert system - sends a message (send_telegram_alert) to the selected channel - to the medical facility staff or to one of the victim's relatives. When a long-term outage is detected, the system sends a corresponding message via a telegram bot to a pre-defined chat, and also records this incident in a separate text file (critical falls) within the project repository.



# SOFTWARE IMPLEMENTATION
One of the versions of the YOLO architecture - YOLOv8m, which belongs to the medium class (medium), was used for implementation, providing significant detection quality with relatively moderate requirements for hardware resources. 
Data processing for model training was carried out using the Roboflow tool. Image annotation was carried out using a bounding box with a class designation according to the position of the object.
![image](https://github.com/user-attachments/assets/0de0b79d-1588-4930-aa67-04af338c74e3)



# PRINCIPLE OF PROGRAM OPERATION
When launched, the program opens the downloaded video file and splits it into frames using the OpenCV library. Next, the pre-trained YOLOv8 model processes each frame and detects people in it for further determination of their pose. 
![image](https://github.com/user-attachments/assets/5d5e132f-2b32-43af-b565-394e960b0802)

After classifying the person's pose as a fall, the program automatically starts a timer for a specified amount of time to track a critical fall. 
![image](https://github.com/user-attachments/assets/cd5d134a-c146-412c-8805-b50a4bc19bcd)

If a person falls and does not get up on their own within the time specified in the timer, the system classifies the fall as critical and proceeds to the function for sending an alert. The alert system works via the Telegram API.
![image](https://github.com/user-attachments/assets/e6fd61b3-8eee-4c4b-afb9-05996cd57e82)
![image](https://github.com/user-attachments/assets/367a1ed8-6e65-4b5c-b6a5-f25b7237bcf7)
