<h1 align='center'>Session 3</h1>
### Linear Regression Recap:

Linear regression is a kind of statistical analysis that attempts to show a relationship between two variables.

The core idea is to obtain a line that best fits the data. The best fit line is the one for which total prediction error (all data points) are as small as possible. Error is the distance between the points to the regression line.



#### Important Formulas and Parameters:

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



#### Gradient Descent:

Gradient descent is a first-order iterative optimization algorithm for finding the minimum of a function. To find a local minimum of a function using gradient descent, one takes steps proportional to the negative of the gradient (or approximate gradient) of the function at the current point.

$$
\theta_j := \theta_j - \alpha \frac{\partial}{\partial\theta_j} J(\theta_0, \theta_1)
\\
\alpha = learning \ rate
$$





###### Graphical Representation of Gradient Descent Algorithm

<img align='center' src="https://machinelearningmedium.com/assets/2017-08-15-gradient-descent/fig-2-gradient-descent-steps.gif?raw=true">



###### Graph of y = tan(x)

<img align='center' src="https://amsi.org.au/ESA_Senior_Years/imageSenior/2d_40.png">



Here we can see how the tan(x) value, that is nothing but our gradient which is varying based on the angle.


###### Deriving the Gradient Descent Formula:

$$
\begin{align}
\frac{\partial}{\partial \theta_j} {J_\theta} & = \frac{\partial}{\partial \theta_j} \frac{1}{2m}\sum_{i=1}^{m}(h_\theta(x_i) - y)^2 \\
 & = \frac{1}{m} \sum_{i=1}^{m}(h_\theta(x_i) - y)\frac{\partial}{\partial\theta_j}(h_\theta(x_i)-y) \\
 & = \frac{1}{m}\sum_{i=1}^{m}(h_\theta(x_i)-y)x_i
\end{align}
$$

Therefore,
$$
\theta_j := \theta_j - \frac{\alpha}{m}\sum_{i=1}^{m}{[(h_\theta(x_i) - y)x_i]}
$$



