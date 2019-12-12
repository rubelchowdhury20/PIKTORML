<h1 align="center">CNN Part 2</h1>
<br>
<h3>Convolution Operation</h3>

<p align='center'><img src="https://i.imgur.com/cq71kyV.gif?noredirect"/></p>
<br>
<p align='center'><img src="https://mlnotebook.github.io/img/CNN/convSobel.gif"/></p>

<p align='center'><img src="https://i.imgur.com/kWkya58.png"/></p>

<h4>parameter sharing</h4>
In convolution one filter is being used by the entire image.Thus only (3x3) parameters are being shared. Thus it decreases the parameter numbers.

Everytime we do convolution operation we reduce input image size. We keep doing it so that we reach at a resolution of 1x1. To go from 400x400 image to 1x1 we need to use around 200 layers of convolution. Gpu can't handle that many layers. So we do some kind of operation called max pooling which will reduce input size drastically keeping the **loudest** features. Let's see what is maxpooling 

<h4>Maxpooling</h4>

Its function is to progressively reduce the spatial size of the representation to reduce the amount of parameters and computation in the network. Pooling layer operates on each feature map independently.
The most common approach used in pooling is max pooling.

Convolution has learnable parameters but max pooling doesn't have. It's extremely fast. If there is a feature map of size 6x6 after max pooling it becomes 3x3. Essentially we are passing only 25% features. This is more like filtering out the relevant features(9/36 * 100 ~ 25% ). Max pooling has to be used very carefully . After we have done couple of convolution and extracted relevant features we use maxpooling to reduce the size of the image. At a receptive field of say 11x11 we can see that network is able to pick up edges and gradient. So we add maxpooling after that. This will be more clear when we go through the receptive field concept.

<p align='center'><img src="https://developers.google.com/machine-learning/practica/image-classification/images/maxpool_animation.gif"/></p>
<br>
<p align='center'><img src="https://mlblr.com/images/maxpool.gif"/></p>
<br>
<p align='center'><img src ="https://media.springernature.com/original/springer-static/image/art%3A10.1007%2Fs13244-018-0639-9/MediaObjects/13244_2018_639_Fig6_HTML.png"/></p>


<h4>Padding</h4>

1. If you have noticed when we do convolution some pixels are covered more num of times than the pixels around the edges. 
2. And also when we do conv we keep decreasing the input image. But sometimes we need to keep the size of feature map same as input. Basically we don't want to shrink the input. So conv on a 6x6 input by 3x3 filter should give me back 6x6 feature map, instead of a 4x4 reduced feature map 

In these kind of scenarios we used a concept of padding where we pad the input image with some values(say zeros or just repeat the pixels, there are different techniques).

<p style="color:blue; font-size:150%;">If the input size is (nxn)
<br>
The conv filter size is (fxf)
<br>
Padding p and Stride is s 
<br>
The output size is calculated as
</p>

<p style="color:blue; font-size:200%;">[(n + 2p - f +1 )/s] * [(n + 2p - f +1 )/s]</p>  

<p style="color:red">(the [ ] represents floor funciton , which rounds the values to nearest integers) 
</p>


<p align='center'><img src="https://miro.medium.com/max/2126/1*W2D564Gkad9lj3_6t9I2PA@2x.gif"/></p>

<p align='center'><img src="https://s3-ap-south-1.amazonaws.com/av-blog-media/wp-content/uploads/2017/06/28094927/padding.gif"/></p>

<p align='center'><img src="https://i.stack.imgur.com/YyCu2.gif"/></p>

In keras the when we do convolution we mention the word valid(p = 0) or same (p=1)



<h4>Strides</h4>
Stride is the number of pixels shifts over the input matrix. When the stride is 1 then we move the filters to 1 pixel at a time. When the stride is 2 then we move the filters to 2 pixels at a time and so on.

Stride helps in reducing feature map faster.(some times it is used instead of maxpooling)



<p align='center'><img src="https://upload.wikimedia.org/wikipedia/commons/0/04/Convolution_arithmetic_-_Padding_strides.gif"/></p>

