**Preventive Maintainance using Object Detection in Rolling Stock Images**

This project was done while interning at Wabtec Corporation, Bangalore.

**ABSTRACT**

This project explores the **improvement of YOLOv8 model** for the task of object
detection in rolling stock images. It also shines light on the need for using **augmentation techniques** 
to generate potential use-cases due to the **scarcity of image data**
for certain components of rolling stock images and further explores the comparizon
of various **image contrast enchancement** technique to know which one best suits the
object detection task.


To improve the performance of YOLOv8 for the task of object detection, 
we incorporate **different types of attention modules with the YOLOv8 architecture of varying
sizes (nano and small)**. The attention modules are chosen based on their efficacy in
**refining the feature representation** while still keeping the computational overheads in
check. The attention modules chosen were **ResBlock + CBAM, GAM, ECA, SA**.


Upon implementing the attention modules, findings reveal that for the YOLOv8
nano model the attention modules show no improvement over the baseline model,
but for the **YOLOv8 small model the ResBlock+CBAM and ECA attention module
give superior performance as compared to the baseline**.

**INTRODUCTION**

At Wabtec, the **Kinetix Machine Vision Algorithms** Team works at automated,
proactive monitoring of Rolling Stock (Engines and Carriages used by railways) condition, 
thereby providing data that can be processed to effectively assess rolling stock
condition from component level to full train inspection. Understanding component
condition in real time, enables:

-maintenance cost savings 

-helps prevent costly incidents

-decreases operational delays

-increases the predictability of long-term maintenance scheduling

**OBJECTIVE**

Monitoring of the rolling stock components is done using Object Detection Models
(YOLOv8) on image data collected using cameras positioned at the required customer site.
Some of the **major challenges** faced during object detection are as follows: 

-It’s a bit difficult to detect components which are a bit smaller in size. 

-Sometimes captured images suffer from challenging lighting conditions.

-Further the dataset for the images is vastly limited and also there are none to very few images for defective/faulty cases.


The objective is to improve the performance/detection capability of the Object Detection model (YOLOv8) such that we are able to overcome 
all or most of the challenges mentioned above.


**MOTIVATION**

The motivation behind detecting the objects is to assess the rolling stock component
condition by either detecting the presence/absence of particular elements of that
component or by using the positional co-ordinates of the elements in the component
to deduce the conditon of the component and proceed accordingly. After
object detection these steps are done during post processing.

**LITERATURE REVIEW**

Attention mechanisms, which enable neural networks to accurately focus on all
the relevant elements of the input, have become an essential component to improve
the performance of deep neural networks. They have also proven to be a potential
means to enhance deep CNNs and thus can improve the performance of a broad range
of computer vision tasks, e.g., image classification, object detection, and instance segmentation.


Attention mechanism have obtained excellent results in the field of object detection.
With the integration of attention mechanism, object detection models are able to
learn better feature representation while suppressing unnecessary information.


There are mainly two attention mechanisms widely used in computer vision tasks,
namely **spatial attention** which captures the **inter-spatial (pixel-level pairwise)** 
relationship between features and **channel attention** which captures the **inter-channel**
dependency between the features. Subsequently the development of the attention
modules can be roughly divided into two directions: enhancement of feature aggregation and 
combination of channel and spatial attention, while also limiting the
computatinal overhead as much as possible.


Based on this some of the attention modules considered are as follows:

