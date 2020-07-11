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
First you have to open the classes.txt and you should define your classes after that you run the command and you download 200 labeled photos for of every one of the 4 classes for training under the same roof
```bash
python main.py downloader --classes Person Mug Bottle Vehicle --type_csv train --multiclasses 1 --limit 200
```

Step 4
Transform labels to pascal voc xml
```bash
python oid_to_pascal_voc_xml.py
```
