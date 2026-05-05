# DachshundSense: A TinyML-Based Wearable System for Dog Behaviour Classification 

Edge Impuse project:

## Introduction

DachshundSense is a low-cost wearable system that uses embedded machine learning (TinyML) to classify dog behaviour in real time. Built around an Arduino Nano 33 BLE Sense mounted on a dog’s collar, the device collects motion sensor data to identify three key behaviours: walking, sitting, and lying down. The project demonstrates how meaningful behavioural insights can be derived without the need for cameras, cloud computing, or high-power hardware (Kularni, 2024).

The inspiration for this project comes from owning a reactive dachshund in a city apartment, where space constraints and long working hours can make it difficult to monitor a dog’s wellbeing (Adamson, 2011). As dachshunds grow in popularity in urban environments, their energetic and sometimes anxious nature(Adamson, 2011) highlights the need for simple monitoring solutions that help owners understand their pets’ behaviour, particularly when left alone.

This project is influenced by existing activity trackers but adopts a more lightweight approach, addressing the challenge of whether accurate behaviour classification can be achieved using limited computational resources. Comparable studies using wearable IMU sensors have reported similar results for similar behaviour classes, suggesting that the performance achieved in this project is consistent with existing research (Kurlarni, 2024).

## Research Question

How effectively can embedded TinyML systems classify dachshund behaviour using real-time IMU sensor data?


## Application Overview

The system follows a modular TinyML architecture consisting of three connected building blocks: sensing, model development, and embedded inference.

In the sensing stage, an Arduino Nano 33 BLE Sense collects tri-axial accelerometer and gyroscope data via its onboard IMU (Lara & Labrador, 2013). The board is powered through a USB connection to a computer during development or alternatively could be powered via a battery or power bank. Sensor data is streamed to Edge Impulse for labelling and storage.

The second stage involves preprocessing and training within Edge Impulse. Raw IMU data is transformed into spectral features, and a neural network is trained to classify behaviours under embedded constraints.

In the final stage, the trained model is deployed back onto the Arduino, enabling real-time, on-device inference with outputs transmitted via serial or BLE. 


## Data
Describe what data sources you have used and any cleaning, wrangling or organising you have done. Including some examples of the data helps others understand what you have been working with.

*Tip: probably ~200 words and images of what the data 'looks like' are good!*

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
