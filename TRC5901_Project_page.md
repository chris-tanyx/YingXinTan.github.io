## TRC 5901: How deep is too deep?

**Project description:** This is a project to wrap up a Level 5 unit in the Monash School of Engineering. The purpose of this project was to provide us students a simple research project studying the effects of varying convolution layers on the prediction accuracies of a model. To test our skills on verbal and written communication, the project required 2 final submissions: a final written report intended for a technical audience and a 3 minute video pitch intended for a general audience. 

### Objectives

- Apply deep learning theory to optimise a deep learning model for object classification.
- Gain experience in using open access tools, such as TensorFlow and PyTorch, in solving computer vision problems.
- Study the effects of *presence of data pre-processing, optimiser selection, and fully-connected layer design, convolutional and pooling layers built* on classification prediction. 

### Methods
#### 1. Load CIFAR-10 dataset from the KERAS library
The CIFAR-10 dataset has 60 000 labeled images of 10 classes, already split into 50 000 for training and 10 000 for testing. Each coloured image has a resolution of 32x32 with 3 channels for red, green and blue colours. 

#### 2. Extract validation datset from testing dataset
The 10 000 images from the original testing dataset was further randomly split into 7000 images for validation and the
remaining 3000 for new testing data.

<img src="images/TRC5901_Project_img1.png?raw=true"/>

It is good practice to do this because the model would be trained to generalize better, avoiding overfitting. This process was done using PyTorch's `random_split()` function, which allows manual allocation of seed. For training purposes, the same seed number of **42** was used throughout this project.

#### 3. Define baseline model
A basic CNN model was first built to serve as a baseline. At each stage, slight modifications are applied to this baseline model to study how it affects the prediction accuracy. 

<img src="images/TRC5901_Project_img2.png?raw=true" height=300/>

Design of baseline model:
- 1 Convolutional (Conv.) Layer + 1 Dense Layer
- Optimiser: Stochastic Gradient Descent (SGD)
- Loss calculation: Sparse Categorical Cross Entropy
- Learning rate: 0.01 (Default)
- Momentum: 0 (Default)

#### 4. Study effects on changed variables 
New models, each a slight variant of the baseline model, was derived by either changing the hyperparameters or data-preprocessing methods. Each model variant was trained for a maximum of 20 epochs. The model's validation loss was caluclated by the end of each epoch and then compared to the lowest value from previous epochs. If there's an improvement in validation loss, the model trained up until the current epoch is saved as the new best model. 

This addresses the issue of overfitting which sometimes occur when the CNN is modelled too well to the training data. It is identifiable by a continuously dropping training loss while the validation loss remains stagnant or even increases.An example of of this is depicted in Figure 4. In case of overfitting, the model with the best performance before 20 epochs was used to evaluate the testing data.

<img src="images/TRC5901_Project_img3.png?raw=true"/>

To summarise, the changed variables studied in this project are data pre-processing methods, optimiser type, structure of fully-connected (FC) layers and also the structure of convulutional + pooling layers.  

#### *4.1 Data pre-processing*
A common practice to training predictive models are to perform data pre-processing on raw data. In this stage, 2 versions of the baseline model is used; one has the images undergo pre-processing and another doesn't. 

Pixel normalization was implemented to reduce training time and to help the model generalised better. Each pixel in a colour image was normalized from a range of 0-255 to 0-1. 

| Model  | Pre-processing Method | Train. Loss | Train. Acc. | Val. Loss | Val. Acc. | Test Loss | Test Acc. | No. of Parameters | Epoch Nr. |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 1  | None  | 2.30 | 9.8% | 2.31 | 11.2% | 2.30 | 9.0% | 923,914 | 12 |
| 2  | Pixel Normalisation  | 0.55 | 81.2% | 1.02 | 66.1% | 1.13 | 64.6% | 923,914 | 17 |

By comparing the values in the table above, it proves that ample data pre-processing greatly improves model predictions.

#### *4.2 Optimiser selection*
The learning rate determines how much the weight parameter updates itself during training using a gradient descent algorithm. In general, a learning rate that is too small makes model training computationally expensive but has a higher chance of arriving at a global minima of a loss function. Conversely, if the learing rate is too large, it is at risk of weights diverging from the global minima. 

<img src="images/TRC5901_Project_img4.png?raw=true"/>

By default, the learning rate and momentum of a SGD optimizer from the Keras library is 0.01 and 0 respectively. As the project task focuses on improving the classification accuracy and the maximum number of eopchs is a relatively small number of 20, the learning rate was reduced to 0.001 to converge at a point closer to the final minimum in the sparse cross-entropy loss function. In addition, the momentim is set to 0.9 to accelerate gradient vectors while optimizing the weight vector. 

| Model  | Hyperparameters | Train. Loss | Train. Acc. | Val. Loss | Val. Acc. | Test Loss | Test Acc. | No. of Parameters | Epoch Nr. |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 1  | LR = 0.01; α = 0  | 0.69 | 76.5% | 1.01 | 65.6% | 1.05 | 64.3% | 923,914 | 16 |
| 2  | LR = 0.001; α = 0.90  | 0.55 | 81.2% | 1.02 | 66.1% | 1.13 | 64.6% | 923,914 | 17 |

whereby LR : Learning Rate and α : Momentum

#### *4.3 Fully Connected layers*
The ability of a CNN to classify an image into one of the 10 classes in the CIFAR-10 dataset is attributed to fully connected or dense layeers. In general, the larger the depth of the hidden dense layers, the higher the model performance. However, if there are too many layers, it could compoud training time. For the purposes of this study, prediction performnace is championed over computational cost. 

Here's the tabulation of the perfomance metrics of models with incresing number of layers with some tweaking of neuron numbers in a layer in the last model. 

| Model  | Dense Layers | Train. Loss | Train. Acc. | Val. Loss | Val. Acc. | Test Loss | Test Acc. | No. of Parameters | Epoch Nr. |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 1  | FC1 (128)  | 0.55 | 81.2% | 1.02 | 66.1% | 1.13 | 64.6% | 923,914 | 17 |
| 2  | FC1 (128) + FC2 (128)  | 0.66 | 81.3% | 1.11 | 65.7% | 1.13 | 65.0% | 940,426 | 12 |
| 3  | FC1 (128) + FC2 (128) + FC3 (128)  | 0.32 | 88.9% | 1.37 | 64.5% | 1.38 | 63.6% | 956,938 | 12 |
| 4  | FC1 (128) + FC2 (120) + FC3 (84)  | 0.80 | 72.0% | 1.04 | 64.4% | 1.06 | 63.6% | 949,118 | 10 |

By comparing the validation loss of the first 3 rows, the values turns out do not align with the aforementioned generalised understanding of CNN depth in relation with model performance. This unexpected behaviour may be the result of limiting the maximum bumber of epochs to a relatiely conseticave 20 epochs as the parameters of this study. As the numer of dense layers increases, the model likely requres more time to optimise its parameters, hence 20 epochs may be insuffucent which results in an unoptimised model that makes poor predictions. 
 

#### *4.4 Convolutional and Pooling layers*






### 5. Best model

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. 

```javascript
if (isAwesome){
  return true
}
```

