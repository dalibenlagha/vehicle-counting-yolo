# Real-Time Vehicle Counting with YOLO11 + ByteTrack

Detect → Track → Count. Each vehicle is detected by **YOLO11**, given a stable ID by **ByteTrack**, and counted once when its center crosses a virtual line.

## How it works
1. **Detection:** Ultralytics YOLO11 (medium) runs on each frame at 1280 px for small, distant vehicles.
2. **Tracking:** ByteTrack (from Roboflow `trackers`) keeps the same ID for each vehicle across frames, so nothing is counted twice.
3. **Counting:** a Supervision `LineZone` counts each ID when the center of its box crosses the line.

## What I learned
My first version counted only about 20% of the vehicles. The detector wasn't the problem: the tracker's default activation threshold (0.7) ignored every vehicle detected with lower confidence. Lowering the tracker thresholds, using a larger model and a higher input resolution fixed it.

## Run it
Open `object_counting.ipynb` in [Google Colab](https://colab.research.google.com), choose **Runtime → Change runtime type → T4 GPU**, and run the cells in order. The output video is saved as `counted_output.mp4`.

## Stack
Python · Ultralytics YOLO11 · ByteTrack (`trackers`) · Supervision · OpenCV
