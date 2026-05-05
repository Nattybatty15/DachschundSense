# DachshundSense: A TinyML-Based Wearable System for Dog Behaviour Classification 

Edge Impuse project:

## Introduction

DachshundSense is a low-cost wearable system that uses embedded machine learning (TinyML) to classify dog behaviour in real time. Built around an Arduino Nano 33 BLE Sense mounted on a dog’s collar, the device collects motion sensor data to identify three key behaviours: walking, sitting, and lying down. The project demonstrates how meaningful behavioural insights can be derived without the need for cameras, cloud computing, or high-power hardware (Kularni, 2024).

The inspiration for this project comes from owning a reactive dachshund in a city apartment, where space constraints and long working hours can make it difficult to monitor a dog’s wellbeing (Adamson, 2011). As dachshunds grow in popularity in urban environments, their energetic and sometimes anxious nature(Adamson, 2011) highlights the need for simple monitoring solutions that help owners understand their pets’ behaviour, particularly when left alone.

This project is influenced by existing activity trackers but adopts a more lightweight approach, addressing the challenge of whether accurate behaviour classification can be achieved using limited computational resources. Comparable studies using wearable IMU sensors have reported similar results for similar behaviour classes, suggesting that the performance achieved in this project is consistent with existing research (Kurlarni, 2024).
<img width="3840" height="2160" alt="8AB7A5D9-896F-4ECC-A780-7337AD5EBA93" src="https://github.com/user-attachments/assets/4acf55e7-fab5-4d82-aae1-5809988dfb2c" />
<img width="1206" height="652" alt="IMG_7064" src="https://github.com/user-attachments/assets/34af5091-9f0d-4347-880e-a03527166389" />
<img width="1206" height="948" alt="IMG_6FAA5EFB4284-1" src="https://github.com/user-attachments/assets/b4e3c421-79c6-4e9a-8fd8-604725a94441" />
**Figure 1. Visual examples of the three labelled behaviours (lying down, sitting, and walking) with the Arduino Nano 33 BLE Sense attached to the collar. The walking and lying image highlights optimal device positioning, where the sensor is securely aligned with the body, enabling more reliable and consistent motion data capture compared to less stable placements.**

## Research Question


How effectively can embedded TinyML systems classify dachshund behaviour using real-time IMU sensor data?


## Application Overview

The system follows a modular TinyML architecture consisting of three connected building blocks: sensing, model development, and embedded inference.

In the sensing stage, an Arduino Nano 33 BLE Sense collects tri-axial accelerometer and gyroscope data via its onboard IMU (Lara & Labrador, 2013). The board is powered through a USB connection to a computer during development or alternatively could be powered via a battery or power bank. Sensor data is streamed to Edge Impulse for labelling and storage.

The second stage involves preprocessing and training within Edge Impulse. Raw IMU data is transformed into spectral features, and a neural network is trained to classify behaviours under embedded constraints.

In the final stage, the trained model is deployed back onto the Arduino, enabling real-time, on-device inference with outputs transmitted via serial or BLE. 


## Data

Motion data was collected using the onboard IMU of the Arduino Nano 33 BLE Sense, capturing nine channels accX, accY, accZ, gyrX, gyrY, gyrZ, and(magX, magY, magZ (Lara & Labrador, 2013). Data was sampled at 62.5 Hz using 5-second windows. This rate was chosen because it exceeds the frequency of typical motion patterns, ensuring sufficient detail while remaining computationally efficient (Lara and Labrador, 2013) and longer data points often captured multiple behaviours due to rapid state transitions.
Three behaviours (walking, sitting, and lying down) were selected due to their feasibility for consistent data collection and their relevance to behavioural monitoring. These states provide meaningful indicators of wellbeing; for example, prolonged inactivity (lying) may indicate low energy or illness, while excessive movement (walking) can signal anxiety or restlessness (Adamson, 2011).
To ensure robustness, data was collected across varied home environments and surfaces, including beds (high/low), sofa, dog-bed, chairs, rugs, and benches. Several days were spent acclimating the dog to wearing the device build prior to data collection, ensuring behaviour was not biased by reactions to the hardware (Kumpulainen, 2018). Additional time was spent refining placement, with the sensor mounted on the upper neck region of the collar to minimise noise and maximise stability (Kulkarni, 2024). “Good posture” of collar was monitored throughout entire training process (Figure 1.) for data consistency.
The dataset was manually labelled, balanced (~100 samples per class), and split (~80/20) into training and testing sets using Edge Impulse.

## Model
This is a Deep Learning project! What model architecture did you use? Did you try different ones? Why did you choose the ones you did?

*Tip: probably ~200 words and a diagram is usually good to describe your model!*

## Experiments
What experiments did you run to test your project? What parameters did you change? How did you measure performance? Did you write any scripts to evaluate performance? Did you use any tools to evaluate performance? Do you have graphs of results? 

*Tip: probably ~300 words and graphs and tables are usually good to convey your results!*

## Results and Observations
Synthesis the main results and observations you made from building the project. Did it work perfectly? Why not? What worked and what didn't? Why? What would you do next if you had more time?  

*Tip: probably ~300 words and remember images and diagrams bring results to life!*

## Conclusion
Wrap it up, summarising key findings.

*Tip: probably ~100 words*

## Bibliography
*If you added any references then add them in here using this format:*

1. Last name, First initial. (Year published). Title. Edition. (Only include the edition if it is not the first edition) City published: Publisher, Page(s). http://google.com

2. Last name, First initial. (Year published). Title. Edition. (Only include the edition if it is not the first edition) City published: Publisher, Page(s). http://google.com

*Tip: we use [https://www.citethisforme.com](https://www.citethisforme.com) to make this task even easier.* 

----

## Declaration of Authorship

I, AUTHORS NAME HERE, confirm that the work presented in this assessment is my own. Where information has been derived from other sources, I confirm that this has been indicated in the work.


*Digitally Sign by typing your name here*

ASSESSMENT DATE

Word count: 
