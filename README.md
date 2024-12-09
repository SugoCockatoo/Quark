QUARK ROBOT  
Made by Sugo  

 ![Logo](https://github.com/SugoCockatoo/Quark/blob/main/Quark%20Large%20Logo.png)


Project Overview: 
Quark is an AI-powered robotic system designed to perform real-time object detection using the YOLOv11 model. While such advanced models are typically reserved for powerful computing systems, Quark brings this state-of-the-art AI technology to the embedded domain, leveraging the capabilities of the ESP32 S3 microcontroller. The project is designed to demonstrate how machine learning, specifically convolutional neural networks (CNNs) and object detection algorithms like YOLOv11, can be effectively deployed on low-cost, low-power devices for robotics applications. 

This project serves as an excellent case study for learning about AI, object detection, robotic control, and how these technologies integrate in a resource-constrained environment. With a low-cost, compact design and sophisticated AI capabilities, Quark allows users to understand how embedded AI systems function and how to optimize such systems to perform complex tasks on a budget. 


Technical Overview: 
Quark operates on the ESP32 S3 board, equipped with the necessary hardware for performing inference on machine learning models such as YOLOv11. The system utilizes MicroPython for software, while the TensorFlow Lite machine learning model is employed for real-time object detection. The model, a 16-bit float TensorFlow Lite version, has been specially optimized for embedded use, making it suitable for a device with the memory and computational limitations of the ESP32. 

 

Machine Learning Model: 
At the heart of Quark's object detection ability lies the YOLOv11 model, a modern, state-of-the-art model for real-time object detection. YOLO, which stands for You Only Look Once, represents a departure from earlier slower, region-based detection systems. YOLO performs object detection by dividing the image into a grid and predicting bounding boxes, object class probabilities, and confidence scores in one forward pass. This is in stark contrast to methods that scan regions of the image sequentially. 

Neural Network Architecture (YOLOv11): 
YOLOv11 employs a convolutional neural network (CNN) architecture. CNNs are a class of deep learning models that are particularly well-suited for image-related tasks. CNNs work by applying filters (or convolutional layers) to an image, which allows them to capture spatial hierarchies of features. These features could range from simple edges in the first layers to more complex object parts in deeper layers. 
Convolutional Layers: These layers perform convolutions on the input image, capturing basic features such as edges, textures, and shapes. 
Pooling Layers: These layers reduce the dimensionality of the image, maintaining only the most important features while reducing computational complexity. 
Fully Connected Layers: At the final stage, fully connected layers combine the extracted features to make predictions on the image, such as object classes, bounding box coordinates, and confidence scores. 
The YOLOv11 model is specifically optimized for embedded systems through techniques such as quantization (reducing the precision of numbers used in computations) and pruning (removing less important parts of the model), both of which help decrease the model size and increase inference speed without significantly impacting performance. 

Object Detection Process (YOLOv11 Workflow): 
Preprocessing: The input image is resized and normalized before being fed into the model. Resizing ensures that the image fits the input dimensions expected by the model (usually 416x416 or 320x320). 
Grid Division: YOLO divides the image into a grid of cells, and each cell predicts bounding boxes and class labels for objects located within the cell. 
Bounding Boxes and Class Labels: Each grid cell predicts multiple bounding boxes, classifying them by the object it contains, along with a confidence score. The bounding boxes are ranked based on their confidence levels. 
Post-Processing: The raw output of YOLO is processed using Non-Maximum Suppression (NMS), which eliminates redundant boxes and keeps only the ones with the highest confidence. 
Key Features of YOLOv11: 
High Speed and Accuracy: YOLOv11 achieves a balance of real-time object detection with high accuracy, making it ideal for robotic applications like Quark, where both speed and precision are paramount. 
Optimized for Embedded Systems: YOLOv11 has been adapted for deployment on systems like the ESP32 by reducing model size through quantization and pruning techniques, making it feasible to run on hardware with limited processing power and memory. 

 

Movement Control and Linear Regression for Quark: 
In addition to object detection, Quark’s movement system is driven by a linear regression model, which has been trained to control the robot's servos based on object position and environmental context. This model allows Quark to move its body (pitch, yaw, and roll) to track objects detected in the camera’s field of view. 

Machine Learning Model for Movement: 
A linear regression algorithm was implemented to translate object positions into servo movements. Linear regression is a supervised learning algorithm that establishes a linear relationship between input features (such as the bounding box coordinates of detected objects) and target outputs (such as servo positions). 
Inputs: The main inputs to the linear regression model are the coordinates of the object in the camera’s frame, typically x and y values representing the position of the object within the image. 
Outputs: The outputs are the servo angles for pitch, yaw, and roll movements, which determine how Quark’s head or body should move to align the object at the center of the frame. 
The regression model is trained on data collected during various interactions, with the robot’s movements being recorded and correlated with the object’s position in the image. By using mean squared error (MSE) as a loss function, the model is optimized to minimize the error between predicted and actual servo positions. 

Movement Logic: 
Centering Objects: Based on the detected bounding box of an object, the robot moves its servos to center the object in the camera’s field of view. If an object is detected to the left of the image, Quark moves its head or body right to align the object centrally. 
Object Tracking: As the object moves, the regression model continuously updates the servo commands to keep the object centered. The movement is fluid and responsive, allowing Quark to track moving objects dynamically. 
Behavior Modes: The movement is also linked to Quark’s behavior modes, such as Pet Me Mode or Dance Mode, where the robot may perform predefined actions or gestures based on the interaction. 

 

Behavior Modes and Interactive Feedback: 

Quark’s behavior modes define how the robot responds to various environmental stimuli, enriching the user experience and showcasing the robot’s ability to interact in a lifelike manner. These modes include: 
Pet Me Mode: Quark reacts to human touch or proximity, moving its head and activating its RGB LEDs to show affection. The robot enters a calm state, where it uses soft, inviting colors like blue and green. 
Dance Mode: In this mode, Quark can perform synchronized movements to music or specific commands, with RGB LEDs pulsing in sync with the music, creating a dynamic and interactive environment. 
Sleep Mode: When inactive or when repetitive objects are detected, Quark enters Sleep Mode, reducing energy consumption and conserving power by minimizing unnecessary movements and dimming its LEDs. 
Emotions: Sometimes, Quark can be more happy, more curious and can have behaviour, just as you
Emotional Expression Mode: By using the RGB LEDs, Quark can express emotional states. For instance, it may light up in soft, calming colors when it detects familiar objects or more intense colors when it’s excited. 

 

RGB LEDs: 
The RGB LEDs serve as a visual feedback mechanism and play an essential role in Quark's emotional interaction system. Each behavior mode or state of the robot is indicated by different colors: 
Green or Blue: Quark is calm or in Pet Me Mode. 
Red or Yellow: Quark is alert, detecting a new object, or in Emotional Expression Mode. 
These LEDs provide an intuitive way for users to understand Quark’s status or mood based on its color patterns, enhancing the robot’s interactive qualities. 

 
Futuristic Case Design and Cooling System: 
Quark’s case is designed with both aesthetics and functionality in mind. Its 3D-printed casing ensures lightweight yet durable protection for the internal components, while ventilation slots and heat sinks ensure the robot does not overheat during extended operation. 
To maintain optimal performance, especially during intensive AI processing tasks, a cooling fan is integrated to manage the heat generated by the ESP32 and other components. The fan operates dynamically, activating during high-load operations, such as object detection and regression calculations. 

 
Camera and AI Vision: 
The camera module serves as Quark’s “eyes,” capturing real-time video to be processed by the YOLOv11 object detection model. The camera is a low-cost ESP32-CAM module, which is sufficient for the robot’s purpose of real-time object detection, despite its small size and limited processing power. 
The AI vision system, powered by YOLOv11, enables Quark to perform real-time object detection with high speed and accuracy, identifying and classifying objects in its environment. The camera provides the necessary input for both object detection and movement control, forming the core of the robot’s interaction capabilities. 


Conclusion: 

Quark represents an advanced example of how AI-based object detection, machine learning models for movement, and interactive behavior modes can be implemented in a low-cost, embedded robotics system. Using YOLOv11 for object detection, coupled with a linear regression model for servo control, Quark can dynamically interact with its environment and users. Its efficient use of limited resources and real-time processing capabilities demonstrates the potential for running complex AI algorithms on microcontrollers, showcasing the future of robotics and AI-powered systems. 
