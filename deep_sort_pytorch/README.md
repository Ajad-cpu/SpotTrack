# Deep Sort with PyTorch

![](demo/demo.gif)

## Update(1-1-2020)

Changes

* fix bugs
* refactor code
* accerate detection by adding nms on gpu

## Latest Update(07-22)

Changes

* bug fix (Thanks @JieChen91 and @yingsen1 for bug reporting).
* using batch for feature extracting for each frame, which lead to a small speed up.
* code improvement.

Futher improvement direction

* Train detector on specific dataset rather than the official one.
* Retrain REID model on pedestrain dataset for better performance.
* Replace YOLOv3 detector with advanced ones.

**Any contributions to this repository is welcome!**

## Introduction

This is an implement of MOT tracking algorithm deep sort. Deep sort is basicly the same with sort but added a CNN model to extract features in image of human part bounded by a detector. This CNN model is indeed a RE-ID model and the detector used in PAPER is FasterRCNN, and the original source code is HERE.
However in original code, the CNN model is implemented with tensorflow, which I'm not familier with. SO I re-implemented the CNN feature extraction model with PyTorch, and changed the CNN model a little bit. Also, I use **YOLOv3** to generate bboxes instead of FasterRCNN.

## Dependencies

* python 3 (python2 not sure)
* numpy
* scipy
* opencv-python
* sklearn
* torch >= 0.4
* torchvision >= 0.1
* pillow
* vizer
* edict

## Quick Start

0. Check all dependencies installed

```bash
pip install -r requirements.txt
```

for user in china, you can specify pypi source to accelerate install like:

```bash
pip install -r requirements.txt -i <your-mirror>
```

1. Clone this repository

```
git clone git@github.com:ZQPei/deep_sort_pytorch.git
```

2. Download YOLOv3 parameters

```
cd detector/YOLOv3/weight/
# place yolov3.weights and yolov3-tiny.weights in this folder
cd ../../../
```

3. Download deepsort parameters ckpt.t7

```
cd deep_sort/deep/checkpoint
# download ckpt.t7 and put it in this folder
cd ../../../
```

4. Compile nms module

```bash
cd detector/YOLOv3/nms
sh build.sh
cd ../../..
```

Notice:
If compiling failed, the simplist way is to \*\*Upgrade your pytorch >= 1.1 and torchvision >= 0.3" and you can avoid the troublesome compiling problems which are most likely caused by either `gcc version too low` or `libraries missing`.

5. Run demo

```
usage: python yolov3_deepsort.py VIDEO_PATH
                                [--help]
                                [--frame_interval FRAME_INTERVAL]
                                [--config_detection CONFIG_DETECTION]
                                [--config_deepsort CONFIG_DEEPSORT]
                                [--display]
                                [--display_width DISPLAY_WIDTH]
                                [--display_height DISPLAY_HEIGHT]
                                [--save_path SAVE_PATH]          
                                [--cpu]          

# yolov3 + deepsort
python yolov3_deepsort.py [VIDEO_PATH]

# yolov3_tiny + deepsort
python yolov3_deepsort.py [VIDEO_PATH] --config_detection ./configs/yolov3_tiny.yaml

# yolov3 + deepsort on webcam
python3 yolov3_deepsort.py /dev/video0 --camera 0

# yolov3_tiny + deepsort on webcam
python3 yolov3_deepsort.py /dev/video0 --config_detection ./configs/yolov3_tiny.yaml --camera 0
```

Use `--display` to enable display.
Results will be saved to `./output/results.avi` and `./output/results.txt`.

All files above can also be accessed from shared storage (check repository notes for locations).

## Training the RE-ID model

The original model used in paper is in original\_model.py, and its parameter is available as a checkpoint file.

To train the model, first you need download Market1501 dataset or Mars dataset.

Then you can try train.py to train your own parameter and evaluate it using test.py and evaluate.py.

## Demo videos and images

* demo.avi
* demo2.avi

![1.jpg](demo/1.jpg)
![2.jpg](demo/2.jpg)

## References

* paper: Simple Online and Realtime Tracking with a Deep Association Metric (PAPER)
* code: nwojke/deep\_sort
* paper: YOLOv3 (paper)
* code: Joseph Redmon/yolov3
