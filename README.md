Credits: https://github.com/xhuvom/darknetFaceID
Other References: https://github.com/quanhua92/darknet


## Requisite
1. create folders for original and darknet images and annotations
```
mkdir ./data/edwin/images-original ./data/edwin/labels-original ./data/edwin/images-darknet ./data/edwin/labels-darknet
```


## CAPTURE 
1. edit the ouput directories in src/image.c line 226 & 231

2. compile the darknet executable
```
make clean && make
```

3. start the capture
```
clear && ./darknet detector demo cfg/coco.data cfg/yolo-face.cfg weights/yolo-face_final.weights
``` 


## TRAIN
1. convert images to darknet JPEGs
```
clear && mogrify -format JPEG -path ./data/edwin/images-darknet ./data/edwin/images-original/*jpg
```

2. run the label to annotation conversion
```
python scripts/convert.py
```


## DEPLOY
```
./darknet yolo train cfg/yolo-face.cfg weights/yolo-face_final.weights 
```



For more information see the [Darknet project website](http://pjreddie.com/darknet).

For questions or issues please use the [Google Group](https://groups.google.com/forum/#!forum/darknet).