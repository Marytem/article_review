# article_review

__Paper info__
* **Title**: ICface: Interpretable and Controllable Face Reenactment Using GANs
* **Authors**: Soumya Tripathy, Juho Kannala and Esa Rahtu
* **[Link](https://arxiv.org/pdf/1904.01909.pdf)**
* **Year**: 2019

### Task formulation & methods

__Idea__ - face animator to controll facial expression and pose. Face control is done using Actual Units for expression and angles for pose. AUs and angles form together a feature tensor. An animator is implemented as a 2-stage NN, learned in self-supervised manner using a large video collection.

__Method/pipeline description__

* Main task - take image as a source and produce a face image depicting the source identity with the desired features (further driving features, or driving image).
* Traditional approach - fit detailed 3d face model on source img, and create animation of the model. Problem - requires too much effort.
* Recently -  animation is directly formulated as an end-to-end learning problem, where the necessary model is obtained implicitly using a large data collection. Problem - lacks interpretability and does not allow selective editing.
* So authors proposed a GAN based system that is able to reenact realistic emotions and head poses for a wide range of source and driving identites. Allows selective editing and extensive control.


### __Architecture__

<img src="/assets/architecture.png">

The architecture of our model consists of four different subnetworks: __image encoder, face neutraliser,  face generator__, and __discriminator__.

* __Image encoder  I<sub>E</sub>__ 

 A network that maps maps the input face image into an equal size feature tensor. The network has a hourglass architecture consisting of convolutions and deconvolutions with normalization and activation layers.
 * __Neutralizer G<sub>N</sub>__ 
 
 The neutralizer is a generator network that transforms the feature representation into representation with a neutral pose and facial expression. The architecture of the GN network consists of strided convolution, residual blocks and deconvolution layers. Inspired by CycleGAN arcitecture. 
* __Generator G<sub>A</sub>__ 

 The generator network transforms the feature representation of the neutral face into the final reenacted output image. The output image is expected to be same as source identity with driving features applied. The architecture of the GA network is similar to that of GN .
 
* __Discriminator D__

The discriminator network performs three tasks simultaneously:   
   * evaluates the realism of the neutral and reenacted images through C1
   * predicts the facial attributes through C2
   * classifies the identity of the generated face through FC layer with softmax
   
The blocks C1 and C2 consist of convolution block with sigmoid activation. The overall architecture consists of strided convolution and activation layers. The same discriminator with identical weights is used for GN and GA.
 
 
### __Training__

<img src="/assets/dataset.png" width="350" align="right"/>

* __dataset__ - [VoxCeleb](http://www.robots.ox.ac.uk/~vgg/data/voxceleb/), publically available.  -->
* __process__: take one frame of the same video as source image, next as driving. Extract features from driving, and feed them to the network as driving features FA<sub>D</sub> 
* __losses__ - a weighted combination of the following losses: __Facial attribute reconstruction loss__, __Identity classification loss__, __Reconstruction loss__.
 
### Results 
 The results and comparison are better seen from images in the paper, as face reenacment is a very visual field. Better see paper ilustrations.
