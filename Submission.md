
### Dataset Analysis
Code - https://www.kaggle.com/code/shukradityabosevit/ham10000-analysis-and-model-comparison/edit
##### HAM10000 
Composed of 10015 dermatoscopic images of pigmented skin lesions. The data was collected from Australian and Austrian patients. The participating institutes were : Cliff Rosendahl in Queensland, Australia, and Medical University of Vienna, Austria. The data set was classified into seven classes. The metadata includes information regarding patient age, sex, lesion location and diagnosis label.
Overall in the dataset, there are:
- 10015 samples
- 10 features
- 0 duplicate entries
- 57 null entries, amounting to 0.6% of the total rows.
A quick read of the csv file tells us that the 57 null entries are for age only.
For the major part, the data is clean and is ready to use.
For some lesions, there must be more than one image as lesion and image ID do not match. The uniques columns also indicate the number of classes and how sex, age and localisation features were organised.
- Majority of the diagnosis is via histopathology.
- Most of the samples in the dataset(approximately 67%) were of Melanocytic Nevi, followed by melanoma, benign keratosis-like lesions, basal cell carcinoma, actinic keratoses, vascular lesions and the least being Dematofibroma.
- Male samples were slightly more than the females (55% to 45%).
The predominating age group was 40-55 years. 
The number of samples rise rapidly after 25 years of age. 
###### Melanoma
Focusing on Melanoma, the predominantly affected gender was male with over 60% reported cases to be male.
However, it's predominant in females until 45 years. From 45 years, it starts peaking in males, reaching a much higher peak at 70 for males than the female peak at 55 or 70.
The dataset reveals that the highest chances of melanoma are in the back, upper and lower extremities. No correlation was found between exposure to sun as hand, ear, neck scalp have some of the lowest occurences.

#### Why is RandomOverSampler used?
Because of the vast difference in the quantity of data available for each class, we balance/augment the data by using RandomOverSampler(). THis brings up the number of images to that of the largest class ie class 4 - Melanocytic Nevi here.

![[Pasted image 20230812160440.png]]
![[Pasted image 20230812160500.png]]



### Proposed Method 1(Xception)
We are going to use Convolutional Neural Networks implemented in the form of the "Xception" network model. The design of the Xception network is similar to the predecessors ie Inception and ResNet networks, all of which use skip connections and multiple convolutional and max-pooling blocks in each layer.
The Xception architecture is a linear stack of depthwise separable with residual connections.
Xception architecture is a convolutional neural network based entirely on depth-wise separable convolution. Composed of 36 convolutional layers forming the feature extraction base of the network. It is structured into 14 modules, all of which have linear residual connections around them, other than first and last modules.

Why use the Xception instead of the Inception v3?
- Since the Xception has same number of parameters as the Inception V3, the performance gains are due to more efficient use of model parameters. 
- architecture very easy to define and modify with about 30-40 lies of code using high level library such as Keras/ Tensorflow-Slim. Similar to VGG16
#### Design of the Model
![[The Xception Architecture.png]]

All Convolution and SeparableConvolution Layers are followed by batch normalisation. All SeparabeConvolution layers use a depth multiplier of 1(no depth expansion).
There are residual connections also known as shortcut/skip connections, that were originally proposed in ResNet for all the flows. Residual connections are important for helping with convergence, both in terms of speed and final classification performance. 

![[Pasted image 20230812021005.png]]
As shown in the paper, Xception with residual connections, the validation accuracy against gradient descent steps is much higher.







### Proposed Method 2
It is a user defined convolutional neural network architecture using the Keras Framework. 
1) Input Layer: Receives images 28x28 pixels with 3 color channels RGB.
2) Convolutional Layers: 
	- the first layer applies 32 filters of size 3x3 using ReLU activation for non-linearity. Padding is same, meaning the output_size = input_size. The "he_normal" kernel initialiser is used for weight initialisation. 
	- Next is the max-pooling layer. It reduces the dimensions while retaining the relevant features.
	- Batch normalisation normalises outputs of the previous layer.
	Two more pairs of similar convolutional-pooling-batch-normalisation layers follow. But the filter counts are increasing ie 64, 128, 256 for extracting more complex features. 
3) Flatten Layer: Output of the final convolutional layer flattened to 1D vector to be fully connected layers.
4) Fully Connected Layers:
	- Drouput layer with a droupout rate of 0.2 to prevent overfitting.
	- A dense layer with 256 units and ReLU activation followed by batch normalisation.
	The same pattern is repeated. The next two layers are with 128 and 64 units, each followed by a batch normalisation.
	The last dense layer has 32 units, a ReLU activation and L1L2 regularisation followed by batch normalisation .
5) Output Layer: The final dense layer has 7 units using softmax to produce probability scores for each class. 
![[Pasted image 20230813023618.png]]
### Proposed Method 3