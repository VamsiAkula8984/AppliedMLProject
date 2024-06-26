# AppliedMLProject
# **Image Classification using CNN on CIFAR-10 Dataset**
## About the Dataset
- Name: CIFAR-10
- Number of Images: 60000(6000 images per class)
- Image Size: 32x32x3
- Number of classes: 10 [airplane, automobile, bird, cat, deer, dog, frog, horse, ship, truck]
![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/c76221e9-0a91-4005-9980-a61eee9c9fe2)

- Train/Test Split: 50000/10000
- Description: The dataset is divided into five training batches and one test batch, each with 10000 images. The test batch contains exactly 1000 randomly-selected images from each class. The training batches contain the remaining images in random order, but some training batches may contain more images from one class than another. Between them, the training batches contain exactly 5000 images from each class.
- More about the dataset in the following [link](https://www.cs.toronto.edu/%7Ekriz/cifar.html)
## plan
Given an image. We plan to predict whether the image belongs to either one of the 10 classes in CIFAR-10 dataset. In doing so, we will be trying to come up with a CNN architecture that can effectively predict to which class the image belongs to.
## Process Overview
- From the title itself, it is evident that the model uses a CNN architecture to train the dataset. So, we decided to start with a simple CNN and later, add a combination of convolution and Maxpooling layers and tune hyper parameters to come up with the best model.
## Exploratory data analysis
- The X here is 32x32x3 dimensional image, a 3D array. Y is a int label value corresponding to one of the 10 classes.
  ![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/b48c01d7-bf11-4a5d-b8d9-f699f3f4dc3f)
- The CIFAR-10 dataset is balanced . Each class has 6000 images of which 5000 images are used to train and 1000 images are used to test the model.
- Because of the fact that that we only have one feature, there is no question of multiple features co-related.
### Feature Engineering:
- To expedite the training process, all pixel values are normalised to 0 - 1.
  ![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/e1e420ed-d4af-4b3a-b1d7-8f5d4068b637)
- Each Y label corresponds to a class ranging from 0 to 9. Hence a list named 'classes' is mapped to each of the ten class categories for easy readability during prediction.
  ![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/ac9187a1-678f-4b14-8067-f172e6513594)
## Model Fitting
### Train / test splitting
The train / test split for CIFAR-10 dataset is already standardised. The dataset is divided into five training batches and one test batch, each with 10000 images. The test batch contains exactly 1000 randomly-selected images from each class. The training batches contain the remaining images in random order, but some training batches may contain more images from one class than another. Between them, the training batches contain exactly 5000 images from each class.
### Models trained
- #### Model with two (Convolution + maxpooling) layers and two dense layers with dropout layer
![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/0b8865d0-c2d9-4f7a-98c7-a7cc293628ff)

We started implementing a basic CNN architecture with epochs=10, batch_size=64, validation_split=0.2. With the number of epochs being low, the model fails to predict and its right to say that the model is overfit. We can see below that the model's training accuracy is far less than validation accuracy which is clear indication of model being overfitted.
![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/bdcbf9b8-a765-4c36-837c-de448f754f68)

- #### Model with four (Convolution + maxpooling) layers and three dense layers with dropout layer
![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/22300616-6b91-4ecf-b571-32427f888c20)

Now, to improve the accuracy, the model is now trained with epochs=20, batch_size=64, validation_split=0.2. Two additional convolution layers and a dense layer is added to capture the underlying patterns. From the accuracies below, its evident that the model is overfit. There is a huge difference between training accuracy and validation accuracy which means that the model fails to predict unseen data.
![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/a1dffed2-856a-41e3-ad31-94cef419948c)

- #### Model with three (Convolution + maxpooling) layers and three dense layers along with batchNormalization and dropout layer
![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/12914fed-1727-42e0-8750-9dc66b197511)

One of the advantages of using batch normaliation is the Regularization Effect. Batch normalization acts as a form of regularization by adding noise to the activations, which can help prevent overfitting. Hence to minimise the overfitting in the model, a batch normalisation layer is added. The model is now trained with epochs=20, batch_size=50, validation_split=0.2. The model ends up with a training accuracy of 81.69% and validation accuracy of nearly 70.6%. The test accuracy of the model is 70.3%. Clearly this model performs well when compared to other models.
![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/d5e472a9-33c9-42ca-8a90-2a36aaa0a43b)
![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/5f16a96b-bbfa-46a8-ac0a-62a69f5b55c4)

## Validation / metrics
- The metric we mostly relied on in determining the model architecture is its accuracy - The train and the validation accuracy. We considered the fact that the model performs well when there is less gap between train and validation accuracies.
  
![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/61c58cd3-a394-4454-8df5-cbd1739feeaa)

- Confusion Matrix
![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/683f2ba9-1af5-4eaa-9ecc-a97051de0d3b)
  - Inference from Confusion Matrix
      - Model fails to distinguish between [cats and dogs], [automobiles and trucks] and [birds and aeroplanes]
      - Model often misclassifies bird as deer. This is observed when the bird looks like an Ostrich.
      - Model also misclassified dog as horse.
      - THe model performs well in predicting data from ship and automobile classes.

- Man vs Machine
We have selected 20 images where the model fails to predict from the confusion matrix and asked 16 people to identify the images. The below images shows the comparison between human and model choice.

![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/2e6e536f-d4f8-4735-9888-c515f780b07c)
![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/6a198021-c6f1-4e32-b1cb-5b84e3a1ac02)
![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/10eecc09-9b02-4b71-8373-2a3f034db6e4)
![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/ef0173d8-3932-4363-9ce1-68aaa30f02bf)
  - it is observed that 20% of time people failed to properly identify the image.
  - 60% of time, people identified the images with 60-80% accuracy.
  - the remaining 20% of time people perfectly predicted the images where the model failed.
  - In conclusion we can say when considering the instances where our model fails, it is considerably difficult for people to identify the image.
  - Therefore, the model is working with acceptable performance.

## Improvements
- The main drawback of this model can be found in images with low quality. This model can be bettered with better quality images.
- We can also try to increase the number of images in the dataset by applying image augmentation techniques like scaling, rotations etc on the images.
