DachshundSense: A TinyML-Based Wearable System for Dog Behaviour Classification 

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

<img width="481" height="167" alt="Screenshot 2026-05-05 at 14 49 50" src="https://github.com/user-attachments/assets/2025e5ed-e175-4849-be55-6a74c592e961" />

Figure 2. Example prediction output from Serial Monitor


## Data

Motion data was collected using the onboard IMU of the Arduino Nano 33 BLE Sense, capturing nine channels accX, accY, accZ, gyrX, gyrY, gyrZ, and(magX, magY, magZ (Lara & Labrador, 2013). Data was sampled at 62.5 Hz using 5-second windows. This rate was chosen because it exceeds the frequency of typical motion patterns, ensuring sufficient detail while remaining computationally efficient (Lara and Labrador, 2013) and longer data points often captured multiple behaviours due to rapid state transitions.
Three behaviours (walking, sitting, and lying down) were selected due to their feasibility for consistent data collection and their relevance to behavioural monitoring. These states provide meaningful indicators of wellbeing; for example, prolonged inactivity (lying) may indicate low energy or illness, while excessive movement (walking) can signal anxiety or restlessness (Adamson, 2011).
To ensure robustness, data was collected across varied home environments and surfaces, including beds (high/low), sofa, dog-bed, chairs, rugs, and benches. Several days were spent acclimating the dog to wearing the device build prior to data collection, ensuring behaviour was not biased by reactions to the hardware (Kumpulainen, 2018). Additional time was spent refining placement, with the sensor mounted on the upper neck region of the collar to minimise noise and maximise stability (Kulkarni, 2024). “Good posture” of collar was monitored throughout entire training process (Figure 1.) for data consistency.
The dataset was manually labelled, balanced (~100 samples per class), and split (~80/20) into training and testing sets using Edge Impulse.

## Model
The model was implemented using the Edge Impulse classification pipeline, combining spectral feature extraction with a fully connected neural network. Spectral analysis was selected to transform raw IMU signals into frequency-domain representations, enabling clearer separation of dynamic versus static (sitting, lying) behaviours (Muminov et al., 2022). 

The resulting feature vector (117 features) was input to a shallow dense architecture comprising two hidden layers (20 and 10 neurons). This configuration was chosen as a trade-off between representational capacity and resource constraints. Larger architectures were considered but would risk overfitting given the dataset size and exceed deployment limits for TinyML (Warden, 2019).
The initial model achieved 75% validation accuracy (loss: 0.57). The confusion matrix showed strong performance for walking, but significant misclassification between sitting and lying. This indicated insufficient feature separability for low-motion states, suggesting a need for improved data quality and additional samples (Chambers et al., 2021). The final trained Edge Impulse model was exported as an Arduino library and uploaded. During deployment, the Arduino collected live IMU data, processed it through the Edge Impulse DSP block, and produced real-time class probabilities through the Serial Monitor.



## Experiments

Two key experiments were conducted to evaluate and improve classification performance. Evaluation metrics included validation accuracy, loss, confusion matrix, precision/recall, and F1-score, all obtained from Edge Impulse.

**Experiment 1: Baseline Model**

The initial phase focused on optimising data acquisition. Sensor placement was varied (front of neck vs upper neck/back), with the front position introducing significant motion artefacts due to nametag interference and excessive contact when interacting with toys or food. The upper neck provided more stable signals and reduced noise (Marcato et al., 2023). Data collection was constrained by the need for natural behaviour, making consistent sampling difficult (Marcator et al., 2023). The baseline model achieved ~75% accuracy (loss: 0.57), but the confusion matrix revealed strong overlap between sitting and lying, indicating poor separability of low-motion classes despite clear classification of walking.

**Experiment 2: Targeted Data Collection**

Rather than increasing model complexity, further experiments prioritised improving data quality. Approximately 100 additional samples were collected (50 sitting, 30 lying, 20 walking), focusing on clearer posture representation. Model parameters (architecture, learning rate, epochs) were not modified, as the initial results suggested the limitation was data-driven rather than due to underfitting (Wang et al., 2017).
A key hypothesis was that misclassification between sitting and lying was influenced by the dachshund’s body geometry and environment. Due to their short legs and elongated torso, posture can appear similar across different surface heights (Lara & Labrador, 2013) (e.g., sitting on a sofa vs lying on the floor). To address this, additional data was collected across varied furniture heights and contexts to improve feature robustness.

Retraining improved accuracy to 77.5% (loss: 0.40). The confusion matrix shows perfect classification of walking (100%), while sitting (63.3%) and lying (72%) improved but still exhibit overlap, supported by clustering patterns in the feature space. The continued overlap between sitting and lying suggests that these classes are not well-separated in the feature space, meaning their sensor signatures are inherently similar (Muminov et al., 2022).

## Results and Observations

The system successfully demonstrated real-time embedded inference on the Arduino Nano 33 BLE Sense, showing that a low-cost TinyML pipeline can classify behaviour directly on-device. The model demonstrates strong overall performance, with a high AUC of 0.93 indicating good separability between classes. However, the weighted precision, recall, and F1 score of approximately 0.77–0.78 suggest moderate classification consistency across all behaviours. This reflects the result that walking achieved consistently high performance whilst sitting and lying down remain more difficult to distinguish, with confusion persisting even after targeted data collection.

These signals are influenced by placement, posture variation, and environmental context such as surface height (Marcato et al., 2023). For dachshunds, their body morphology further compresses the distinction between sitting and lying positions. Furthermore, the model is learning patterns that are specific to this dog’s morphology and environment, meaning it would not generalise well to other breeds (Kulkarni, 2024). A user replicating this system would need to retrain the model with data specific to their own dog.

With more time, the system could develop into a fully wearable solution with real-time predictions displayed on a mobile dashboard. The Edge Impulse model could be integrated with BLE using the ArduinoBLE library to connect directly to an application, allowing users to view live behaviour predictions and summaries (Brugarolas et al., 2016). The device could be powered by a compact 3.7V LiPo battery with appropriate voltage regulation and charging circuitry for continuous operation (FitBark, n.d.).

Another direction for future work could expand the model beyond behaviour classification to include context-aware activity recognition, such as identifying when the dog is on specific furniture (e.g., bed, chair, dog bed). This would require collecting labelled data across different surfaces and elevations (Wang et al., 2019) and could enable more insights into daily routines and resting habits.


## Conclusion

<img width="773" height="222" alt="Screenshot 2026-05-05 at 14 41 51" src="https://github.com/user-attachments/assets/b3b49774-e799-4fc9-89e8-1384fe82f440" />

**Figure 9. Side-by-side visualisation of the physical deployment and inference output. The left image displays the Arduino Nano 33 BLE Sense mounted on the dog’s collar, while the right displays real-time classification results generated by the embedded model**

The DachshundSense system demonstrates the potential of a low-cost TinyML approach for real-time animal behaviour classification, highlighting the importance of data quality, sensor placement, and class design in embedded machine learning (Chambers et al., 2021). Strong performance was achieved for dynamic activities, supporting its feasibility for real-world deployment. However, results indicate that limitations were primarily driven by dataset scale and diversity rather than model design. Future work should focus on more extensive data collection to improve robustness and generalisation, reflecting both the promise and practical challenges of embedded machine learning systems (Chambers et al., 2021).

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
