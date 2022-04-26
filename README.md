# Food_NonFood_Classification
This project is for the second interview of ARTORG Center for Biomedical, University of Bern.
The original networks I have used include: ResNet50, ResNet101, ResNet152, DenseNet161, DenseNet201.
The revised network I used in this project is: DenseNet-201 with additional CBAM.
I will illustrate the processes and methods in the presentation.

## Requirements
Torch = 1.10.2 <br>
Torchvision = 0.11.3 <br>
cuda && cudnn <br>

## Data preparation
The data set of this task should be prepared. The directory structure is the standard layout for the torchvision datasets.ImageFolder, and the training and validation data is expected to be in the ```train/``` folder and ```val/``` folder respectively:  <br>
```
Food_classification/
    train/
        0/
            0.jpg
            1.jpg
            …
        1/
            0.jpg
            1.jpg
            …
    val/
        0/
            0.jpg
            1.jpg
            …
        1/
            0.jpg
            1.jpg
            …

```

## Training
To train the original network (ResNet and DenseNet) run: <br>
``` train_main.py ``` <br>
**Do not forget:** <br>
Changing **Pick_model** into the structure you want to train in line 19.<br>
Changing path in **data_loader()** into the dictionary where you data located in line 109.<br>

To train the revised network run: <br>
``` train_dense_cbam.py ```<br>
**Do not forget:** <br>
Changing path in **data_loader()** into the dictionary where you data located in line 52.

To train the revised network with online augmentation run:<br>
``` train_dense_cbam.py ``` <br>
**Do not forget:** <br>
Enable the function of **OnlineAugmentation()** in line 89.

## Grad-cam
This project use Grad-cam as the validation of model’s attention.<br>
The directory structure has been showed below. ```Example_food/``` contains all of images that to be tested.
```
Food_classification/Example_food/
    0/
        0.jpg
        1.jpg
        …
    1/
        0.jpg
        1.jpg
        …
```
```Example_food_out/``` contains the results of Grad-cam.
```
Food_classification/Example_food_out/
    0/
        0_out.jpg
        1_out.jpg
        …
    1/
        0_out.jpg
        1_out.jpg
        …
```
Run ```cam.py``` to generate the result of original networks. Please notice the information from line 78 to line 106 to change the corresponding parts.<br>

Run ```cam_cbam.py``` to generate the result of revised model.

## Result
### Accuracy
| - | Accuracy  | Model Size (M) |  Epoch  |
| --- | --- | --- | --- |
| Resnet50 | 92.620 | 204 | 212 | 
| Resnet101 | 92.681 | 357 | 55 | 
| Resnet152 | 92.193 | 482 | 214 | 
| Densenet161 | 93.395 | 230 | 154 | 
| Densenet201 | 93.395 | 161 | 49 | 
| Densenet201-CBAM | 94.451 | 77 | 199 | 
| Densenet201-CBAM-Aug | 95.24 | 77 | 185 |

### Grad-cam
#### Original models
![pictures](https://github.com/SunJJ1996/Food_NonFood_Classification/tree/main/pictures/origin_food.PNG) <br>
![pictures](https://github.com/SunJJ1996/Food_NonFood_Classification/tree/main/pictures/origin_nonfood.PNG) <br>
#### Revised model
![pictures](https://github.com/SunJJ1996/Food_NonFood_Classification/tree/main/pictures/revised.PNG) <br>
