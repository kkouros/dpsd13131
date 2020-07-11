# dpsd13131
## Requirements
- Python 3.6 
- Torch 1.4.0
- Torchvision 0.5.0
- Git
- CUDA (optional)


**Step 1**

Clone Yolo v3 Repo
- git clone https://github.com/kkouros/dpsd13131

Download the Weights 
- https://pjreddie.com/media/files/yolov3.weights

**Step 2**


Install the packages

```bash
pip install -r Requirements.txt
```


**Step 3**

Use command to prepare download images
```bash 
cd object-detection/OIDv4_ToolKit/
```


**Step 4**


Open the files

- dpsd13131\object-detection\OIDv4_ToolKit\classes.txt 
- dpsd13131\object-detection\YoloV3-Custom-Object-Detection\conversion\classes.txt
- dpsd13131\object-detection\YoloV3-Custom-Object-Detection\training\object.names

```
Person
Mug
Bottle
Vehicle
```

and define your classes after running the command and downloading 200 labeled photos for each of the four training classes under the same roof
```bash
python main.py downloader --classes Person Mug Bottle Vehicle --type_csv train --multiclasses 1 --limit 200
```


**Step 5**


Transform labels to pascal voc xml
```bash
python oid_to_pascal_voc_xml.py
```


**Step 6**


Change directory

```bash
cd ..\YoloV3-Custom-Object-Detection\conversion
copy ..\..\OIDv4_ToolKit\TO_PASCAL_XML\*.* xmls
python xmltotxt.py -xml xmls -out output
dir output
```


**Step 7**

Create directories images, labels and copy the photos
```
cd ..\training
mkdir images
mkdir labels
copy ..\..\OIDv4_ToolKit\OID\Dataset\train\Person_Mug_Bottle_Vehicle\*.jp* images
copy ..\conversion\output labels
```
 
 
 **Step 8**
 

Generate two files train.txt and test.txt 
```
python train_test.py
cd ..
```

``` python
# Percentage of images to be used for the test set
percentage_test = 30;
```

Edit this file 
dpsd13131\object-detection\YoloV3-Custom-Object-Detection\training\trainer.data

```
classes=4
train=\Your_Path\dpsd13131\object-detection\YoloV3-Custom-Object-Detection\training\train.txt
valid=\Your_Path\dpsd13131\object-detection\YoloV3-Custom-Object-Detection\training\test.txt
names=\Your_Path\dpsd13131\object-detection\YoloV3-Custom-Object-Detection\training\object.names
backup=training\backup
eval=coco
```

```
python train.py --epochs 110 --data training/trainer.data --cfg training/yolov3.cfg --batch 4 --accum 1
```
epochs 110, batch 4 are variables and you can change them. Depends on GPU. 
ctrl+c (to stop anytime) and use command below to resume the training
```
python train.py --epochs 110 --data training/trainer.data --cfg training/yolov3.cfg --batch 4 --accum 1 --resume
```



 **Step 9**
 
 
 Detect
 
 
