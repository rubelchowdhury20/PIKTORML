
<h1>Session 1</h1>
<h2>Supervised Learning</h2>
<p>

In supervised machine learning we train the machine learning model with previously  __labelled__ data. Model learns from the previously labeled data and predicts on similar kind of new data(which is not labelled).

The term __supervised__ itself says that model is build up with a supervision before it starts predicting on unforeseen data.
</p>

<h2>Examples of Supervised Learning:</h2>
<ul>
    <li>Regression:
    The goal of regression is to find surfaces in that space that best 'conform' to the overall distribution of the data.
    Example : Predicting house prices
    </li>
    <li>Classification :
     The goal of classification is to find surfaces that best separate different clusters of data. 
     Example : Gender Classification
    </li>
</ul>
<p align='center'><img src="https://www.researchgate.net/profile/Yves_Matanga2/publication/326175998/figure/fig9/AS:644582983352328@1530691967314/Classification-vs-Regression.png" width = "400"/></p>
<br>

<h2>Unsupervised Learning</h2>
<p>
In unsupervised machine learning we give model unlabelled data and let it figure out on its own to discover some info about the data
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
Cost function is used to guide the model to fit the data better.
<p align='center'><img src="https://billyinn.files.wordpress.com/2014/07/e5b18fe5b995e5bfabe785a7-2014-07-12-e4b88be58d8812-53-04.png" width = "600"/></p>
<br>
</p>
<h3>Linear regression with one variable :</h3>
Let's say theta0 is 0, we have only one variable. Let's try to plot a graph of hypothesis vs theta0 and Cost function vs theta0.
<p align='center'><img src="
https://raw.githubusercontent.com/astikanand/techblogs/master/5_machine_learning/assets/cost_function_intuition_1.png" width = "600"/></p>

We have a plot of cost function vs theta0 and we can find the value of theta for which cost function is minimum

if we consider both theta0 and theta1, we get a __bow__ shaped cost funciton graph and we try to find values of theta0 and theta1 for which cost function is minimum
<p align='center'><img src="https://i.ytimg.com/vi/riplXsNf_zs/maxresdefault.jpg" width = "600"/></p>

Let's talk about gradient descent:
let's say we have cost function graph like below. In this case how do we reach to minimum point.
<p align='center'><img src="https://thumbs.gfycat.com/AngryInconsequentialDiplodocus-size_restricted.gif" width = "600"/></p>

This is how they say the math looks like :

<p align='center'><img src="https://media.geeksforgeeks.org/wp-content/uploads/Cost-Function.jpg" width = "600"/></p>

This is what happens Actually:

<p align='center'><img src="https://media.giphy.com/media/O9rcZVmRcEGqI/giphy.gif" width = "600"/></p>

[Good read](https://machinelearningmastery.com/linear-regression-tutorial-using-gradient-descent-for-machine-learning/)

<ul>Assignment:</ul>
    <li>
     1. Write an md file to describe at least 2 real life examples of supervised/ unsupervised learning, clustering , classification problems
    </li>
    <li>
    2. coding assignment:
    </li>
</ul>