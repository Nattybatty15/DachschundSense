# DachschundSense
CASA0018 Deep Learning for Sensor Networks course material. 

## Overview
DachshundSense is a lightweight wearable system built using an Arduino Nano 33 BLE Sense and TinyML. It classifies three core behaviours — walking, sitting, and lying down — using IMU sensor data collected directly from the collar.

This repository contains the full project structure, including documentation, training data, the Edge Impulse export, and the Arduino sketch used for live inference.

A full write‑up of the methodology, experiments, and results can be found in report.md, which serves as the main project report.

## Important Notes

**Clarifications**

The live demo shown in the video includes the only instance where the dog’s behaviour was intentionally prompted for demonstration purposes.
All training data was collected from natural behaviour, not staged or coerced actions.

- Retraining required for other dogs
- This model is not generalisable across dog breeds
- Because IMU signatures vary by size, posture, morphology, and behaviour: Any user repeating this project MUST retrain the model with data from their own dog.

The model in this repo is tailored to one specific dachshund and will not reliably transfer to other dogs.

## Folder Details
```data/```
Contains all IMU training samples, labels, and raw data exported from Edge Impulse.
Includes the full project ZIP from Edge Impulse so the entire pipeline is reproducible.

```sketches/```
Contains the Arduino Nano 33 BLE Sense sketch used for running live inference and displaying classification output. The second sketch represents a future extension of the system, introducing Bluetooth Low Energy (BLE) for wireless communication. It builds on the original inference the main changes include:

- added <ArduinoBLE.h>
- created a BLE service + characteristic
- started BLE advertising in setup()
- sent the highest-confidence prediction over BLE after each inference

```documentation/```
Holds images, live demos and supporting materials used in the report.

```report.md```
Serves as the main report covering background, data collection, modelling, experiments, and conclusions.
