# Enhanced YOLO11 for Lightweight and Accurate Drone-Based Maritime Search and Rescue Object Detection

## 1. Overview

This repository contains the code supporting the article **"Enhanced YOLO11 for Lightweight and Accurate Drone-Based Maritime Search and Rescue Object Detection"**, which is currently under peer review.

YOLO configuration files supporting the experiments in the paper can be found in the `cfgs` folder.

The `cfgs` folder contains two subfolders:

- **`Ablation Study`**: Includes configuration files for all models used in the Ablation Study section of the paper.
- **`SOTA Comparison`**: Contains configuration files for our proposed YOLO11 models used in the "Comparison with State-of-the-Art Methods" section of the paper.

The Space-to-Depth and CARAFE modules introduced as part of the optimization strategies are available in the `code` folder of this repository. For detailed instructions on their usage, please refer to the **User Guide** section below.



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

3. modify the `parse_model` function in `tasks.py` by adding the following code under the `if m in ...` branch:
   
   ```python
   elif m is space_to_depth:
       c2 = 4 * ch[f]
   ```
   
   This ensures proper handling and integration of the `space_to_depth` module within the YOLO11 model architecture.

4. Update the YOLO11 model's YAML configuration file to include the `space_to_depth` module. Example configurations can be found in the `cfgs` directory of this repository.

**Notes:**

- The Space-to-Depth module is based on the original paper by Sunkara et al., titled *"No More Strided Convolutions or Pooling: A New CNN Building Block for Low-Resolution Images and Small Objects"*.
- The official code for the SPD module can be found in the repository: https://github.com/LabSAINT/SPD-Conv/tree/main/YOLOv5-SPD

### 3.2 Integrating CARAFE Upsampling into YOLO11

To integrate the CARAFE upsampling module into the YOLO11 framework, follow these steps:

1. Place the `code/carafe.py` file from this repository into the `ultralytics/nn/modules` folder in the YOLO11 project.

2. Add the following import statement to the `ultralytics/nn/tasks.py` file:
   
   ```python
   from ultralytics.nn.modules.carafe import CARAFE
   ```

3. Update the `parse_model` function in `tasks.py` to include the CARAFE module. Add `CARAFE` to the existing branch that processes modules like `Classify` and `Conv`. The updated code should look as follows:
   
   ```python
   from ultralytics.nn.modules.carafe import CARAFE
   ```

4. Configure the CARAFE module in the YAML configuration file for YOLO11. Refer to the example configurations provided in the `cfgs` directory of this repository.

**note:**

- The CARAFE upsampling is based on the original paper by Wang et al., titled "*CARAFE: Content-Aware ReAssembly of FEatures* ".

## 4. About Mamba-YOLO

- The implementation of Mamba-YOLO in our experiments strictly follows the methods provided in the original authors' GitHub repository: https://github.com/HZAI-ZJNU/Mamba-YOLO

- It is important to emphasize that Mamba-YOLO represents a remarkable and valuable recent contribution to the field. However, it was not specifically designed or optimized for the drone-based maritime search and rescue object detection task. As a result, its performance scores in our experiments are lower in this particular context.

- The inclusion of Mamba-YOLO in our experiments is solely intended to highlight the necessity of task-specific optimizations for the unique challenges of drone-based maritime search and rescue scenarios. The experimental results do not diminish the significance of MambaYOLO's contributions to broader object detection research.

## 5. About YoloOW

- The implementation of YoloOW in our experiments is based on the methods provided in the original authors' GitHub repository: https://github.com/Xjh-UCAS/YoloOW.

- Please note that we adhered to all training hyperparameter settings and pre-trained "YoloOW.pt" models specified by YoloOW's authors. The only modification was adjusting the input image size from 1280 to 640 to ensure fair comparisons with other methods in our experiments, as all other methods use an image size of 640. Consequently, the performance metrics reported in our experiments may be slightly lower than those in YoloOW's original paper.

- Additionally, YoloOW is a remarkable method specifically designed for drone-based maritime search and rescue object detection, focusing on achieving high precision rather than lightweight implementation. The inclusion of YoloOW in our experiments aims to emphasize the necessity of lightweight model optimizations for resource-constrained scenarios. This comparison does not diminish the significance of YoloOW's contributions to the field.