• **CBAM: Convolutional Block Attention Module [Woo et al.,2018]**

                            
![image](https://github.com/user-attachments/assets/cd180ce3-b0b3-4b44-9691-00779a556810)

                        An Oveview of CBAM

                       
![image](https://github.com/user-attachments/assets/8117f1a1-b73f-4f2c-9feb-864be54ff260)

                       Channel Attention module in CBAM

                       
![image](https://github.com/user-attachments/assets/b4cd3863-1c60-4031-af7c-ce88396cd8a7)

                      Spatial Attention module in CBAM


• **Global Attention Mechanisms: Retain Information to Enhance Channel-Spatial Interactions [Liu et al.,2021]**

                         
![image](https://github.com/user-attachments/assets/3fedc749-19d1-4075-9bc0-9d0bca46a59e)

                        An overview of GAM

                      
![image](https://github.com/user-attachments/assets/47f3bdcc-4f2f-4bf7-adea-e3bc42bfc217)

                       Channel Attention Module in GAM
                       
                       
![image](https://github.com/user-attachments/assets/9990108e-24d2-4e14-a0b3-cf4e062e9ddf)

                       Spatial Attention Module in GAM

• **ECA-Net: Efficient Channel Attention for Deep CNN's [Wang et al.,2020]**

                
![image](https://github.com/user-attachments/assets/4c6822d2-beca-4a16-81ff-c6ed12c97165)

                    An overview of Efficient Channel Attention Module

• **SA-Net: Shuffle Attention for Deep CNN's Zhang et al.,2021]**

                         
![image](https://github.com/user-attachments/assets/93dcd91f-bce4-41b7-9dee-07694a42e544)

                    An overview of Shuffle Attention module 



**METHODOLOGY**

As seen from the literature review there are various approaches on how to improve the performance of 
deep CNN networks using attention mechanism while at
the same time limiting the computational overhead. Using YOLOv8 as our baseline
model for the task of object detection we proceed further.

• **Dataset Preparation**

As mentioned before one of the major challenge faced for preventive maintenance using object detection in 
rolling stock images is the **low availability of data**
or images. Thus, to increase the amount of data available for training of an object
detection model (YOLOv8) we use certain data augmentation techniques so as to
generate images of **potential use-cases** that are observed in the setting of images for
rolling stock components. The images are augmented by **brightening/darkening** them,
introducing **gaussian noise, gaussian blur** and **rotating** the image.

Secondly, the images for rolling stock components generally **suffer from poor contrast
conditions**. So we also make use of certain image contrast enhancement techniques
like **Histogram equalization** and **Contrast Limited Adaptive Histogram Equalization
(CLAHE)**. Further we also analyse which contrast enhancement approach is giving
the best result for object detection using YOLOv8.

• **Incorporating Attention modules in YOLOv8 architecture**

The attention modules are used to improve the feature representation of deep
CNNs network. Here we are using the attention modules to improve the performance
of YOLOv8 for object detection tasks.

YOLOv8 architecture consists of **three components namely, the backbone, the neck
and the head**. The backbone is a deep learning architecture that extracts features at
various resolution levels, the neck combines the features extracted by the backbone
and the head is responsible for predicting the object classes and the bounding box
co-ordinates.

We are adding the attention modules to the neck of the YOLOv8 architecture as the neck combines the features from different levels of 
abstraction (as shown in the figure below) and are used to generate the final predictions. By introducing attention
mechanisms at this stage, the model can refine the feature representations and enhance the localization accuracy.

![image](https://github.com/user-attachments/assets/971f03c4-892f-4286-81ec-e1b08e9f15c2)

                  YOLO architecture with Attetion modules

The attention modules used are:
- ResBlock + Convolutional Block Attention module
- Global Attention module
- Efficient Channel Attention Module
- Shuffle Attention Module

• **Implementing using different YOLOv8 model size**

As a real time object detection approach for preventive maintenance using
rolling stock images, the **processing time** and the **computational load** on the edge devices at the 
customer site are certain parameters which are very critical for a choice of
a model for production, a comparative study is done using YOLOv8 nano and small
variant so as to analyse the trade-off between the performance improvement and the
increase in the inference time or the computational overhead.

Bigger variants of YOLOv8 (medium, large etc) were not considered as they are
too large for production.


**EXPERIMENTAL EVALUATION: Original Dataset**

• **How Image data is collected?**

![image](https://github.com/user-attachments/assets/07525019-872d-465e-a746-bc318b7cedea)

          A site view showing the cameras, sensors and edge devices setup


• **Original Dataset Details**

The dataset used consists of images of **Extreme Guiding components**. The
Extreme guiding components connect the wagon (bogie) with the locomotive (engine).
The images are captured from two camera views namely the **Control Arm Bolt View** and the **Side view**.

![image](https://github.com/user-attachments/assets/5e05291a-2704-4ad8-8abd-77556e79643c)

![image](https://github.com/user-attachments/assets/63eb0f80-9941-4470-a2d9-40b12603ef16)

The original dataset consists of a total of **111 images** having **9 object classes**
namely, Arm nut, Bolt Thread, Horizontal Nut, Security Plate Bolt, Top Security
Plate, Top Security Wire, Vertical Bolt, Vertical Nut and Washer. 

![image](https://github.com/user-attachments/assets/c76acded-3b94-47e3-be97-bb2b52ba8f04)

![image](https://github.com/user-attachments/assets/dcb56b18-848e-47b5-92cc-f941af037c73)


• **Object Detection using YOLOv8 nano and small models on the original dataset**

Object Detection by training the YOLOv8 nano and small model on the original
dataset with a 80:20 train-validation split gives the result as shown in the following table


![image](https://github.com/user-attachments/assets/f1fa6577-8106-42f2-9139-980aaaf5478f)

