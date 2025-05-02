## Undergraduate Research Opportunities Program (UROP) | An Extended Look on Subclinical Tremor Differentiation using AI

**On the UROP:** Junior engineering students who achieved certain academic prerequisites set by the faculty were eligilbe to apply for research projects with the researchers of the university starting from their 2nd year of studies as an auxilliary activity to gain early first-hand experience on academia-level research. Within the span of 1 year, students planned, conducted and presented their experiments to the academic staff. My project supervisor was Dr. Chan Ping Yi, lecturer at Monash University, experienced in the field of biomechanics.     

**Project description:** Tremors are observed at several body segments at regular and irregular oscillations, often involuntary in nature. A major symptom of common neurological movement disorders such as Essential Tremor (ET) and Parkinson’s Diseases (PD) are tremors, yet they are often still misdiagnosed. In the earlier stages, ET and PD tremors manifest as subclinical tremors, which are of amplitudes too low for clinical assessment. It can be measured using attitude and heading reference systems (AHRS) strapped on to a patient’s arms. The aim of the research is to utilize artificial intelligence (AI) to classify the subclinical tremors into normal, and PD tremors. Consistent accurate classification of low amplitude tremors by the AI architecture may allow for better diagnosis of PD and normal tremors. Subclinical tremors measured at different positions are fed into the network, designed based on a Long-Short Term Memory (LSTM) network. When data collected from a WING position are fed into the network, it yielded the highest accuracy of 78%. The outcome of this study suggests that with further improvements, this method can aid clinicians in differentiating between subclinical tremors. The environment used is MATLAB.

**KEYWORDS:** Parkinson’s Disease, Essential Tremor, Subclincal tremor, Artificial Intelligence, LSTM networks, MATLAB. 
 

### Introduction

Essential Tremors (ET) and Parkinson’s Disease (PD) are amongst the most prevalent neurological diseases amongst adults. As of date, a patient is diagnosed with either of these diseases by movement disorder specialists who would deliver a diagnosis upon studying a patient’s medical history and repeated clinical analysis of the tremors. This process could take up to a year yet despite that, these diseases can be misclassified up to 25% of the time because of the overlapping characteristics. The current method of neurological diseases detection could deter early prevention and treatment which could be detrimental for both ET and PD patients with rapid and progressive symptoms.  

Previous works have ustilised Artificial Intelligence (AI) and Machine Learning (ML) algorithms, used in conjunction with sensors and signal processing methodologies, to classify visible tremors. Examples are such as artificial neural networks and also deep learning methodologies like convolutional neural networks (CNN) and recurrent neural networks (RNN) [1, 2]. Sanghee Moon et el also compared the accuracy of predictions of different machine learning models, including gradient boosting, random forest, support vector machine and several others. The study found that neural networks yielded the highest accuracy for differentiating between healthy patients and those with pathological tremors. Julian et el whereas tested different combinations of algorithms and extracted features extraction and concluded that the right features should be extracted for accurate tremor classification [1]. However, these previous works have primarily focused on categorising visible tremors, amongst other symptoms exhibited by PD and ET patients. 

An alternative symptom to use in machine learning tremor classification are subclinical tremors. These are tremors with low amplitude and manifests in a much larger percentage of the population. 30% of PD patients display only subclinical tremors and non-visible tremors. Compared to visible tremors, a ML model built on subclinical tremors have yet to be heavily developed, but it has potential to aid clinicians in early detection and treatment. 

This research project aims to use a new combination of artificial intelligence methodologies including LSTM networks and deep learning methodologies to differentiate between the pathological subclinical tremors. It focuses on differentiating between PD and normal patients because they have subclinical tremors while others ET doesn’t.

### Objectives
- Refine a machine learning algorithm that can categorise subclinical tremors.
- Achieve > 65% categorisation accuracy with a focus on differentiating between normal patients and those with PD. 
- Pick up new toolboxes to aid in MATLAB data analysis. 
- Allow Year 2 students (myself) to familirise themselves with the structure of designing, planning, executing and documenting an academic research. 

### Methodology
#### 1. Literature Review
At least a month was dedicated to obtain background information on this project previously led by then PhD candidate, Gerard Ruchin Randil Nanayakkara. His paper Subclinical tremor differentiation using LSTM networks, co-written with Dr. Chan Ping Yi, largely informed the project pipeline for this research [3]. Hence part of the project scope was to expand the field of references beyond those already included in Gerard's study. 

From the literature review, it was decided to proceed with the method of feature extraction of short-time Fourier transform (STFT). As for the classifiers, both artificial neural networks (ANN) and LSTM networks were compared for accuracy but ultimately LSTM was selected due to better performance. 

