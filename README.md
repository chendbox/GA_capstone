# GA_DSI_Capstone_Project

## Problem Statement
Pathology is the discipline of diagnosiing a disease mostly through analysis of tissue, cell and body fluid samples. In swine industry, the pathologists focus on the analysis of swine tissue sample. The examination starts with a necropsy. Chemical fixatives, like formalin are used to preserve the tissue from degradation until the specimen gets to the histology lab. After the staining process, the pathologists observe the slides under the microscope and give the diagnosis reports based on the morphologic changes on the cells. As we can see, the world population is 7.3 billons and the consumpation of pork is increasing year by year. With the industrial expansion, there is significant disease pressure on pig health. There are serveral diagnostic methods that can be used to tell the causes of the diseases, following with treatments. The histopathology is the golden standard and principle to make the final decision. However, there is not enough patholgists around the world to support animal health industry. With the quick expansion of swine industry, pathologist support is far behind the level of health satisfaction. This issue is getting worse since the number of pathologists is predicted to decrease. According to one study, by 2030 the number of active pathologsits may drop by 30 percents compared to 2010 levels. If there are no effective proposed solutions, the pig health is in danger and the swine industry could be deadly impacted by diseases. 
Histopathology images as well as whole slide imaging makes the images online and pathologists can reveiw anywhere. However, with the limitation on capacity, there is nothing the pathologists can do to read thousands images in a single day and that's definitley the number industry wants yesterday. We leverage the deep learning power and try to set up a covolutional nerual network model to let the algorthim train the computer to read the images and make a prediction. This will significantly improve the diagnosis capacity and meet the industry requirements. 

## Contents
| File/Folder | Description |
| --- | --- |
| images (copy) | no permisson to release |
| notebook | the jupyternotebook includes the data loads, data clean, EDA, Modeling to answer the problem statement |
| PPT | PDF of presentation slides |

## Workflow
**1. Data Collection and Cleaning**<br>
All the WSI images are from a veterinary pathologist - Dr. Paulo Arruda from AMVC, Ames, Iowa. The images contain 210 normal pig lung images and 44 H1N1 swine influenza virus lesioned lung images from different pigs (# unknown). Since these images with uniform size 3585 X 2748 RGB, my Mac can't hold that sized data(restricted by computer capacity), I downsized the images to 100X 100 size RGB. In pathologists point of view, they want to find the lesion impacted marphorlogical changes in cell and tissues with as much as clear images(aka. big enough). In Data Scientist opinions, we will extact as much feature as we can to do the modeling, tune hyperparameters and check the scores. 

**2. EDA**<br>
The images contain 210 normal lung images and 44 disease lung images. The WSI pixel intensity indicates the Red color dominate. The final data dimensions are 100 X 100 X 3.There was imbalanced labels, and I used randomoversampler methods to bring the labels back to even.

**3.Modeling**<br>
The input layer filled with images. Used CNN model with padding and pooling open to extract features. Also set te flatten layer before the fully connected layers. It's a binary classification problem, so I use sigmoid as activation fuctions. Relu used in all input, hidden layers.


**4.Results**<br>
binary classification entropy, val loss used to evalute the train and test sets. accuracy is important evalutor as well. Other metircs precision, recall, f1-score are all included in the evaluation. Confusion matrix is made at the end.

## Executive Summary
I collected 254 images total, with 210 normal and 44 disease images from pathologists. 
Total number of images: 254
Number of Normal Images: 210
Number of Lesion Images: 44
Percentage of positive images: 17.32%
Image shape (Width, Height, Channels): (100, 100, 3)
I downsized the iamges from 3585 X 2748 RGB to 100 X 100 RGB. In order to reduce noise and overfit, I updated the label class weights, from imbalanced 0.6, 2.9 to new class weights, 1. 1. through RandomOverSampler. I used two convolutional layers as well as the padding and pooling to extract the features from the images. Kernel size set up in 3X3 to match the RGB channels. Dropout ratio 0.25 before the fully connected layers. All the activation fuction in input and hidden layers is Relu and sigmoid at output layer, along with a epochs50, batchsize=256, and early stop with patience at 10. In short, 1 input layers, 3 hidden layer + 2 convolutional nerual network layers + 4 hidden layers + 1 output layers is the model. Total params is 494,430 and trainalbe params is 494,430. 
we focused more on accuracy, since the patient can't afford false negative senario. Our accuracy is 95.6%, beat the patholgist expectation at 85% accuracy. 0.96 recall, 0.96 f1-score. Our confusion matrix indicated there are 4 false postive case out of 90 samples. 

**Conclusion**<br>
We can build a CNN model to classify WSI images, with an accuracy of 95.56%, beat client’s expectation of 85%.
The machine learning model can support pathologists to improve the work  accuracy and capacity on diagnosis.
More images should be involved in lesion groups (up to 200) to balance the data.
Object detection to frame the interested area to reduce noise and improve the accuracy.
Feature works would be conducted by classifying influenza subtype images as well as commingle swine diseases (Multiclassification).

**Reference**<br>
https://www.hollisnh.org/sites/g/files/vyhlif3271/f/uploads/swine_flu_fact_sheet.pdf
https://www.cdc.gov/h1n1flu/estimates/april_february_13.htm
https://journals.asm.org/doi/10.1128/JVI.01211-10#F1
Park S, Parwani AV, Aller RD, et al. The history of pathology informatics: a global perspective. J Pathol Inform.2013;4:7; doi: 10.4103/2153-3539.112689.
Robboy SJ, Weintraub S, Horvath AE, et al. Pathologist workforce in the United States, I: development of a predictive model to examine factors influencing supply. Arch Pathol Lab Med. 2013;137(12):1723–1732; doi: 10.5858/arpa.2013-0200-OA.
Source: www.clpmag.com
https://www.sciencedirect.com/science/article/pii/S2352914819301133
