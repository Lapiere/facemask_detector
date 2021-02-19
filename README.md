To train the network:

1. Clone the DarkNet Repository

```
git clone https://github.com/AlexeyAB/darknet.git
```

2. Compile DarkNet
```
cd darknet

sed -i 's/OPENCV=0/OPENCV=1/' Makefile
sed -i 's/GPU=0/GPU=1/' Makefile
sed -i 's/CUDNN=0/CUDNN=1/' Makefile

make
```

3. Download Data
```
wget "https://www.dropbox.com/s/uq0x32w70c390fb/mask_no-mask_dataset.zip?dl=1" -O mask_no-mask_dataset.zip
unzip mask_no-mask_dataset.zip -d mask_no-mask_dataset
```

Prepare dataset files:
Copy prepare_data in the darknet folder

```
python3 prepare_data.py
```

4. Copy config files

Copy the config files for yolov3 or yolov4 in the darknet folder

5. Download weights for convolutional backbone

yolov3:
```
wget "https://www.dropbox.com/s/18dwbfth7prbf0h/darknet53.conv.74?dl=1" -O darknet53.conv.74
```

yolov4:
```
https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.conv.137
```


6. Train network

yolov3:
```
./darknet detector train yolov3-maskdetector-setup.data yolov3-maskdetector-train.cfg ./darknet53.conv.74 -map
```

yolov4
```
./darknet detector train yolov4-maskdetector-setup.data yolov4-maskdetector-train.cfg ./yolov4.conv.137 -map
```

7. Test network on images

```
./darknet detector test yolov3-maskdetector-setup.data yolov3-maskdetector-test.cfg backup/yolov3-maskdetector-train_best.weights image.jpg -thresh .6

./darknet detector test yolov4-maskdetector-setup.data yolov4-maskdetector-test.cfg backup/yolov4-maskdetector-train_best.weights image.jpg -thresh .6
```

8. Test network on videos
```
./darknet detector demo yolov3-maskdetector-setup.data yolov3-maskdetector-test.cfg backup/yolov3-maskdetector-train_best.weights test-video.mp4 -thresh .6 -out_filename out-vid.avi -dont_show

./darknet detector demo yolov4-maskdetector-setup.data yolov4-maskdetector-test.cfg backup/yolov4-maskdetector-train_best.weights test-video.mp4 -thresh .6 -out_filename out-vid.avi -dont_show

```
