## TRC 5901: How deep is too deep?

**Project description:** This is a project to wrap up a Level 5 unit in the Monash School of Engineering. The purpose of this project was to provide us students a simple research project studying the effects of varying convolution layers on the prediction accuracies of a model. To test our skills on verbal and written communication, the project required 2 final submissions: a final written report intended for a technical audience and a 3 minute video pitch intended for a general audience. 

### Objectives

- Apply deep learning theory to optimise a deep learning model for object classification.
- Gain experience in using open access tools, such as TensorFlow and PyTorch, in solving computer vision problems.
- Study the effects of *presence of data pre-processing, optimiser selection, and fully-connected layer design, convolutional and pooling layers built* on classification prediction. 

### Methods
#### 1. Load CIFAR-10 dataset from the KERAS library
It has 60 000 labeled images of 10 classes, already split into 50 000 for training and 10 000 for testing. Each coloured image has a resolution of 32x32 with 3 channels for red, green and blue colours. 

#### 2. Extract validation datset from testing dataset
The 10 000 images from the original testing dataset was further randomly split into 7000 images for validation and the
remaining 3000 for new testing data.

<img src="images/TRC5901_Project_img1.png?raw=true"/>

It is good practice to do this because the model would be trained to generalize better, avoiding overfitting. This process was done using PyTorch's `random_split()` function, which allows manual allocation of seed. For training purposes, the same seed number of **42** was used throughout this project.

#### 3. Define baseline model
A basic CNN model was first built to serve as a baseline. At each stage, slight modifications are applied to this baseline model to study how it affects the prediction accuracy. 

<img src="images/TRC5901_Project_img2.png?raw=true"/>

Design of baseline model:
- 1 Convolutional (Conv.) Layer + 1 Dense Layer
- Optimiser: Stochastic Gradient Descent (SGD)
- Loss calculation: Sparse Categorical Cross Entropy
- Learning rate: 0.01 (Default)
- Momentum: 0 (Default)

#### 4. Study effects on changed variables 
    <Proofread pls>
    After each modification to the baseline model, the best modified model was selected to be used in the next level of testing.
#### *4.1 Data pre-processing*
#### *4.2 Optimiser selection*
#### *4.3 Fully Connected layers*
#### *4.4 Convolutional and Pooling layers*






### 5. Best model

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. 

```javascript
if (isAwesome){
  return true
}
```

