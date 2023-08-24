### Terms:
1) Parameter - Variable that is automatically learned during the training process
2) Hyperparameter - Variable that needs to be set before the training process starts
3) Kernel - Set of learnable parameters applied in convolution operations
4) Weight - Generally used interchangeably with parameter. However, specifically, refers to those parameters outside convolution layers




### Building blocks of CNN:
#### Convolution Layer
- responsible for feature extraction
- kernel - small array of parameters applied across the input(array of numbers aka tensor)
	![[Pasted image 20230625161514.png]]
- Output tensor is called a **feature map**
- General convolution doesn't allow centre of each kernel to overlap with the outermost element
- That's why, we use zero padding. 
- Stride - distance between two successive kernel operations. More than one for downsampling.
- Pooling is also used for downsampling
- Kernels are learnt automatically during the training process in the convolution layer
- size of kernels, no. of kernels, padding, stride are hyperparameters.


#### Non Linear Convolution Function
- earlier, smooth sigmoid or tanh was used as it resembled neuron functions closely.
- however, Rectified Linear Unit -  ReLU is used now. 
- ReLU computes f(x)=max(0,x)


#### Pooling Layer
- Downsampling that reduces the in-plane dimensionality of the feature maps
- "This introduces translation invariance to small shifts and distortions" ie It would go over a bigger picture and ignore small artifacts
- No learnable parameter in  any pooling layer
- However, filter size, stride and padding are hyperparameters


#### Max Pooling
- Takes patches from the input tensor and outputs only the maximum value in each patch
	   ![[Pasted image 20230625212329.png]]
- Downsampled images are halved in dimension

#### Global Average Pooling 
- Extreme downsampling where a feature map is downsampled into a 1x1 array
- This is by taking the average of all the elements in a feature map
- Depth of feature maps are retained

#### Fully Connected Layer
- Output feature map of the final convolution layer is "flattened" - transformed into a 1D array of numbers
- One or more fully connected layers aka Dense Layers
- Every input in dense layer connected by learnable weight
- The output of convolution and pooling are mapped by a subset of fully connected layers to the final outputs of the network
- The fully  connected final layer typically has the same number of output nodes as the number of classes
- Each fully connected layer is followed by a non-linear function such as ReLU.
- Explanation  - By going through these fully connected layers with non-linear functions, the network can learn to map the extracted features to the final outputs, which are the probabilities for each class in classification tasks. In other words, the network learns to recognize important features and make predictions based on those features.

#### Last Layer Activation Function
- usually different from the others. 
- Appropriate activation function needs to be chosen according to each task
- Activation function for multiclass classification is a softmax function
- softmax normalises output and makes each value between 0 and 1.
- ![[Pasted image 20230625220526.png]]