A large reservoir of data was passed down to me when I started working on it. These are tremor data amassed from patients already clinically diagnosed classified with either essential tremors, Parkinson’s or normal. It was measured using 3 MEMS AHRS attached along 3 parts of a patient’s arm – back of hand, distal lower end, Upper lower end. The sensors inside these devises outputs the acceleration, angle, change in magnetic field and the 3d orientation data; only the orientation data, stored as quaternion was used in this research. 

<p align="center"><img src="images/UROP_img1.png?raw=true"/></p> 

Then comes determining whether the tremor is subclinical or not. The relative hand-arm movements are expressed in joint angles. And using the equation below, the tremor rating is calculated. A rating value of less than 0.5 is subclinical, conversely would be clinical tremors. After separating the data, the tremor of clinical tremors were selected for this research.<br>

```math
Tremor\,rating = 2.6496 + 0.3071*log\,\theta_{W FE_{RMS}} + 0.0731*log\,\theta_{W AA_{RMS}} + 0.1843*log\,\theta_{E PS_{RMS}} + 0.0988*log\,\theta_{E FE_{RMS}}
```
#### 2. Processing Data and Model Training
**Reading Data** </br>
The sensor data was already in .xls format for ease of reading in MTALAB. The first part of the code reads the directory and file name of all the available data sets. It filters out incomplete, or faulty data sets or data, then extracts out the time and quaternion data, strong them into data structures. During this process, the code simultaneously stores the file names and location also in said data structure.

**Cartesian Conversion** </br>
The table with all the measured data is now separated into 2 separate arrays of time data and quaternion data. Then the array with quaternions is transformed into cartesian coordinates using the “rotatepoint” function. These arrays have 3 dimensions, the first two indicates the number of rows and columns respectively. And the last one is the total number of essential and normal patient’s data is currently used. After which, all the amplitude data was normalised to start t = 0 and their amplitudes are calculated. Raw positional data often has missing datapoints, which results in discontinuity in time series data, affecting results of any further data processing. Hence, a cubic interpolation function was applied to estimate missing datapoints.

**Bandpass STFT** </br>
<p align="center"><img src="images/UROP_img2.png?raw=true"/></p>
<p align="center"><img src="images/UROP_img3.png?raw=true"/></p>
The 2 figures above are to observe the effects of data pre-processing with (top) and withouth (bottom) bandpass filter. When the signal has been passed through the bandpass filter, the output signal has smaller amplitudes in general and oscillates around x = 0 axis while without the bandpass filter, the data increases from 0 and doesn’t oscillate. The range of the bandpass filter applied here is 3-30Hz, which is a range selected from research that indicates that the frequency range for low amplitude subclinical tremors are typically within <strong>3 to 9Hz for Parkinson’s Disease patients</strong> and <strong>4 to 14 Hz for essential tremor patients</strong> and up to <strong>30Hz for normal patients</strong>. 

Therefore, this comparison proves that bandpass filtering is required to remove any noise and irrelevant datapoints from the processed data. 

```matlab
% for R2 data padded + bandpass
for c = 1 : z
    amp_Rest2_nc(:,1,c) = bandpass(amp_Rest2_padded(:,1,c),[3 30],100);
    amp_Rest2_nc(:,2,c) = bandpass(amp_Rest2_padded(:,2,c),[3 30],100);
    amp_Rest2_nc(:,3,c) = bandpass(amp_Rest2_padded(:,3,c),[3 30],100);
end
```

**Padding and Interpolation** </br>
Front and back zero padding was added to the normalised positional cartesian data, so that the abrupt start and ending point amplitudes are zeroed or excluded from the tremor signals. This helps to avoid sudden peaks in positions that often arise in signals at the start and end of a motion. 

For funsies -- I mean clarity -- a comparison was done between different combinations of data preprocessing to determine the optimum combination. 
<p align="center"><img src="images/UROP_img4.png?raw=true"/></p>
From the figure above, it demonstrates that by applying only padding (a), or only interpolation (b), these unwanted spikes can be removed in the final output signal, which is (c), as seen by comparing the parts of the signal that are circled in purple. 

<p align="center"><img src="images/UROP_img5.png?raw=true"/></p>
Now this graph plots the sensor data of another patient's movement. The individual effects of what padding and interpolation does is clearer in this figure than the previous one. After comparing the parts of the signal circled in orange, it shows the effects of interpolation in smoothing the shape of the curve and that of padding is shown in the purple circled section. As seen in (b), some of the unwanted spikes are removed when only interpolation is applied, and a similar case can be observed in Figure 4(a) when only padding is applied. Therefore, it is concluded that both interpolation and padding should be applied to the signal after bandpass filtering (refer plot (c)) to mitigate the effects of errors during data measurement and collection. 

