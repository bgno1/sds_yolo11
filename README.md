# Enhanced YOLO11 for Lightweight and Accurate Drone-Based Maritime Search and Rescue Object Detection

## 1. Overview

This repository contains the code supporting the article **"Enhanced YOLO11 for Lightweight and Accurate Drone-Based Maritime Search and Rescue Object Detection"**, which is currently under peer review.

YOLO configuration files supporting the experiments in the paper can be found in the `cfgs` folder.

The `cfgs` folder contains two subfolders:

- **`Ablation Study`**: Includes configuration files for all models used in the Ablation Study section of the paper.
- **`SOTA Comparison`**: Contains configuration files for our proposed YOLO11 models used in the "Comparison with State-of-the-Art Methods" section of the paper.

## 2. SeaDronesSee Dataset

The SeaDronesSee dataset, essential for maritime search and rescue object detection tasks, can be downloaded directly from the official repository: [Download SeaDronesSee Dataset](https://cloud.cs.uni-tuebingen.de/index.php/s/aJQPHLGnke68M52). For further details please refer to the official SeaDronesSee website: [https://macvi.org/](https://macvi.org/).

## 3. User Guide

### 3.1 Integrating the Space-to-Depth Module into YOLO11

To integrate the Space-to-Depth (SPD) module into the YOLO11 framework, follow these steps:

1. Place the `code/space_to_depth.py` file from this repository into the `ultralytics/nn/modules` folder in the YOLO11 project.

2. In the `ultralytics/nn/tasks.py` file of the YOLO11 project, add the following import statement:
   
   ```python
   from ultralytics.nn.modules.space_to_depth import space_to_depth
   ```

3. Update the YOLO11 model's YAML configuration file to include the `space_to_depth` module. Example configurations can be found in the `cfgs` directory of this repository.

**Notes:**

- The Space-to-Depth module is based on the original paper by Sunkara et al., titled *"No More Strided Convolutions or Pooling: A New CNN Building Block for Low-Resolution Images and Small Objects"*.
- The official code for the SPD module can be found in the repository [SPD-Conv](https://github.com/LabSAINT/SPD-Conv/tree/main/YOLOv5-SPD).

### 3.2