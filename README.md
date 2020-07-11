# dpsd13131
## Requirements
- Python 3.6
- Pytorch 
- Git
- Git Bash
- Torch 1.4.0
- Torchvision 0.5.0


Step 1

You install the packages

```bash
pip install -r Requirements.txt
```

Step 2

```bash 
cd object-detection/OIDv4_ToolKit/
```

Step 3 

First you have to open the file 

- dpsd13131\object-detection\OIDv4_ToolKit\classes.txt 
- dpsd13131\object-detection\YoloV3-Custom-Object-Detection\conversion\classes.txt
- dpsd13131\object-detection\YoloV3-Custom-Object-Detection\training\object.names

```
Person
Mug
Bottle
Vehicle
```

and you should define your classes after that you run the command and you download 200 labeled photos for of every one of the 4 classes for training under the same roof
```bash
python main.py downloader --classes Person Mug Bottle Vehicle --type_csv train --multiclasses 1 --limit 200
```

Step 4

Transform labels to pascal voc xml
```bash
python oid_to_pascal_voc_xml.py
```

Step 5

You have to change directory

```bash
cd ..\YoloV3-Custom-Object-Detection\conversion
copy ..\..\OIDv4_ToolKit\TO_PASCAL_XML\*.* xmls
python xmltotxt.py -xml xmls -out output
dir output
```
Step 6 

```
cd ..\training
mkdir images
mkdir labels
copy ..\..\OIDv4_ToolKit\OID\Dataset\train\Person_Mug_Bottle_Vehicle\*.jp* images
copy ..\conversion\output labels
```

Step 7


You should to generate two files train.txt and test.txt 
```
python train_test.py
cd ..
```
You should to edit this file 
dpsd13131\object-detection\YoloV3-Custom-Object-Detection\training\trainer.data

```
classes=4
train=\Users\Helena\dpsd13131\object-detection\YoloV3-Custom-Object-Detection\training\train.txt
valid=\Users\Helena\dpsd13131\object-detection\YoloV3-Custom-Object-Detection\training\test.txt
names=\Users\Helena\dpsd13131\object-detection\YoloV3-Custom-Object-Detection\training\object.names
backup=training\backup
eval=coco
```
python train.py --epochs 110 --data training/trainer.data --cfg training/yolov3.cfg --batch 4 --accum 1
 
 
 
