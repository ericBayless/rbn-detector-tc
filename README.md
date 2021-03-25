# Contents
- [Problem Statement](#Problem-Statement)
- [Executive Summary](#Executive-Summary)
- [Conclusions](#Conclusions)
- [File Directory](#File-Directory)
- [Data Description](#Data-Description)
- [Resources](#Resources)

# Problem Statement
Create bib and digit detector models that can be used in an iOS app.

# Executive Summary
Previous models for race bib number detection have been created using Darknet Yolov4-tiny which can be found [here](https://github.com/ericBayless/bib-detector)


# Conclusions
While conversion of the Darknet models appears to be possible, more work is needed to resolve errors rebuilding the YOLOv4-tiny models using other frameworks.  The more straight-forward solution is to train new models using Turi Create which can directly export a coreML model which is used by iOS.  This method produced similar results for bib detection with an average precision of 95.67% versus the darknet average precision of 94.42%.  However, the mean average precision for the digit detector created with Turi Create yielded much worse results when compared to the Darknet YOLOv4-tiny model trained on the same data (mAP 39.89% vs. 84.12%).  The only object detection model available in Turi Create currently is a slightly modified YOLOv2 model.  This could explain the difference in ability given that many improvements were made in YOLOv3 and YOLOv4.

# File Directory
```
bib-detector-tc
|__ code
|   |__ 01_Data_Preprocessing.ipynb   
|   |__ 02_Model_Training.ipynb 
|__ config
|   |__ bib_detector.model 
|   |__ digit_detector.model
|   |__ digit_detector2.model
|   |__ bib_detector.mlmodel
|   |__ digit_detector.mlmodel 
|   |__ digit_detector2.mlmodel 
|__ data
|   |__ Bibs
|       |__ images of bibs for validation
|   |__ Demo-Images
|       |__ images of runners with bibs
|   |__ RBNR
|       |__ augmented 
|       |__ rbnr_tiny.sframe
|   |__ SVHN 
|       |__ extra
|       |__ svhn_tiny.sframe
|       |__ svhn1_tiny.sframe
|__ scratch
|   |__ scratch work files
|__ README.md
```

# Data Description
#### Race Bib Number (RBNR) Dataset
The dataset can be found [here](https://people.csail.mit.edu/talidekel/RBNR.html)

This image data is split into 3 sets.  Augmented images from sets 1 and 2 were used to train the model to detect racing bibs. 

#### Street View House Number (SVHN) Dataset
The dataset can be found [here](http://ufldl.stanford.edu/housenumbers/)

This dataset contains a set of full numbers split into train, test, and extra, as well as cropped digits with the same catagorization.  Only a subset of the extra full numbers were used to train a model to detect digits.

# Resources
#### Studies
- [Racing Bib Number Recognition](https://people.csail.mit.edu/talidekel/RBNR.html)
- [Racing Bib Number Recognition Using Deep Learning](https://www.researchgate.net/publication/335234017_Racing_Bib_Number_Recognition_Using_Deep_Learning)

#### Turi Create Object Detection
- [Turi Create Object Detection](https://apple.github.io/turicreate/docs/userguide/object_detection/)