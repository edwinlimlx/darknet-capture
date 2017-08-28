YOLO V2

## Requisite
1. Create folder for darknet images and label
```
mkdir captures captures/final
```



## CAPTURE 
1. Change the name for class in src/image.c line 226

2. Change the path in cfg/yolo-face.data 

3. Change the name in data/face.names

4. Compile the darknet executable
```
make clean && make
```
5. Start the capture
Try with -thresh .7 or more for better quality training. Using yolo-face.cfg and yolo-face_final.weights from quanhua92's weights https://mega.nz/#F!GRV1XKbJ!v8BCsFO8iJVNppiGXY4qMw
```
clear && ./darknet detector demo cfg/yolo-face.data cfg/yolo-face.cfg weights/yolo-face_final.weights -thresh .6
``` 
6. Shorthand for recompiling and start capturing
```
clear && make clean && make && ./darknet detector demo cfg/yolo-face.data weights/yolo-face.cfg weights/yolo-face_final.weights -thresh .6
``` 



## TRAIN
1. Train
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