[Understanding Correlation Matrix](https://towardsdatascience.com/let-us-understand-the-correlation-matrix-and-covariance-matrix-d42e6b643c22)





<h3 align="center">The Logistic Regression</h3>
Logistic regression is a statistical model that in its basic form uses a logistic function to model a binary dependent variable.

#### Problem Statement:

**1>** Given a list of passengers who survived and did not survive the sinking of the Titanic, predict if someone might survive the disaster ([from Kaggle](https://www.kaggle.com/c/titanic/overview))

**2>** Given a set of images of cats and dogs, identify if the next image contains a dog or a cat ([from Kaggle](https://www.kaggle.com/c/dogs-vs-cats-redux-kernels-edition/overview))



##### Why don't we use Linear Regression to solve these classification problems?

Let's say we have a data set that contains a list of customers and a label to determine if the customer had purchased a certain product. In the data set, there are 20 customers. 10 customers age between 10 to 19 who purchased, and 10 customers age between 20 to 29 who didn't purchase. "Purchased" is a binary label denoted by 0 and 1, where 0 denote "customer didn't make a purchase" and 1 denote "customer made a purchase".

If we plot the graph for linear regression we will get the red line that best fits the model.



<img width="500px" align='center' src="https://miro.medium.com/max/621/1*lBc9kCcWfZxlvX-gdrVoUA.png">

Given any age, we will predict the value along Y-axis. If Y is greater than 0.5(above the green line), the customer had purchased the product.



Now the problem arises when the data is imbalanced. Let's add 10 more customers, whose age is between 60 to 70. Let's train the network and try to find the best fit line.



<img align='center' width="500px" src="https://miro.medium.com/max/621/1*HFrHo41Fe9Zqo32v4_Sbcw.png">

Do you see the problem here?

For a few of the customers whose age is in the range of 20-30, the prediction will be wrong.

If we use logistic regression, that's how it tries to solve the above problem.



<img align='center' width='500px' src="https://miro.medium.com/max/612/1*GgUYnIinlmTUnEc8CEesjQ.png">



Now the question is, how does it work??

The first requirement we can see here is that the output here is not continuous like linear regression. The output here is binary that is either 0 or 1.

For that, we will take the help of **Sigmoid Function**



#### Sigmoid Function:





<img align='center' width='600px' src="https://miro.medium.com/max/1200/1*RqXFpiNGwdiKBWyLJc_E7g.png"/>



If **t** goes to infinity, **sig(t)** will become 1 and if **t** goes to negative infinity, **sig(t)** will become 0.



So, if we put **Sigmoid Function** to the hypothesis of **Linear Regression** the output will be in the range of 0 to 1.



#### Hypothesis Function:

$$
h_\theta(x) = Sigmoid(\theta_0 + \theta_1x)
$$



#### Cost Function:

Now for the cost function we could have simply used the cost function of linear regression which is 
$$
J(\theta_0, \theta_1) = \frac{1}{2m} \sum_{i=1}^m {(h_\theta(x^{(i)}) - y^{(i)})^2}
$$
But this cost function can't be used with Logistic Regression. It will result in a non-convex cost function. Which results in cost function with local minimas which is a very big problem for Gradient Descent to compute the global optima.



<img align='center' width='500px' src='https://media.geeksforgeeks.org/wp-content/uploads/20190424185211/Cost_func_Non_Convex.jpg'/>



So, for Logistic Regression the cost function is
$$
Cost(h_\theta(x),y) = 
\begin{cases}
-\log(h_\theta(x)),  & \text{if $y$=1} \\
-\log(1-h_\theta(x)), & \text{if $y$=0}
\end{cases}
$$

##### Cost Function Explanation:



###### for y = 1,

$$
Cost(h_\theta(x),y) = -\log(h_\theta(x))
$$

<img align='center' width='500px' src='https://media.geeksforgeeks.org/wp-content/uploads/20190424192136/For_cost_func_y1_new1.jpg'/>




$$
Cost\ = 0\ for\ h_\theta(x) = 1\\
Cost\ = \infin\ for\ h_\theta(x) = 0\\

If\ h_\theta(x)=0,\ it\ is\ similar\ to\ predicting\ P(y=1|x;\theta) = 0
$$


###### for y = 0,

$$
Cost(h_\theta(x),y) = -\log(1-h_\theta(x))
$$

<img align='center' width='500px' src="https://media.geeksforgeeks.org/wp-content/uploads/20190424191536/For_cost_func_y0.jpg"/>
$$
Cost\ = 0\ for\ h_\theta(x) = 0\\
Cost\ = \infin\ for\ h_\theta(x) = 1\\

If\ h_\theta(x)=1,\ it\ is\ similar\ to\ predicting\ P(y=0|x;\theta) = 0
$$





##### Simplified Cost Function:

$$
Cost(h_\theta(x),y) = -y\log(h_\theta(x)) - (1-y)\log(1-h_\theta(x))
$$



##### Derivation of Gradient Descent Formula


$$
h_\theta(x) = \sigma(z) = a\\
where,\\
z = \theta_0x_0 + \theta_1x_1 + \theta_2x_2 + ...\\
\\~\\~\\
Loss = L(h_\theta(x),y)\\
\\~\\~\\
\frac{\partial{L}}{\partial{\theta_0}}=\frac{\partial{L}}{\partial{a}}\frac{\partial{a}}{\partial{z}}\frac{\partial{z}}{\partial{\theta_0}}\\
\\~\\
\begin{align}
\frac{\partial{L}}{\partial{a}} & = \frac{\partial{(-y\log{a} - (1-y)\log{1-a})}}{\partial{a}}\\
&=-y\frac{1}{a} -(-1)\frac{1-y}{a-a}
\end{align}\\
\bbox[5px,border:2px solid red]{
\frac{\partial{L}}{\partial{a}}=\frac{-y}{a} + \frac{1-y}{1-a}
}\\
\bbox[5px,border:2px solid red]{
\frac{\partial{a}}{\partial{z}} = a(1-a)
}\\
\bbox[5px,border:2px solid red]{
\frac{\partial{a}}{\partial{\theta_0}} = x_0
}
\\~\\~\\
\frac{\partial{L}}{\partial{\theta_0}} = (a-y)x_1\\
\bbox[5px,border:2px solid red]{
\frac{\partial{L}}{\partial{\theta_0}} = \sum_{i=1}^{m}(h_\theta(x_i)-y)x_1
}\\
\\~\\~\\
\bbox[5px,border:2px solid red]{
\theta_i := \theta_i -\alpha\frac{\partial{L}}{\partial{\theta_i}}
}\\
$$



small changes to make texify work 