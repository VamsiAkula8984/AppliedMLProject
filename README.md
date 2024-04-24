# AppliedMLProject
** Image Classification using CNN on Cifar10 Dataset **
## About the Dataset
- Name: CIFAR-10
- Number of Images: 60000(6000 images per class)
- Resolution: 32x32 RGB
- Number of classes: 10 [airplane, automobile, bird, cat, deer, dog, frog, horse, ship, truck]
-Here are the classes in the dataset, as well as 10 random images from each:
![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/c76221e9-0a91-4005-9980-a61eee9c9fe2)

- Train/Test Split: 50000/10000
- Dexsription: The dataset is divided into five training batches and one test batch, each with 10000 images. The test batch contains exactly 1000 randomly-selected images from each class. The training batches contain the remaining images in random order, but some training batches may contain more images from one class than another. Between them, the training batches contain exactly 5000 images from each class.
- More about the dataset in the following [link](https://www.cs.toronto.edu/%7Ekriz/cifar.html)
## plan
Given an image. We plan to predict whether the image belongs to either one of the 10 classes in CIFAR-10 dataset. In doing so, we will be trying to come up with a CNN architecture that can effectively predict to which an image belongs to.
## Process Overview
- From the title itself, it is evident that the model uses a CNN architecture to train the dataset. So, we decided to start with a simple CNN and later, add a combination of convolution and Maxpooling layers and tune hyper parameters to come up with the best model.
## Exploratory data analysis
- The X here is the 32x32 RGB pixel values of the image. A 3D numpy array. Y is a int label value corresponding to one of the 10 classes.
  ![image](https://github.com/VamsiAkula8984/AppliedMLProject/assets/149032259/b48c01d7-bf11-4a5d-b8d9-f699f3f4dc3f)
