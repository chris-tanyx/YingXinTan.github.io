## Undergraduate Research Opportunities Program (UROP) | An Extended Look on Subclinical Tremor Differentiation using AI

**On the (UROP)**

**Project description:** Tremor is observed at several body segments at regular and irregular oscillations, often involuntary in nature. A major symptom of common neurological movement disorders such as Essential Tremor (ET) and Parkinson’s Diseases (PD) are tremors, yet they are often still misdiagnosed. In the earlier stages, ET and PD tremors manifest as subclinical tremors, which are of amplitudes too low for clinical assessment. It can be measured using attitude and heading reference systems (AHRS) strapped on to a patient’s arms. The aim of the research is to utilize artificial intelligence (AI) to classify the subclinical tremors into normal, and PD tremors. Consistent accurate classification of low amplitude tremors by the AI architecture may allow for better diagnosis of PD and normal tremors. Subclinical tremors measured at different positions are fed into the network, designed based on a Long-Short Term Memory (LSTM) network. When data collected from a WING position are fed into the network, it yielded the highest accuracy of 78%. The outcome of this study suggests that with further improvements, this method can aid clinicians in differentiating between subclinical tremors. The environment used is MATLAB.

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
At least a month was dedicated to obtain background information on this project previously led by then PhD candidate, Gerard Ruchin Randil Nanayakkara. His paper Subclinical tremor differentiation using LSTM networks, co-written with Dr. Chan Ping Yi, largely informed the project pipeline for this research [3]. Hence part of the project scope was to expand the field of references beyond those already included in Gerard's paper. 

https://pubmed.ncbi.nlm.nih.gov/39992543/
### Results and Discussions

### References
[1]	Julián D. Loaiza Duque, Andrés M. González-Vargas, Antonio J. Sánchez Egea & Hermán A. González Rojas, "Using Machine Learning and Accelerometry Data for Differential Diagnosis of Parkinson’s Disease and Essential Tremor," presented at the Workshop on Engineering Applications, Santa Marta, Columbia, 2019. [Online]. Available: https://link.springer.com/chapter/10.1007/978-3-030-31019-6_32.

[2] Sanghee Moon, Hyun-Je Song, Vibhash D. Sharma, Kelly E. Lyons, Rajesh Pahwa, Abiodun E. Akinwuntan & Hannes Devos, "Classification of Parkinson’s disease and essential tremor based on balance and gait characteristics from wearable motion sensors via machine learning techniques: a data-driven approach", Journal of Neuroengineering and Rehabilitation, 2020. [Online] Available: https://link.springer.com/article/10.1186/s12984-020-00756-5

[3] Gerard Ruchin Randil Nanayakkara, Ping Yi Chan, "Classification of Parkinson’s disease and essential tremor based on balance and gait characteristics from wearable motion sensors via machine learning techniques: a data-driven approach", Journal of Neuroengineering and Rehabilitation, 2020. [Online] Available: https://link.springer.com/article/10.1186/s12984-020-00756-5


