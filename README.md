Credits: https://github.com/xhuvom/darknetFaceID
Other References: https://github.com/quanhua92/darknet

# WORK FLOW
# Requisite

// create folders for original and darknet images and annotations
mkdir /Users/elim/Site/git/darknetFaceID/data/edwin/images-original /Users/elim/Site/git/darknetFaceID/data/edwin/labels-original /Users/elim/Site/git/darknetFaceID/data/edwin/images-darknet /Users/elim/Site/git/darknetFaceID/data/edwin/labels-darknet


# CAPTURE 
// edit the ouput directories in src/image.c line 223 & 227

// compile the darknet executable
make clean && make

// start the capture
clear && ./darknet detector demo cfg/coco.data /Users/elim/Site/git/quanhua-weights/yolo-face.cfg /Users/elim/Site/git/quanhua-weights/yolo-face_final.weights
 

# TRAIN
// convert images to darknet JPEGs
clear && mogrify -format JPEG -path /Users/elim/Site/git/darknetFaceID/data/edwin/images-darknet /Users/elim/Site/git/darknetFaceID/data/edwin/images-original/*jpg

// run the label to annotation conversion
python scripts/convert.py

# DEPLOY
./darknet yolo train cfg/yolo-face.cfg weights/yolo-face_final.weights 




For more information see the Darknet project website.
For questions or issues please use the Google Group.