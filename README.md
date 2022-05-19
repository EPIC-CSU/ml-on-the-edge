# Machine Learning Models for Low Power Object Detection

This repository contains code for video object detection, as part of the 2021 IEEE Low Power Computer Vision Challenge. The code consits of a YOLOv5 object detector model that has been optimized for real-time detection on the LPCV.ai dataset, and has been deployed on teh Coral AI accelerator. The image below shows the YOLOv5 object detector in action.

![LPCV video object detection](http://www.engr.colostate.edu/~sudeep/wp-content/uploads/lpcv-challenge.gif)

## Notebook and Folder Descriptions
- YOLOv5_LPCV_Train: Used to train YOLOv5 on the LPCV data. To train on the LPCV.ai data from the challenges files. If you do not have a zip file of the LPCV data in image and label format, you must upload all LPCV.ai videos and csv files before running all cells in succession. If you possess such a zip file, unzip the folder and run the cells beginning with the data augmenation cells.

- YOLOv5_Compile_For_Edge: A modified version of Google's compile_for_edgetpu.ipynb. This version includes the ability to convert a .pt model to .tflite using the YOLOv5 repo, as well as a special command to compile the model that overrides an error that occurs without the edited command.

This folder yolov5-coral contains scripts necessary to run an edge optimized version of YOLOv5

To run on Coral: 
  ```bash
  python3 detect.py --weights MODEL_PATH --source SOURCE --imgsz INPUT_SIZE --data DATASET_YAML --conf CONFIDENCE_PARAMETER
  ```
  
   - MODEL_PATH - location of the model
   - SOURCE - location of the source image or video
   - INPUT_SIZE - one of 256, 320, 384, 448, or 512 - should match the input size of the model
   - CONFIDENCE_PARAMETER - a decimal number that the model should be as confident that an object is in a location, typically anywhere from 0.25 to 0.6

The yaml file should contain the same list as found in the yaml file used to train the model. The current detect.py uses NumPy arrays, however a different version exists in a branch entitled "torch" which uses torch tensors. This may work faster on the Raspberry Pi with Coral accelerator. The current detect.py may appear slow, however that is due only to OpenCV. If you remove the write or imshow statements, the script will run much faster. Print statements exist to demonstrate which parts of the code are taking a long or short time. general.py contains auxilary function necessary for detect.py to work properly.
