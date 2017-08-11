YOLO V1

## Requisite
1. Create folders for original and darknet images and annotations
```
mkdir ./data/edwin ./data/edwin/images-original ./data/edwin/labels-original ./data/edwin/images-darknet ./data/edwin/labels-darknet
```


## CAPTURE 
1. Edit the ouput directories in src/image.c line 226 & 231

2. Compile the darknet executable
```
make clean && make
```

3. Start the capture
images will be saved into path specific in #1. In my case is data/edwin/images-original/
```
clear && ./darknet detector demo cfg/yolo-face.data cfg/yolo-face.cfg weights/yolo-face_final.weights 
``` 


## TRAIN
1. Convert images to darknet JPEGs. This will convert *.jpg images in data/edwin/images-original/ to JPEG at data/edwin/images-darknet/
```
clear && mogrify -format JPEG -path ./data/edwin/images-darknet ./data/edwin/images-original/*jpg
```

2. Update the root path in convert.py

3. Run the label to annotation conversion. This will generate edwin_list.txt & convert data/edwin/label-original/ to data/edwin/label-darknet/
```
python scripts/convert.py
```

Lazy me
```
clear && mogrify -format JPEG -path ./data/edwin/images-darknet ./data/edwin/images-original/*jpg && python scripts/convert.py
```

3. Train
```
./darknet yolo train cfg/yolo-face.cfg weights/yolo-face_final.weights
./darknet detector train cfg/yolo-face.data cfg/yolo-face.cfg weights/darknet19_448.conv.23
```

## DEPLOY & DETECTOR (NOT TESTED)
```
./darknet detector demo cfg/yolo-face.data cfg/yolo-face.cfg backup/yolo-face_final.weights
```

## Snippets
1. Made changes to sources files, recompile and execute training
```
make clean && make && ./darknet yolo train cfg/yolo-face.cfg weights/yolo-face_final.weights 
```

2. Complete clean up, rebuild and jumps to capture training (NOT TESTED)
```
clear && rm -R data/edwin && mkdir ./data/edwin ./data/edwin/images-original ./data/edwin/labels-original ./data/edwin/images-darknet ./data/edwin/labels-darknet && make clean && make && clear && ./darknet detector demo cfg/yolo-face.data cfg/yolo-face.cfg weights/yolo-face_final.weights
```

3. Rebuild and Train
```
clear && make clean && make
```

## TODO
- [ ] deploy

## SETUP
* Intel Core i7, 2.5 GHz
* 1 Processor, 4 Cors
* 16GB MEMORY
* AMD Radeon R9 M370X

## Credits & Reference & Acknowledgments 
* Credits: https://github.com/xhuvom/darknetFaceID
* Other References: https://github.com/quanhua92/darknet
* For more information see the [Darknet project website](http://pjreddie.com/darknet).
* For questions or issues please use the [Google Group](https://groups.google.com/forum/#!forum/darknet).