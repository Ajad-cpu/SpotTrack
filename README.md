Here's a short, image-free, simplified README you can use:

# YOLOv5 + DeepSort (PyTorch)

**Simple real-time multi-object tracker** — YOLOv5 produces detections which are passed to Deep SORT for identity tracking. Works with any object classes your YOLOv5 model can detect.

## Quick start

```bash
# clone
git clone --recurse-submodules https://github.com/mikel-brostrom/Yolov5_DeepSort_Pytorch.git

# install (Python 3.8+)
pip install -r requirements.txt
```

## Run tracker

```bash
# webcam
python track.py --source 0

# image, video, folder, YouTube or stream
python track.py --source img.jpg
python track.py --source vid.mp4
python track.py --source 'https://youtu.be/...' 
python track.py --source 'rtsp://...'
```

## Choose YOLOv5 model

```bash
# example: use small model with 640px
python track.py --source 0 --yolo_weights yolov5s.pt --img 640
```

## Track only certain classes

```bash
# persons only (COCO class 0)
python track.py --source 0 --classes 0
```

## Save MOT-style results

```bash
python track.py --source ... --save-txt
```

## Cite

If used in research, please cite: *Real-time multi-object tracker using YOLOv5 and deep sort* (Mikel Broström, 2020).

---

Want it even shorter (single paragraph) or tailored to a renamed project (e.g., "SpotTrack")? I can provide that version too.