[Convolution animations](https://github.com/vdumoulin/conv_arithmetic)

<br>

<h4>why 3x3 not 5x5 or 7x7</h4>

1. Parameters are more so we need more computationally expensive hardware

2. Since Nvidia has started using 3x3 accelerator in their chip it has become a industry practice

3. Bigger kernels are slower may give better accuracy while testing. But it all comes down the problem of acc vs time trade off. You don't want to do some cancer test fast, but it should be accurate. But self driving car has to have fast output

<p align='center'><img src="https://i.imgur.com/pxWkqtC.png"/></p>


[Deciding optimal kernel size for CNN](https://towardsdatascience.com/deciding-optimal-filter-size-for-cnns-d6f7b56f9363)

<h4> Receptive Field of CNN </h4>

The receptive field in a convolutional neural network refers to the part of the image that is visible to one filter at a time. 

Here after applying 3x3 filter the output becomes 3x3 from 5x5. Each pixel of the first layer can see(have information) 3 pixel of the input. Similarly the next layer can see(have information) 3 pixel of its previous input(feature map).This is called local receptive filed. It is 3 here

But we can say the each pixel of the 2nd layer has seen the entire 5x5 indirectly. So it's global receptive field is 5

with every 3x3 filter conv receptive field is increased by 2 and after maxpooling it is doubled(roughly)



<p align='center'><img src="https://i.imgur.com/cq71kyV.gif"/></p>

<h4>Convolution in a RGB image</h4>

If you have a rgb image ,say 400x400x3. We use a filter of size 3x3x3 and we get a output of 398x398 
Here the filter has 3 channels.This is required say you want to detect only red edge or only blue edge etc. It doesn't make sense to use the same kernel channel for all 3 input image channels.So we use multiple channels for the filter

Now say we want to detect one red edge , one blue edge , one slant edge, one black edge(4types) etc . Now we have to use 4(4types)x (3x3x3)

so finally if we do convlution on a 400x400x3 image and we want extract 100 types of image we will 100s of (3x3x3) filters(kernels). that is 3x3x3x100 . output will be 398x398x100

<p align='center'><img src="https://predictiveprogrammer.com/wp-content/uploads/2018/06/convolve.gif"/></p>

<p align='center'><img src="https://dhruvkaran.com/conv-84deaf2954585b37a73fbcf84bc3cf6e.gif
"/></p>
<h4>Why do we add layers<h4> 

We add layers in a DNN for multiple reasons:

   we have an objective (say detecting an object), and we can do that easily if we could detect the parts of the objects. Parts of the objects can be built from some patterns, and these patterns in-turn can be made from textures. To make any kind of texture, we would need edges and gradients. We add layers to procedurally do exactly this. We expect that our first layers would be able to extract simples features like edges and gradients. Next layers would then build slightly complex features like textures, and the patterns. Then later layers could build parts of objects, which can then be combined into objects. This can be seen in the image above.
2. we progressively add layers, the receptive field of the network slowly increases. If we are using 3x3 filters, then each pixel in the second layers has only "seen" (receptive field) 3x3 pixels. Before the network can take any decision, the whole image needs to be processed. We add layers to achieve this. Also, consider the fact that required or important edges and gradients can be made or seen within 11x11 pixels in an image of 400x400. But say, we were looking at a face, the parts of the face would take much more area (or the number of pixels). 

<p align='center'><img src="https://i.imgur.com/cq71kyV.gif"/></p>

Here we see our first layer as a 5x5 image. We are convolving this 5x5 image with a filter of size 3x3, and hence the resulting output resolution will be a channel with 3x3 pixels/values. When we convolve on this 3x3 channel with a kernel of size 3x3, we will get only 1 output. We have added 2 layers here. 

 

To get the final output of 1 or 1x1, we could have used a 5x5 kernel directly. This means that using a 3x3 kernel twice is equivalent to using a 5x5 kernel. This also means that two layers of 3x3 have a resulting receptive field of 5x5. 

 

As we have discussed in the class, we want the final global receptive field (at the final prediction layer or output layer) to be equal to the size of the image. This is important as the network needs to "see" the whole image before it can predict exactly what the image is all about. 

 

This would mean that we need to add as many layers are required to reach the final receptive field equal to the size of the object. Since we have decided to consider the size of the object to be equal to the size of the image (for first few sessions), our final receptive field is going to be the size of the image. (We know this is not true, images can have objects of any size, but we need to consider this restriction to build our concepts. Later we would work on what needs to be done to remove this restriction). 


<p align='center'> <img src="https://cdn-images-1.medium.com/max/1600/1*Zx-ZMLKab7VOCQTxdZ1OAw.gif"/></p>

Whenever our kernel is stopping on a 3x3 area, we are looking at 9 multiplications and the sum of the resulting 9 multiplications being passed on to the output (green) channel as shown in the image above. 

The values in the output channel can be considered as the "confidence" of finding a particular feature. Higher the value, higher the confidence, and lower (or more negative) the value, "higher" the confidence of the non-existence of the feature.


<h4>Why maxpooling is added after some convolution operations</h4>


Let's look at what 3x3 kernels are trying to extract:

<p align='center'> <img src="https://i.stack.imgur.com/V0iCy.jpg"/></p>

We really cannot find any pattern here. 3x3 is a very small area to actually gather any Perceivable information (for human eyes), especially when we are referring to an image of size 400x400. 

How about 5x5?
<p align='center'> <img src="https://i.stack.imgur.com/i89Cq.jpg"/></p>
 
Even at 5x5 (for large image sizes) we can't make our a lot of stuff. In fact, at 7x7 we might also fail (look below):

<p align='center'> <img src="https://cdn-images-1.medium.com/max/1600/1*Rrplue_mc9imvH19Q58BGA.png"/></p>


11x11
It is only at the receptive field of around 11x11 when we'd be able to make out thinks. Look what textures are extracting at 11x11. 

Let's look at what 3x3 kernels are trying to extract:

<p align='center'> <img src="https://qph.fs.quoracdn.net/main-qimg-4bfdf63a4c5b24590f0deec9673eaee5.webp"/></p>

That's why we have some restrictions for where to add maxpooling. Generally we add maxpooling after receptive field is around 11x11(for an 400x400 image considering the size of the image is equal to size if the object present)

[kernal visualization](https://distill.pub/2017/feature-visualization/)

<h4>1x1 convolution<h4>
<h4>non linearity<h4>
<h4>Summary of constructing a cnn</h4>