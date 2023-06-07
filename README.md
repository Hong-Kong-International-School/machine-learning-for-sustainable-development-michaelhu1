# Mission:
There are two reasons why someone would not properly recycle their waste, either they are too lazy to properly recycle their waste, or they do not know where different types of trash go. A lot of it has to be manually sorted, which many people may be unwilling to do. According to Resource Recycling Systems in Ann Arbor, Michigan, 63% of schools surveyed had recycling programs on campus, while only 24% of waste was recycled at these schools [1]. This project aims to increase the amount of recycled trash by creating a model which can automatically sort trash. This object detection model will be able to classify different types of recyclable trash and output what type of trash it is. It can be applied in many scenarios, such as an automatic sorting recycling bin.

The SDGs this project will focus on are SDG 11: sustainable cities and communities, and SDG 12: responsible consumption and production. This project serves as a proof of concept that AI can be used to sort trash. 

## Required materials
1x Raspberry Pi <br> 
1x HDMI - HDMI cable <br>
1x Monitor <br>
1x Keyboard & Mouse <br>
1x Micro SD card <br>
1x MicroSD to SD card adapter <br>
1x Ethernet Cable <br>
3x LED lights <br> 
1x Small breadboard <br>
3x Resistors <br>
1x Webcam <br> 
Python (Version 3.7 - 3.9) <br>

## What does the system do
The model takes in an image as an input and identifies what type of trash it is and where the trash is. After classifying the type of trash in the frame, the type of trash will be output in the form of different colored LEDs to represent different types of recyclable trash.

## How the system works  
The system runs on Python utilizing the OpenCV library on a Raspberry Pi. After taking in the input from a live camera feed connected to the Pi, the trained object classification model stored in the tflite file is then used to identify what type of trash is in the frame.   

## How to install the system
Upload the run.py and model.tflite files within the repository, along with installing the required packages on the Raspberry Pi.  
Packages that need to be installed include cv2, tflite_support, and RPi.GPIO. These packages can be installed using pip.  

## How to use the system
Make sure a Raspberry Pi compatible webcam is plugged into the Pi.  
Run the command below:  
`python run.py --model model.tflite`  
Point the camera to the trash.

# Model Details:
The model was created using transfer learning on top of the efficientdet_lite3 model.  
The model was trained for 30 epochs with a batch size of 8 and the weights for the whole model were changed.  

## Data Source
Took pictures of common recycled trash from the supermarket.
[Data.](https://drive.google.com/drive/folders/1UmpN3HiBLTDrQucEYZQCulAUr62JJf89?usp=sharing)

## Model Performance
The model has an average precision of 48.4% on the validation data. The final validation loss was 0.4477. Although the training accuracy is low, the object detection can still correctly classify trash to a decent degree showing that the real world performace is still acceptable. Lower model performance is likely due to using lite versions of pre-trained models to fit the Raspberry Pi's processing capabilities.

# Development Overview:

## Design Process
The goal of the project was to create a compact live object detection system that could be run outside of a computer. In order to do this, I needed to run the system on microcontroller. The microcontroller I decided to use was a Raspberry Pi. As the Raspberry Pi is not a very powerful micro controller, a lot of the process was built around accommodating the Pi's processing power to successfully run the model. This included using a tflite model rather than a TensorFlow model. Because the goal of the system is to be used in other applications outside of just object detection, the system would also have to make an output of what it detects shown in the different colored LEDs. 

## Stages of Development
The first stage of development was creating a dataset. This was done by taking over 300 photos of recyclable trash from supermarkets and around the school.   
The second stage of development involved training a model compatible with the Raspberry Pi. 
The third stage of development was getting the live object detection to run on the Pi using the OpenCV library along with the trained model.
The final stage of development was getting the system to output the type of trash it detects using LEDs and GPIO on the Pi.

## Future Work
There are many ways in which the performance of this system can be improved. One of which is using a more powerful microcontroller such as the Nvidia Jetson. A stronger computing platform will allow the use of bigger, more accurate models, along with increasing the framerate and overall performance of the live object detection. Alternatively, I could upload the model to the could and use the Pi to send image data to and from the model in the cloud.  

Another way the performace of the system can be improved is by training a more accurate model. With more processing power, the model can be trained on a non-lite version of pre-trained models such as efficientnet, increasing prediction accuracy. The model can also be improved by getting more training data, as the dataset is currently limited with only 300 images.

## List of References

[1](https://recycle.com/2021-report-university-sustainability-recovery/)
[TFlite](https://www.tensorflow.org/lite/api_docs)  
[Efficientdet_lite3 pretrained model](https://www.tensorflow.org/lite/api_docs/python/tflite_model_maker/object_detector/EfficientDetLite3Spec)  
[OpenCV](https://docs.opencv.org/4.x/index.html)
