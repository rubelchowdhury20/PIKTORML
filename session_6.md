<h1 align="center"> Introduction to CNN</h1>
<br>
<h3>Let's Understand what is an Image:</h3>
Most of the colour images we see are RGB(3 channel images).RGB image is 8-bits(industry standard)

And Grayscale image has 1 channel with 8 bit(0-255)

Intensity values for binary image is defined by bits. It only have two colors Black and White. 


[rgb image histogram](https://www.google.com/search?biw=836&bih=936&tbm=isch&sxsrf=ACYBGNSjxSxAF3VOivizjmxxeViUHisuSw%3A1574917825451&sa=1&ei=wVbfXaeLG4Kv9QOEgKZ4&q=rgb+iamge+histagram&oq=rgb+iamge+histagram&gs_l=img.3...8017.13134..13303...2.0..0.115.1718.19j2......0....1..gws-wiz-img.......0i8i30j35i39j0i67j0.xGVB3H2ioIQ&ved=0ahUKEwjn76SMkozmAhWCV30KHQSACQ8Q4dUDCAc&uact=5)

[grayscale image histogram](https://www.google.com/search?biw=836&bih=936&tbm=isch&sxsrf=ACYBGNRSjbJenicR7yGYvolzGzKJHGDIcA%3A1574917839714&sa=1&ei=z1bfXZeQK9a6rQH9r4DIBw&q=grayscale+image+histogram&oq=grayscale+image+histogram&gs_l=img.3..35i39j0i24.108229.109748..110597...0.0..0.113.688.8j1......0....1..gws-wiz-img.......0i7i30j0i8i7i30.qxJ-tRNdvvg&ved=0ahUKEwjXs4uTkozmAhVWXSsKHf0XAHkQ4dUDCAc&uact=5#imgrc=XX2uP6TjYFs2-M:)

<h3 align = "left">Why RGB not something else(why not RYB)</h3>

<p align='center'><img src="https://i.imgur.com/4tFVqI8.png" width = "600"/></p>

A color is defined by one specific wave length or a mixture of these wave lengths. There is a spectrum of colors that only consist of a single wave length, like a specific kind of Red, Blue, Yellow, Green, etc. Mixing these wave lengths at a specific ratio we get colors like White, Brown, and Pink. This is the physical view on colors.
However, our eyes have receptors for 3 different colors/wave lengths. The combination of the neural signal strength on these three receptors are interpreted by our brain as a specific color. Simply speaking our cone cells can receive Blue, Green, and Red light. If you see something that is pure Yellow, the Red and Green cones are stimulated. If you now stimulate the cones with the right combination of a pure Red and pure Green wave length your brain will also perceive this as Yellow. Your eye cannot tell the difference.
Based on this assumption how the eye works the previous answers are correct. This is why we use RGB for additive colors and CMYK for subtractive colors. This is just the natural result of how we perceive physics (through our eyes). The alternative would be to describe each color (when we want to store it) as a combination of an infinite number of wave length. This is not feasible at all. Why use an infinite number of values when 3 numbers in RGB will do the trick for our eyes?

[additive vs subtractive colour](https://www.youtube.com/watch?v=Er7CM_RNFZ4)

<p align='center'><img src="https://i.imgur.com/Cq2v4O6.png"/></p>

<h3>whats' a channel</h3>

Images are usually represented as Height x Width x #Channels where #Channels is 3 for RGB images and 1 for grayscale images. Sometimes you see Width x Height x #Channels, but the third dimension is the “channels.”

Note: in deep learning libraries like caffe, the fundamental “activation” tensor is a N x C x H x W quantity. The rearrangement makes sense for deep learning, and in this case the second dimension is the channels.

Fom DNN perspective, channels are where similar features are gathered together

[Images and Channels](http://www.georeference.org/doc/images_and_channels.htm)

<h3>How does brain visualize</h3>

<p align='center'><img src="https://personal.utdallas.edu/~tres/integ/sen4/8_05.jpg"/></p>

<p align='center'><img src="https://i.imgur.com/OiWuTUi.png"/></p>

<h3>Convolution</h3>

<h4>why convolution</h4>
Facebook’s Yann LeCun helped establish how we use CNNs today—as multiple layers of neurons for processing more complex features at deeper layers of the network. Their properties differ from traditional feed-forward neural networks in some important ways that make them effective at image-based problems. For example, images are frequently best-represented in multiple dimensions: height, width, and depth, where depth corresponds to the number of channels used for each pixel. If an image is encoded with a depth of three, for example, those channels would likely correspond to the red, blue, and green channels. In some workflows, using a traditional fully-connected network could lead to a drastic increase in the number of model parameters—in a 670 x 1040 image, this would be over two million weights in the first layer of the network alone!  This would almost certainly lead to something we in the data sciences refer to as “over-fitting”—building a model that is really good at classifying the images that were used to estimate the weight parameters, such as puppies, but really bad at classifying images it hasn’t already been exposed to, such as a puppy wearing a hat. CNNs minimize the number of parameters by allowing different parts of the network to specialize in high-level features like a texture or a repeating pattern.

<!-- todo read the paper mentioned in the article to get an understanding of the intution of conv net -->
[CNN history](https://towardsdatascience.com/convolutional-neural-networks-the-biologically-inspired-model-f2d23a301f71)

<h4>Edge detection:</h4>
We can say that sudden changes of discontinuities in an image are called as edges. Significant transitions in an image are called as edges.

Types of edges
Generally edges are of three types:

Horizontal edges

Vertical Edges

Diagonal Edges

Why detect edges

Most of the shape information of an image is enclosed in edges. So first we detect these edges in an image and by using these filters and then by enhancing those areas of image which contains edges, sharpness of the image will increase and image will become clearer.

<p align='center'><img src="https://i.imgur.com/CoPvRh7.png"/></p>
<br>

<h3>How is convolution performed</h3>


<p align='center'><img src="https://i.imgur.com/cq71kyV.gif?noredirect"/></p>
<br>
<p align='center'><img src="https://mlnotebook.github.io/img/CNN/convSobel.gif"/></p>


[very good resource for convolution visualization](http://setosa.io/ev/image-kernels/)

[convolution explained](http://cs231n.github.io/convolutional-networks/)

<p align='center'><img src="https://i.imgur.com/pxWkqtC.png"/></p>
<h4>why 3x3 not 5x5 or 7x7</h4>

1. Parameters are more so we need more computationally expensive hardware

2. Since Nvidia has started using 3x3 accelerator in their chip it has become a industry practice

3. Bigger kernels are slower may give better accuracy while testing. But it all comes down the problem of acc vs time trade off. You don't want to do some cancer test fast, but it should be accurate. But self driving car has to have fast output

[Deciding optimal kernel size for CNN](https://towardsdatascience.com/deciding-optimal-filter-size-for-cnns-d6f7b56f9363)

<!-- <h4>Maxpooling</h4>

Its function is to progressively reduce the spatial size of the representation to reduce the amount of parameters and computation in the network. Pooling layer operates on each feature map independently.
The most common approach used in pooling is max pooling.

<p align='center'><img src="https://mlblr.com/images/maxpool.gif"/></p> -->


<h4>Convolution Operation in network</h5>

<p align='center'><img src="https://i.imgur.com/kWkya58.png"/></p>

[Session_6 introduction to CNN](https://www.youtube.com/watch?v=qZEpu5zBIyE)