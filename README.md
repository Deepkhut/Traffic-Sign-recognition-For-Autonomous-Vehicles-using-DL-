
# Traffic-Sign-recognition-For-Autonomous-Vehicles-using-DL-






Introduction

traffic signs are an integral part of our road infrastructure. they provide critical information, sometimes compelling recommendations, for road users, which in turn requires them to adjust their driving behavior to make sure they adhere with whatever road regulation currently enforced. without such useful signs, we would most likely be faced with more accidents, as drivers would not be given critical feedback on how fast they could safely go, or informed about road works, sharp turn, or school crossings ahead. in our modern age, around 1.3m people die on roads each year. this number would be much higher without our road signs. naturally, autonomous vehicles must also abide by road legislation and therefore recognize and understand traffic signs.

Traditionally, standard computer vision methods were employed to detect and classify traffic signs, but these required considerable and time-consuming manual work to handcraft important features in images. Instead, by applying deep learning to this problem, we create a model that reliably classifies traffic signs, learning to identify the most appropriate features for this problem by itself.
Dataset Description
The image dataset is consists of more than 50,000 pictures of various traffic signs(speed limit, crossing, traffic signals, etc.) Around 43 different classes are present in the dataset for image classification. The dataset classes vary in size like some class has very few images while others have a vast number of images. The dataset doesn’t take much time and space to download as the file size is around 314.36 MB. It contains two separate folders, train and test, where the train folder is consists of classes, and every category contains various images.

The dataset is Split into training, test and validation sets, with the following characteristics:

	Images are 32 (width) x 32 (height) x 3 (RGB color channels)
	Training set is composed of 34799 images
	Validation set is composed of 4410 images
	Test set is composed of 12630 images
	There are 43 classes (e.g. Speed Limit 20km/h, No entry, Bumpy road, etc.)







Proposed Methods
	AlexNet
The original AlexNet architecture was proposed for the ImageNet data which is much larger then the images we have in the GTSRB data set. I therefore build a much smaller CNN then the original architecture proposed in the AlexNet paper, but build it according to the same design principles. The only difference being the local response normalization layers used in the originally proposed AlexNet model are not included as these have fell out of favor in recent times. I instead include batch normalization layers, this essentially incorporates normalization within each layer of the network and allows the network to reduce the internal co-variate shift via learnt parameters. The result of this is an increase in training speed and an increased robustness to choices in weight initialization.

	DenseNet-121
In DenseNet each layer is connected to every other layer in the network in a feed forward fashion. For each layer, the feature-maps of all preceding layers are used as input, and its own feature-maps are concatenated with its input into a single tensor and the used as inputs into its subsequent layer. A standard feed forward CNN with L layers will have L connections (one between each layer), DenseNet with its densely connected scheme must have (L+1)/ 2 direct connections.

Layers	output size	Densenet-121
Convolution	112x112	7 x 7 conv, stride2
pooling	56x56	3 x 3 max pooling, stride2

Dense Block (1)	56 x 56	[■(1&X&1 conv@3&X&3 conv)]          
Transition Layer (1)	56 x 56	1 x 1 conv
	28 x 28	2 x 2 average pool, stride 2

Dense Block (2)	28 x 28	[■(1&X&1 conv@3&X&3 conv)]    
Transition Layer (2)	28 x 28	1 x 1 conv
	14 x 14	2 x 2 average pool, stride 2

Dense Block (3)	14 x 14	[■(1&X&1 conv@3&X&3 conv)]    
Transition Layer (2)	14 x 14	1 x 1 conv
	7 x 7	2 x 2 average pool, stride 2

Dense Block (4)	7 x 7	[■(1&X&1 conv@3&X&3 conv)]    
classification layer	1 x 1	7 x 7 Global Average 
		1000D fully connected, softmax

	EdLenet 

The network is composed of 3 convolutional layers — kernel size is 3x3, with depth doubling at next layer — using ReLU as the activation function, each followed by a 2x2 max pooling operation. The last 3 layers are fully connected, with the final layer producing 43 results (the total number of possible labels) computed using the SoftMax activation function. The network is trained using mini-batch stochastic gradient descent with the Adam optimizer.


	Customized version

Results
	AlexNet


  




     Fig1. Accuracy and Loss for AlexNet
	DenseNet
				Fig2. Accuracy and Loss for DenseNet
	EdLenet
				Fig3. Accuracy and Loss for EdLeNet
	Customized Version
				Fig4. Accuracy and Loss 
Transfer Learning Model	Validation Accuracy 
AlexNet	Training accuracy: 100 %
Validation accuracy: 99.8%
Test accuracy: 98.32 %
 DenseNet	Training accuracy: 100%
Validation accuracy: 99.7%
Test accuracy 99.02%
 EdLenet	Training accuracy: 99.8%
Validation accuracy: 99.02%
Test accuracy 97.86%
Customized 	Training accuracy: 99.6%
Validation accuracy: 98.4%
Test accuracy 97.32%
Conclusion & Future scope of work
Through this project, understood how deep learning can be used to classify traffic signs with high accuracy, employing a variety of pre-processing and regularization techniques, and trying different model architectures.
AlexNet and DenseNet has performed very good in this problem giving an accuracy of 98 and 99% respectively.  With the accuracy and real-time results, the proposed model can be implemented/used in autonomous as well as non-Autonomous vehicles where it can be used to alert the driver regarding the road side traffic signs that are coming up or passing by.
