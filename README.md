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
dataset with a 80:20 train-validation split gives the result as shown in the following table:


![image](https://github.com/user-attachments/assets/f1fa6577-8106-42f2-9139-980aaaf5478f)

![image](https://github.com/user-attachments/assets/5136f417-fad0-42f7-b3d5-0ebe915d4089)

      Precision-Recall curve for YOLOv8 nano model for original dataset

![image](https://github.com/user-attachments/assets/b6a2cc19-58e5-463b-9a54-af726c33b121)

       Precision-Recall curve for YOLOv8 small model for original dataset

The models are not giving very good overall performance on the original dataset and
give extremely **poor performance** for 3 particular object classes: **Bolt Thread, Security Plate Bolt and Top Security Wire**.

As a product for object detection in extreme guiding components of rolling stock,
the model should give good performance for all of the object classes.



**DATA PREPARATION PIPELINE: Extended Dataset**

As our dataset is very small, to extend the dataset, augmentation techniques
were used to generate potential use cases that are observed in images of rolling stock
components. Also, the augmentation of training and validation set is done separately
so as to avoid any data leakage.

Further to find the optimal pre-processing technique we generate 3 sets of data, normal, 
histogram equalized and contrast limited adaptive histogram equalized.

The Testing set is taken from a batch of data different from the original dataset,
obtained at a later time. The **data preparation pipeline** is shown in the figure below:

![image](https://github.com/user-attachments/assets/936e788d-1b70-4358-8109-b02e7523ea70)

The extended dataset’s **train, validation and test split** and the **object class data distribution** is shown in the table 
and figure below respectively:

![image](https://github.com/user-attachments/assets/ac2ccc6e-4257-435c-bfc0-3d940659204e)

![image](https://github.com/user-attachments/assets/fc424858-c3bd-4562-83a1-328793a0bc2f)


**EXPERIMENTAL EVALUATION: Extended Dataset**

• **Finding the Optimal Image Contrast Enhancement Technique**

Since the images for the rolling stock generally suffer from poor contrast, thus
for pre-processing contrast enhancement techniques are being considered to improve
the object detection performance of YOLOv8 model.

Two techniques were considered namely **Histogram Equalization** and **Contrast Limited Adaptive Histogram Equalization (CLAHE)** and the performance of YOLOv8 object detection model both nano and small, were compared on all 3 generated dataset
(one normal and two enhanced).

• **YOLOv8 nano object detection results**

The results for YOLOv8-nano on the 3 datasets is shown in table along with
the class wise performance shown using precision recall curves
for normal, histogram equalized and clahe dataset respectively.

![image](https://github.com/user-attachments/assets/e446b2c4-b145-4ed7-b147-e5e6834d621a)

![image](https://github.com/user-attachments/assets/66900ecb-205e-4125-8baf-ce6894d7b540)

        Precision-Recall curve for YOLOv8 nano on HE dataset


• **YOLOv8 small object detection results**

The results for YOLOv8-small on the 3 datasets is shown in table along with the
class wise performance shown using precision recall curves
for normal, histogram equalized and clahe dataset respectively.

![image](https://github.com/user-attachments/assets/a5254432-62ff-457d-8471-79a81e29a1ca)

![image](https://github.com/user-attachments/assets/05a1ecf4-25aa-43eb-a560-86257cd6ed20)

      Precision-Recall curve for YOLOv8 small on HE dataset

Upon analysing it is seen that both YOLOv8 nano and small models produce best
overall and class wise results for **histogram equalized dataset**. Thus, for the extreme
guiding dataset histogram equalization is the best image pre-processing technique.


**QUANTITATIVE ANALYSIS of YOLOv8 Nano + Attention Modules**

This analysis is done using a histogram equalized dataset with the following tuned hyperparameters: Optimizer- Adam, Epochs- 150, 
Learning Rate- 0.001, Image-size- 960.

![image](https://github.com/user-attachments/assets/424d121b-f2f0-440d-9949-4c9ce072da82)

This table showcases the performance of YOLOv8 nano model with different attention modules. We can see that **YOLOv8 nano model with attention modules does not show any improvement over the baseline**.

**QUANTITATIVE ANALYSIS of YOLOv8 Small + Attention Modules**

This analysis is done using a histogram equalized dataset with the following tuned hyperparameters: Optimizer- Adam, Epochs- 150, 
Learning Rate- 0.001, Image-size- 960.

![image](https://github.com/user-attachments/assets/8a3dbcda-fb0e-40c8-add8-368caa9bb5fc)

This table showcases the performance of YOLOv8 small model with different
attention modules. We can see that the **ResBlock + CBAM** and the **ECA**
attention modules are **giving better overall mAP** than the baseline model.

**QUALITATIVE ANALYSIS on TEST SET using YOLOv8 small model**

Here we compare the qualitative performance of the **YOLOv8 small baseline**
model and the model utilizing the **ResBlock+CBAM attention** module.

Specifically we compare their performance on the **3 object classes** namely **Bolt thread, Top
Security wire** and **Security Plate Bolt**, which were initially very difficult to detect and
accurately localize.

![image](https://github.com/user-attachments/assets/32a4c2ce-8944-4cd6-b515-ea70087a77e5)

            Qualitative Results using YOLOv8 baseline

![image](https://github.com/user-attachments/assets/90a77793-23bb-4296-8be0-0ed21fe4aa31)

        Qualitative Results using YOLOv8 with ResBlock + CBAM attention

From the figures we can see that even though the **baseline model** is able to detect
all the 3 object classes but it is not able to do so with good localization accuracy as
we can see that it gives multiple bounding boxes for the same object. On the other
hand the **YOLOv8 model with ResBlock + CBAM** attention module gives **better confidence score** and
**shows far greater object localization accuracy**.

**CONCLUSION**

• **Histogram Equalization** is the best image contrast enhancement technique for
the extreme guiding dataset for object detection task.

• Adding attention modules to the YOLOv8 nano model didn’t result in any
improvement over the baseline model.

• As for the YOLOv8 small model, two attention modules ResBlock + CBAM 
and ECA showed better performance than the baseline model.

• The attention modules not showing any improvement for the nano model could
be due to the **model not being deep enough** to make the most out of the feature
extraction.

• **We also saw that though using attention modules improved the performance of
the model but it also caused a increase in the inference time**. Thus, there exists
a trade-off between performance enhancement and reducing the inference time
and subsequently the processing time of the model, and thus the choice of a
particular model depends on the requirements of the customer.
