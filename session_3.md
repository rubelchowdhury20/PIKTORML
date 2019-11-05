<h1 align='center'>Session 3</h1>
<h3 align='center'>Recap</h3>
#### The Linear Regression:

Linear regression is a kind of statistical analysis that attempts to show a relationship between two variables.

The core idea is to obtain a line that best fits the data. The best fit line is the one for which total prediction error (all data points) are as small as possible. Error is the distance between the point to the regression line.

##### Important Formulas:

###### Hypothesis:

$$
h_\theta(x) = \theta_0 + \theta_1x
$$

###### Parameters:

$$
\theta_0, \theta_1
$$

###### Cost Function:

$$
J(\theta_0, \theta_1) = \frac{1}{2m} \sum_{i=1}^m {(h_\theta(x^{(i)}) - y^{(i)})^2}
$$



###### Goal:

$$
\min_{\theta_0, \theta_1} {J(\theta_0, \theta_1)}
$$



##### Gradient Descent:

Gradient descent is a first-order iterative optimisation algorithm for finding the minimum of a function. To find a local minimum of a function using gradient descent, one takes steps proportional to the negative of the gradient (or approximate gradient) of the function at the current point.

$$
\theta_j := \theta_j - \alpha \frac{\partial}{\partial\theta_j} J(\theta_0, \theta_1)
\\
\alpha = learning \ rate
$$

###### Graphical Representation of Gradient Descent Algorithm
<img align='center' src="https://machinelearningmedium.com/assets/2017-08-15-gradient-descent/fig-2-gradient-descent-steps.gif?raw=true">

###### Graph of y = tan(x)
<img align='center' src="https://amsi.org.au/ESA_Senior_Years/imageSenior/2d_40.png">

Here we can see how the tan(x) value, that is nothing but our gradient which is varying based on the angle or theta value.

###### Simplification of Gradient Descent Formula:

$$
\begin{align}
\frac{\partial}{\partial \theta_j} {J_\theta} & = \frac{\partial}{\partial \theta_j} \frac{1}{2m}\sum_{i=1}^{m}(h_\theta(x_i) - y)^2 \\
 & = \frac{1}{m} \sum_{i=1}^{m}(h_\theta(x_i) - y)\frac{\partial}{\partial\theta_j}(h_\theta(x_i)-y) \\
 & = \frac{1}{m}(h_\theta(x_i)-y)x_i
\end{align}
$$

Therefore,
$$
\theta_j := \theta_j - \frac{\alpha}{m}\sum_{i=1}^{m}{[(h_\theta(x_i) - y)x_i]}
$$



[Understanding Correlation Matrix](https://towardsdatascience.com/let-us-understand-the-correlation-matrix-and-covariance-matrix-d42e6b643c22)





<h3 align="center">The Logistic Regression</h3>
Logistic regression is a statistical model that in its basic form uses a logistic function to model a binary dependent variable.

##### Problem Statement:

**1>** Given a list of passengers who survived and did not survive the sinking of the Titanic, predict if someone might survive the disaster ([from Kaggle](https://www.kaggle.com/c/titanic/overview))

**2>** Given a set of images of cats and dogs, identify if the next image contains a dog or a cat ([from Kaggle](https://www.kaggle.com/c/dogs-vs-cats-redux-kernels-edition/overview))



##### Why don't we use Linear Regression to solve these classification problems?

Let's say we have a data set which contains a list of customers and a label to determine if the customer had purchased certain product. In the data set, there are 20 customers. 10 customers age between 10 to 19 who purchased, and 10 customers age between 20 to 29 who didn't purchase. "Purchased" is a binary label denoted by 0 and 1, where 0 denote "customer didn't make a purchase" and 1 denote "customer made a purchase".

If we plot the graph for linear regression we will get the red line which best fits the model.



<img width="500px" align='center' src="https://miro.medium.com/max/621/1*lBc9kCcWfZxlvX-gdrVoUA.png">

Given any age, we will predict the value along Y-axis. If Y is greater than 0.5(above the green line), the customer had purchased the product.



Now the problem arises, when the data is imbalanced. Let's add 10 more customers, whose age is between 60 to 70. Let's train the network and try to find the best fit line.



<img align='center' width="500px" src="https://miro.medium.com/max/621/1*HFrHo41Fe9Zqo32v4_Sbcw.png">

Do you see the problem here?

For few of the customers whose age is in the range of 20-30, the prediction will be wrong.

If we use logistic regression, that's how it tries to solve the above problem.



<img align='center' width='500px' src="https://miro.medium.com/max/612/1*GgUYnIinlmTUnEc8CEesjQ.png">



Now how does it work??



