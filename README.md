# Object Detection on Jetson Nano

This repository provides a guide to performing object detection on Jetson Nano using the `jetson-inference` library. The guide includes steps for detecting objects in images, videos, and live camera streams using pre-trained models.

## Table of Contents

1. [Setup Jetson Nano](#setup-jetson-nano)
2. [Install jetson-inference](#install-jetson-inference)
3. [Running Object Detection](#running-object-detection)
   - [On Static Images](#on-static-images)
   - [On Video Files](#on-video-files)
   - [On Multiple Images](#on-multiple-images)
   - [On Live Camera Stream](#on-live-camera-stream)
4. [Customization](#customization)
   - [Changing Detection Models](#changing-detection-models)
   - [Adjusting Detection Sensitivity](#adjusting-detection-sensitivity)
   - [Customizing Overlay](#customizing-overlay)
5. [Optimizing Performance](#optimizing-performance)
6. [References](#references)

## Setup Jetson Nano

Ensure your Jetson Nano is properly set up with the JetPack SDK, which includes TensorRT, CUDA, and cuDNN. Follow the [official guide](https://developer.nvidia.com/embedded/jetpack) to set up your Jetson Nano.

## Install jetson-inference

To install the `jetson-inference` library, execute the following commands:

```bash
# Clone the repository
git clone https://github.com/dusty-nv/jetson-inference.git

# Navigate to the project directory
cd jetson-inference

# Create a build directory
mkdir build
cd build

# Configure and build the project
cmake ..
make

# Install the library
sudo make install
sudo ldconfig
```
## Running Object Detection
### On Static Images:
```python
python3 detectnet.py --network=ssd-mobilenet-v2 images/peds_0.jpg images/test/output.jpg
```
### On Video Files
To detect objects in a video file:

```python
# Download a sample video
wget https://nvidia.box.com/shared/static/veuuimq6pwvd62p9fresqhrrmfqz0e2f.mp4 -O pedestrians.mp4

python3 detectnet.py pedestrians.mp4 images/test/pedestrians_ssd.mp4
```
### On Multiple Images
To process a sequence or directory of images:

```python
python3 detectnet.py "images/peds_*.jpg" images/test/peds_output_%i.jpg
```

### On Live Camera Stream
To perform real-time object detection using a camera connected to Jetson Nano:
```python
python3 detectnet.py /dev/video0 images/test/output.mp4
```
## Customization
### Changing Detection Models
You can change the detection model using the --network flag. For example, to use the ssd-inception-v2 model:
```python
python3 detectnet.py --network=ssd-inception-v2 input.jpg output.jpg
```
### Adjusting Detection Sensitivity
You can adjust the detection threshold to change the sensitivity:
```python
python3 detectnet.py --threshold=0.3 input.jpg output.jpg
```
The --threshold flag sets the minimum detection confidence (default is 0.5).
### Customizing Overlay
You can customize the overlay options to display bounding boxes, labels, and confidence scores:
```python
python3 detectnet.py --overlay=box,labels,conf input.jpg output.jpg
```
The overlay options include box, labels, conf, and none.

## References


