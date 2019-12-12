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

<p align='center'><img src="https://i.imgur.com/cRhhjRi.mp4"/></p>

[RGB convolution explained by Andrew NG](https://www.youtube.com/watch?v=KTB_OFoAQcc&list=PLkDaE6sCZn6Gl29AoE31iwdVwSG-KnDzF&index=6)

<p>

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

[filter visualization](https://distill.pub/2017/feature-visualization/)

We stopped here:

400x400x3     | (3x3x3)x32        | 398x398x32     RF of 3x3<br>
398x398x32   | (3x3x32)x64      | 396x396x64    RF of 5X5<br>
396x396x64   | (3x3x64)x128    | 394x394x128  RF of 7X7<br>
394x394x128 | (3x3x128)x256 | 392x392x256  RF of 9X9<br>
392x392x256 | (3x3x256)x512 | 390x390x512  RF of 11X11<br>
MaxPooling<br>
195x195x512 | (?x?x512)x32    | ?x?x32 RF of 22x22<br>
<br>

.. 3x3x32x64                    RF of 24x24<br>
.. 3x3x64x128                  RF of 26x26<br>
.. 3x3x128x256               RF of 38x28<br>
.. 3x3x256x512                RF of 30x30<br>


Some points to consider before we proceed:
In the network above, the most important numbers for us are:

1. 400x400, as that defines where our edges and gradients would form
2. 11x11, as that's the receptive field which we are trying to achieve before we add transformations (like channel size reduction using MaxPooling)
3. 512 kernels, as that is what we would need at a minimum to describe all the edges and gradients for the kind of images we are working with (ImageNet)
4. We have added 5 layers of conv, but that is inconsequential as our aim was to reach 11x11 receptive field. For some other dataset we might have reach required RF for edges&gradients, say after 4 or 3 layers
5. We are using 3x3 because of the benefits it provides, our ultimate aim is to reach the receptive field of 11x11
6 . We are following 32, 64, 128, 256, 512 kernels, but there are other possible patterns. We are choosing this specific one as this is expressive enough to build 512 final kernels we need, and since this is an experiment we could, later on, reduce the kernels depending on what hardware we pick for deployment. 
7. The receptive field of 30x30 is again important for us because that is where we are "hoping" form textures. 
8. The 5 Convolution Layers we see above form "Convolution Block".
9. We are again following the same pattern of the increasing number of kernels from 32 to 512 in the second convolution block for the same reason we picked this pattern in the first block. 
10. Again 512 kernels in the second convolution block are important for us as we need a large number of textures to be able to define all out images. 

<h4>How do reduce number of filters</h4>

We cannot just add 32, 3x3 kernels as that would re-analyze all the 512 channels and give us 32 kernels. This is something we used to do before 2014, and it works, but intuitively we need something better. We have 512 features now, instead of evaluating these 512 kernels and coming out with 32 new ones, it makes sense to combine them to form 32 mixtures. That is where 1x1 convolution helps us. 

Think about these few points:

1. Wouldn't it be better to merge our 512 kernels into 32 richer kernels which could extract multiple features which come together?
2. 3x3 is an expensive kernel, and we should be able to figure out something lighter, less computationally expensive method. 
3. Since we are merging 512 kernels into 32 complex one, it would be great if we do not pick those features which are not required by the network to predict our images (like backgrounds). 
   

<h4>1x1 convolution<h4>
1x1 provides all these features. 

1. 1x1 is computation less expensive. 
2. 1x1 is not even a proper convolution, as we can, instead of convolving each pixel separately, multiply the whole channel with just 1 number
4. 1x1 is merging the pre-existing feature extractors, creating new ones, keeping in mind that those features are found together (like edges/gradients which make up an eye)(back propagation will make sure to merge relevant features)
4. 1x1 is performing a weighted sum of the channels, so it can so happen that it decides not to pick a particular feature which defines the background and not a part of the object. This is helpful as this acts like filtering. Imaging the last few layers seeing only the dog, instead of the dog sitting on the sofa, the background walls, painting on the wall, shoes on the floor and so on. If the network can filter out unnecessary pixels, later layers can focus on describing our classes more, instead of defining the whole image. 
This is how 1x1 convolution looks like:

<p align = 'center'><img src = "https://cdn-images-1.medium.com/max/1600/1*deVKbCzJs_7eL6p2ltkY0g.png"/></p>

<p align = 'center'> <img src="https://miro.medium.com/max/600/1*AjaTIcaz2oHFuBwTiGfL3w.gif"/></p>

in the above gif 

What you see above is an input of size 32x32x10. We are using 4 1x1 kernels here. Since we have 10 channels in input, our 1x1 kernel also has 10 channels. 

32x32x10 | 1x1x10x4 | 32x32x4

We have reduced the number of channels from 10 to 4. Similarly, we will use 1x1 in our network to reduce the number of channels from 512 to 32. Let's look at the new network:



<h4>Activation Function</h4>


Their main purpose is to convert an input signal of a node in an ANN to an output signal.

Since ages, this activation function has kept AIML community occupied in wrong directions. 

After the convolution is done, we need to take a call with what to do with the values our kernel is providing us. Should we let all pass, or should we change them? This question of choice (of what to do with output) has kept us guessing. And as humans always feel, deciding what to pick and what to remove must have a complicated solution. 
 

Why do we need an activation function?
 

If we do not apply an Activation function then the output signal would simply be a simple linear function. A linear function is just a polynomial of one degree. Now, a linear equation is easy to solve but they are limited in their complexity and have less power to learn complex functional mappings from data. A Neural Network without Activation function would simply be a Linear regression Model, which has limited power and does not perform well most of the times. We want our Neural Network to not just learn and compute a linear function but something more complicated than that.

 

Why do we need non-linearities?

We need a Neural Network Model to learn and represent almost anything and any arbitrary complex function which maps inputs to outputs. Neural-Networks are considered Universal Function Approximators. It means that they can compute and learn any function at all. Almost any process we can think of can be represented as a functional computation in Neural Networks.

 

Hence it all comes down to this, we need to apply an Activation function f(x) so as to make the network more powerful and add the ability to it to learn something complex and complicated form data and represent non-linear complex arbitrary functional mappings between inputs and outputs. Hence using a non-linear Activation we are able to generate non-linear mappings from inputs to outputs.

<h4>Relu</h4>
<br>
<p align = 'center'><img src = "https://miro.medium.com/max/2052/1*DfMRHwxY1gyyDmrIAd-gjQ.png"/></p>

<br>

<p align = 'center'><img src = "https://i.imgur.com/EolgnXi.jpgg"/></p>



This is a very simple function. It allows all the positive numbers to pass on, as it is, and converts all the negatives to zero. It's message to backpropagation or kernels is simple. If you want some data to be passed on to the next layers, please make sure the values are positive. Negative values would be filtered out. This also means that if some value should not be passed on to the next layers, just convert them to negatives. 

ReLU since has worked wonders for us. It is fast, simple and efficient. 

ReLu- Rectified Linear units : It has become very popular in the past couple of years. It was recently proved that it had 6 times improvement in convergencefrom Tanh function. It’s just R(x) = max(0,x) i.e if x < 0 , R(x) = 0 and if x >= 0 , R(x) = x.

 

ReLU is linear (identity) for all positive values, and zero for all negative values. This means that:

1. It’s cheap to compute as there is no complicated math. The model can therefore take less time to train or run.

2. It converges faster. Linearity means that the slope doesn’t plateau, or “saturate,” when x gets large. It doesn’t have the vanishing gradient problem suffered by other activation functions like sigmoid or tanh.

3. It’s sparsely activated. Since ReLU is zero for all negative inputs, it’s likely for any given unit to not activate at all. 




ReLU is simple, efficient and fast, and even if any one of the above is better, we are talking about a marginal benefit, with an increase in computation. We'll stick to ReLU in our course. Also NVIDIA has acceleration for ReLU activation, so that helps too. 


<h4>Summary of constructing a cnn</h4>

This is how our network looks like 

<p>CONVOLUTION BLOCK 1 BEGINS<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;398x398x32&nbsp; &nbsp;| (3x3x32)x64&nbsp; &nbsp; &nbsp; | 396x396x64&nbsp; &nbsp; RF of 5X5<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;396x396x64&nbsp; &nbsp;| (3x3x64)x128&nbsp; &nbsp; | 394x394x128&nbsp; RF of 7X7<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;394x394x128 | (3x3x128)x256 | 392x392x256&nbsp; RF of 9X9<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;392x392x256 | (3x3x256)x<strong>512</strong> | 390x390x512&nbsp; RF<strong>&nbsp;of 11X11</strong></p>
<p>CONVOLUTION BLOCK 1 ENDS</p>
<p>&nbsp;</p>
<p>TRANSITION BLOCK 1 BEGINS<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;MAXPOOLING(2x2)<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;195x195x512 | <strong>(1x1x512)x32</strong>&nbsp; &nbsp; | 195x195x32 RF of 22x22<br>TRANSITION BLOCK 1 ENDS</p>
<p>&nbsp;</p>
<p>CONVOLUTION BLOCK 2 BEGINS<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;195x195x32&nbsp; &nbsp; &nbsp;|(3x3x32)x64&nbsp; &nbsp; &nbsp; &nbsp; | 193x193x64&nbsp; &nbsp; &nbsp; RF of 24x24<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;193x193x64&nbsp; &nbsp; &nbsp;|(3x3x64)x128&nbsp; &nbsp; &nbsp; | 191x191x128&nbsp; &nbsp; RF of 26x26<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;191x191x128&nbsp; &nbsp;|(3x3x128)x256&nbsp; &nbsp;| 189x189x256&nbsp; &nbsp; RF of 28x28<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;189x189x256&nbsp; &nbsp;|(3x3x256)x512&nbsp; &nbsp;| 187x187x512&nbsp; &nbsp; RF of 30x30<br>CONVOLUTION BLOCK 2 ENDS</p>
<p>&nbsp;</p>
<p>TRANSITION BLOCK 2 BEGINS<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;MAXPOOLING(2x2)<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;93x93x512 | <strong>(1x1x512)x32</strong> &nbsp; | 93x93x32 RF of 60x60<br>TRANSITION BLOCK 2 ENDS</p>
<p>&nbsp;</p>
<p>CONVOLUTION BLOCK 3 BEGINS<br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp;93x93x32 | (3x3x32)x64 | 91x91x64&nbsp; &nbsp; &nbsp; &nbsp;RF of 62x62<br>...</p>

<br>
<p align = "center"><img src = "https://miro.medium.com/max/1200/1*5A4b1qOZIr4Q6SKceqGn7w.jpeg"/></p>

[mnist data filter visualization](https://scs.ryerson.ca/~aharley/vis/conv/)