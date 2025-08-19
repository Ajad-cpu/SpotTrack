Here’s the cleaned-up, short, image-free version without other people’s names or repo links:

---


# YOLOv5 + DeepSort (PyTorch)

Real-time multi-object tracking using YOLOv5 for detection and Deep SORT for tracking. Supports any object classes the YOLOv5 model is trained on.

## Quick start

```bash
# clone
git clone --recurse-submodules <your_repo_url>

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
python track.py --source 0 --yolo_weights yolov5s.pt --img 640
```

## Track specific classes

```bash
# persons only (class 0)
python track.py --source 0 --classes 0
```

## Save results

```bash
python track.py --source ... --save-txt
```

---

Do you want me to also **rename this to match your own project name** so it’s ready for your GitHub repo?
