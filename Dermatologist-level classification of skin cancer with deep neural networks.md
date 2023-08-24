Andre Esteva and Colleageues

- used [[Deep Convolutional Neural Networks(Theory)]]
- single CNN that was trained end to end using only pixels and disease labels as inputs.
- CNN using dataset of 129450 clinical images consisting of 2032 different diseases.
- outperformed/ performed at par with 21 board certified dermatologists on biopsy proven clinical images with two critical binary classification use cases.
- Statistics of importance  - 
	- 5.4 million new cases of skin cancer in US every-year
	- 1/5 Americans diagnosed with cutaneous malignancy in their lifetime
	- Although melanomas(the worst kind) account for less than 5% of all types of skin cancer in the US, they account for 10,000 deaths in the US alone.
	- Early Detection is key as 5-year survival rate drops from 99% when detected in early stages to 14% in last stage.


### The need for this?
- Previous work lacked generalisation capability of medical practioners as there was lack of diversity in the dataset.
- They utilised on dermascopic images and histological images, which are highly standardized and quite often difficult to acquire by the common man.
- They focused on mobile phone images that are more variable as zoom, angle, lighting.
- These variable factors made classification more challenging.
- They also required extensive pre-processing, lesion segmentation and extraction of domain-specific visual features before classification.
- used a small dataset

### How was it overcome?
- Data driven approach taken
- 1.41 mil. pre training and training images make classification robust. 
- Thus, not affected by photographic variability.
- Single network for both photographic and dermoscopic images.



#### Trained using transfer learning
- GoogleNet Inception v3 CNN architecture was pretrained on 1.28 million images
- Train it on the data set using transfer learning


## Method
### Taxonomy
- 2032 Individual diseases arranged in a tree structure with three general disease classes![[Pasted image 20230624230358.png]]
