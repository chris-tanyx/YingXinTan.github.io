## TRC 5901: How deep is too deep?

**Project description:** This is a project to wrap up a Level 5 unit in the Monash School of Engineering. The purpose of this project was to provide us students a simple research project studying the effects of varying convolution layers on the prediction accuracies of a model. To test our skills on verbal and written communication, the project required 2 final submissions: a final written report intended for a technical audience and a 3 minute video pitch intended for a general audience. 

### Objectives

- Apply deep learning theory to optimise a deep learning model for object classification.
- Gain experience in using open access tools, such as TensorFlow and PyTorch, in solving computer vision problems.
- Familiarise commonly used labelled image classification data such as CIFAR-10. 

### Methods
#### 1. Load CIFAR-10 dataset from the KERAS library
It has 60 000 labeled images of 10 classes, already split into 50 000 for training and 10 000 for testing. Each coloured image has a resolution of 32x32 with 3 channels for red, green and blue colours. 

#### 2. Extract validation datset from testing dataset
The 10 000 images from the original testing dataset was further randomly split into 7000 images for validation and the
remaining 3000 for new testing data.

<img src="images/TRC5901_Project_img1.png?raw=true"/>

It is good practice to do this because the model would be trained to generalize better, avoiding overfitting. This process was done using PyTorch's `random_split()` function, which allows manual allocation of seed. For training purposes, the same seed number of **42** was used throughout this project.

#### 3. ffff



```javascript
if (isAwesome){
  return true
}
```


### 4. Provide a basis for further data collection through surveys or experiments

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. 

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).