```matlab
%% Interpolating
[x,y,z] = size(cart_H_Rest2);

for c = 1 : z
    tq(:,1,c) = time_Rest2(1,1,c):5:13000; % Change resolution to 1ms
    amp_Rest2_int(:,1,c) = pchip(time_Rest2(:,1,c),amp_Rest2(:,1,c),tq(:,1,c));
    tq(:,2,c) = time_Rest2(1,2,c):5:13000;
    amp_Rest2_int(:,2,c) = pchip(time_Rest2(:,2,c),amp_Rest2(:,2,c),tq(:,2,c));
    tq(:,3,c) = time_Rest2(1,3,c):5:13000;
    amp_Rest2_int(:,3,c) = pchip(time_Rest2(:,3,c),amp_Rest2(:,3,c),tq(:,3,c));
end

%% Padding
[x,y,z] = size(cart_H_Rest2);
 
amp_Rest2_padded = zeros(x+1,y,z);

for c = 1 : z
    amp_Rest2_padded(2:x+1,1,c) = amp_Rest2(:,1,c);
    amp_Rest2_padded(1,1,c) = amp_Rest2(1,1,c);
    amp_Rest2_padded(2:x+1,2,c) = amp_Rest2(:,2,c);
    amp_Rest2_padded(1,2,c) = amp_Rest2(1,2,c);
    amp_Rest2_padded(2:x+1,3,c) = amp_Rest2(:,3,c);
    amp_Rest2_padded(1,3,c) = amp_Rest2(1,3,c);
end

```
With that settled, feature extraction from the cleaned positional data was done using STFT and then interpolation again over regions of discontinuity. The effects of a bandpass filter, interpolation and padding were also observed on the extracted features post-STFT as visualised in the spectograms below.  

<p align="center"><img src="images/UROP_img6.png?raw=true"/></p>

The key findings of this exercise are as such: 
- Without filtering out any frequencies, it would lead to all the amplitudes of movements concentrated at close to frequncies of 0 Hz. This is because the STFT transforms all signals including any noise and unwanted spikes in sensor data. Skipping this step would render the output of feature extraction not usable. 
-  Input data should be interpolated and padded so that datapoints have a large distinction between points of higher and lower amplitude and are more concentrated at a certain frequency. Thereby making it easier to pinpoint the corresponding frequencies at which maximum amplitudes occur.


**Convolutional + LSTM Model Building** </br> 
Separate the datapoints into set for training and set for testing and organise them into structs. Determine the y label at this point and store in categorical arrays. Next, use the Network Fitting tool from the Network Fitting Toolbox. The parametrers are as such:

```matlab
inputSize = [3531 1 1]; % determined by the percentage of data selected for training. Optimal number is referenced from previous analysis on subclinical tremors
filterSize = [1 20]; % suggested values from matLab
numFilters = 30; % suggested values from matLab
numHiddenUnits = 50; Optimal number is referenced from previous analysis on subclinical tremors
numClasses = 2; % suggested values from matLab
hiddenlayersize = 10 % suggested values from matLab
```
**Deep Learning Net Model** </br> 
Similar to Convplus lstm, but meant for testing. Building a convolutional + LSTM model from scratch is a rather manual process. Whilst it allows room for perfect customisation, it requires many functions to be self-written as well. MATLAB has helpful built-in functions in their Deep Learning Toolbox so that was explored as well. For testing the trained model, the parameters were set as above and along with the built model, it was fed into the Deep Learning Net feature to allow the model to train until a user-defined max. number of epochs or until prediction analysis stabilises to a user-specified minimum threshold, whichever comes first. 


### References
[1]	Julián D. Loaiza Duque, Andrés M. González-Vargas, Antonio J. Sánchez Egea & Hermán A. González Rojas, "Using Machine Learning and Accelerometry Data for Differential Diagnosis of Parkinson’s Disease and Essential Tremor," presented at the Workshop on Engineering Applications, Santa Marta, Columbia, 2019. [Online]. Available: https://link.springer.com/chapter/10.1007/978-3-030-31019-6_32.

[2] Sanghee Moon, Hyun-Je Song, Vibhash D. Sharma, Kelly E. Lyons, Rajesh Pahwa, Abiodun E. Akinwuntan & Hannes Devos, "Classification of Parkinson’s disease and essential tremor based on balance and gait characteristics from wearable motion sensors via machine learning techniques: a data-driven approach", Journal of Neuroengineering and Rehabilitation, 2020. [Online] Available: https://link.springer.com/article/10.1186/s12984-020-00756-5

[3] Gerard Ruchin Randil Nanayakkara, Ping Yi Chan, "Subclinical tremor differentiation using LSTM networks", Phys Eng Sci Med, 2025 Feb 24. [Online] Available: https://pubmed.ncbi.nlm.nih.gov/39992543/

