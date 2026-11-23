# AI-Based Assistive Spatial Memory and Guidance System for Visually Impaired Users

## Overview

The AI-Based Assistive Spatial Memory and Guidance System is designed to improve independent mobility and environmental awareness for visually impaired individuals.

The system uses computer vision, artificial intelligence, and voice interaction to identify objects, detect obstacles, recognize familiar people, and provide audio-based guidance.

Unlike conventional object detection systems that only identify objects in the current camera frame, this project introduces **Spatial Memory and Contextual Recall**, which enables the system to remember previously detected objects and provide their last known location and contextual information when requested by the user.

## Key Features

- **Real-Time Object Detection:** Identifies objects in the user's surroundings using YOLO.
- **Voice-Assisted Navigation:** Provides audio guidance through voice interaction.
- **Obstacle Detection:** Identifies nearby obstacles and communicates their direction, such as left, right, or front.
- **Face Recognition:** Recognizes familiar individuals.
- **Add Person:** Allows users to register and store information about familiar people.
- **Spatial Memory:** Stores information about previously detected objects.
- **Contextual Recall:** Retrieves the last known location, detection time, and description of an object when it is not visible in the current frame.
- **Voice-Based Interaction:** Enables users to interact with the system through spoken commands.

## Technology Stack

- **Programming Language:** Python
- **Computer Vision:** OpenCV
- **Object Detection:** YOLO
- **Face Recognition:** Face Recognition / Computer Vision
- **Speech Interaction:** Speech Recognition and Text-to-Speech
- **AI & Machine Learning:** Object Detection and Image Processing

## How It Works

1. The camera captures the user's surroundings.
2. The YOLO model detects objects in real time.
3. The system identifies obstacles and provides directional voice guidance.
4. Detected objects are stored in spatial memory along with their contextual information.
5. When the user asks for an object, the system first checks the current camera frame.
6. If the object is not currently visible, the system retrieves its previously stored information, including its last known position and detection time.
7. The system communicates the information through voice output.

## Project Innovation

The major contribution of this project is the integration of **Spatial Memory and Contextual Recall** into an AI-based assistive navigation system.

For example, if a user asks, "Where is my laptop?" and the laptop is not visible in the current camera frame, the system can retrieve its previously recorded location and the time it was last detected.

This provides additional environmental context beyond conventional real-time object detection.

## Project Objective

To develop an intelligent, voice-assisted system that enhances environmental awareness and supports greater independence for visually impaired individuals through real-time object detection, navigation assistance, and contextual memory.

## Future Enhancements

- Integration with a mobile application.
- Improved object-location tracking.
- More accurate spatial mapping and indoor navigation.
- Integration with wearable assistive devices.
- Enhanced contextual understanding using AI models.

## Project Type

Final Year Engineering Project – Information Science and Engineering.
