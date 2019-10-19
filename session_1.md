
<h1>Session 1</h1>


<h2>labeled vs unlabeled data</h2>
<h3>Unlabeled data</h3>
Typically, unlabeled data consists of samples of natural or human-created artifacts that you can obtain relatively easily from the world. Some examples of unlabeled data might include photos, audio recordings, videos, news articles, tweets, x-rays (if you were working on a medical application), etc. There is no "explanation" for each piece of unlabeled data -- it just contains the data, and nothing else.
<h3>Labeled data</h3>
Labeled data typically takes a set of unlabeled data and augments each piece of that unlabeled data with some sort of meaningful "tag," "label," or "class" that is somehow informative or desirable to know. For example, labels for the above types of unlabeled data might be whether this photo contains a horse or a cow, which words were uttered in this audio recording, what type of action is being performed in this video, what the topic of this news article is, what the overall sentiment of this tweet is, whether the dot in this x-ray is a tumor, etc.

[labeled vs unlabeled data](https://stackoverflow.com/questions/19170603/what-is-the-difference-between-labeled-and-unlabeled-data)<br>
[examples of labeled vs unlabeled data](https://stats.stackexchange.com/questions/60987/are-there-examples-of-labelled-and-unlabelled-data)
<h2>Supervised Learning</h2>
<p>
    
In general, supervised learning occurs when a system is given input and output variables with the intentions of learning how they are mapped together, or related. The goal is to produce an accurate enough mapping function that when new input is given, the algorithm can predict the output.

Training data for supervised learning includes a set of examples with paired input subjects and desired output (which is also referred to as the supervisory signal). For example, in an application of supervised learning for image processing, an AI system might be provided with labeled pictures of vehicles in categories such as cars or trucks. After a sufficient amount of observation, the system should be able to predict from unlabeled data.


In supervised machine learning we train the machine learning model with previously  __labelled__ data. Model learns from the previously labeled data and predicts on similar kind of new data(which is not labelled).

The term __supervised__ itself says that model is build up with a supervision before it starts predicting on unforeseen data.
</p>

<h2>Examples of Supervised Learning:</h2>
<ul>
    <li>Classification vs Regression:
    Regression and classification are both related to prediction, where regression predicts a value from a continuous set, whereas classification predicts the 'belonging' to the class.

For example, the price of a house depending on the 'size' (in some unit) and say 'location' of the house, can be some 'numerical value' (which can be continuous): this relates to regression.

Similarly, the prediction of price can be in words, viz., 'very costly', 'costly', 'affordable', 'cheap', and 'very cheap': this relates to classification.
    </li>
    
</ul>
<p align='center'><img src="https://www.researchgate.net/profile/Yves_Matanga2/publication/326175998/figure/fig9/AS:644582983352328@1530691967314/Classification-vs-Regression.png" width = "400"/></p>
<br>

<h2>Unsupervised Learning</h2>
<p>

**Please go through what is labelled and ublabelled data to understand unsupervised learning**

Unsupervised learning is the training of an artificial intelligence (AI) algorithm using information that is neither classified nor labeled and allowing the algorithm to act on that information without guidance.

In unsupervised learning, an AI system is presented with unlabeled, uncategorised data and the system’s algorithms act on the data without prior training. The output is dependent upon the coded algorithms. Subjecting a system to unsupervised learning is one way of testing AI.
</p>
<h2>Examples of unsupervised Learning:</h2>
<ul>
    <li>Clustering:
    This is used to seperate differnet types of data so that when given a new data the model should be able to tell which group of data it belongs to.
    </li>
</ul>
<p align='center'><img src="https://i.imgur.com/qtodMJB.png" width = "400"/></p>
<br>

[Supervised and Unsupervised Machine Learning Algorithms](https://machinelearningmastery.com/supervised-and-unsupervised-machine-learning-algorithms/)

<h2>Linear Regression</h2>
<p><h3>Problem statement:</h3>
Let's say we have some data of house size(in sqft) and their corresponding prices.Given We need to figure out how can i use this data to predict a new house price based on this data(the test data will have only size, we won't know the price of it)
<p align='center'><img src="https://wingshore.files.wordpress.com/2014/11/model.png" width = "600"/></p>
<br>
</p>
<p>So we have training data x and output y. We need to find a h(hypothesis) which will map x to y</p>

<h3>Cost function:</h3>
It is a function that measures the performance of a Machine Learning model for given data. Cost Function quantifies the error between predicted values and expected values and presents it in the form of a single real number. Depending on the problem Cost Function can be formed in many different ways. The purpose of Cost Function is to be either
<p align='center'><img src="https://billyinn.files.wordpress.com/2014/07/e5b18fe5b995e5bfabe785a7-2014-07-12-e4b88be58d8812-53-04.png" width = "600"/></p>
<br>
</p>
<h3>Linear regression with one variable :</h3>
Let's say theta0 is 0, we have only one variable. Let's try to plot a graph of hypothesis vs theta0 and Cost function vs theta0.
<p align='center'><img src="
https://raw.githubusercontent.com/astikanand/techblogs/master/5_machine_learning/assets/cost_function_intuition_1.png" width = "600"/></p>

[The above image explanation](https://www.youtube.com/watch?v=yR2ipCoFvNo&list=PLLssT5z_DsK-h9vYZkQkYNWcItqhlRJLN&index=6)

We have a plot of cost function vs theta0 and we can find the value of theta for which cost function is minimum

if we consider both theta0 and theta1, we get a __bow__ shaped cost funciton graph and we try to find values of theta0 and theta1 for which cost function is minimum
<p align='center'><img src="https://i.ytimg.com/vi/riplXsNf_zs/maxresdefault.jpg" width = "600"/></p>

Let's talk about gradient descent:
let's say we have cost function graph like below. In this case how do we reach to minimum point.
Gradient descent is an optimization algorithm used to minimize some function by iteratively moving in the direction of steepest descent as defined by the negative of the gradient. In machine learning, we use gradient descent to update the parameters of our model. Parameters refer to coefficients in Linear Regression and weights in neural networks.

<p align='center'><img src="https://thumbs.gfycat.com/AngryInconsequentialDiplodocus-size_restricted.gif" width = "600"/></p>

This is how they say the math looks like :

<p align='center'><img src="https://media.geeksforgeeks.org/wp-content/uploads/Cost-Function.jpg" width = "600"/></p>

This is what happens Actually:

<p align='center'><img src="https://media.giphy.com/media/O9rcZVmRcEGqI/giphy.gif" width = "600"/></p>

[Interested people can go through the andrew ng lecture of machine learning from 2.1 to 2.8](https://www.youtube.com/watch?v=kHwlB_j7Hkc&list=PLLssT5z_DsK-h9vYZkQkYNWcItqhlRJLN&index=4)

[linear regression explained](https://towardsdatascience.com/linear-regression-using-gradient-descent-97a6c8700931)<br>

[play with linear regression online](http://www.shodor.org/interactivate/activities/Regression/)

[Good read](https://machinelearningmastery.com/linear-regression-tutorial-using-gradient-descent-for-machine-learning/)

**Please look for medium articles for linear regression with gradient decent**
<br>
<ul>Assignment:</ul>
    <li>
     1. Write an md file to describe at least 2 real life examples of supervised/ unsupervised learning, clustering , classification problems
    </li>
    <li>
    1. coding assignment:
    </li>
</ul>