<h1 align='center'>Session 3</h1>
<h2 align='center'>Recap</h2>
### The Linear Regression:

Linear regression is a kind of statistical analysis that attempts to show a relationship between two variables.

The core idea is to obtain a line that best fits the data. The best fit line is the one for which total prediction error (all data points) are as small as possible. Error is the distance between the point to the regression line.



#### Important Formulas and Parameters:

###### Hypothesis:

<p align="center"><img src="/tex/911580c5a1927b43cd9192f32b75fbee.svg?invert_in_darkmode&sanitize=true" align=middle width=120.67521674999999pt height=16.438356pt/></p>

###### Parameters:

<p align="center"><img src="/tex/26c773ba965e896d62ab0218c5c6afba.svg?invert_in_darkmode&sanitize=true" align=middle width=36.666674549999996pt height=14.611878599999999pt/></p>

###### Cost Function:

<p align="center"><img src="/tex/b1ad1ec07b33ba49ea964257a743d1a3.svg?invert_in_darkmode&sanitize=true" align=middle width=257.36987925pt height=44.89738935pt/></p>



###### Goal:

<p align="center"><img src="/tex/4724967ddea467ca228b8f46943d9afc.svg?invert_in_darkmode&sanitize=true" align=middle width=92.96812634999999pt height=25.2967704pt/></p>



#### Gradient Descent:

Gradient descent is a first-order iterative optimisation algorithm for finding the minimum of a function. To find a local minimum of a function using gradient descent, one takes steps proportional to the negative of the gradient (or approximate gradient) of the function at the current point.

<p align="center"><img src="/tex/4f91a8c5382708dcf5a0c8862793d5b4.svg?invert_in_darkmode&sanitize=true" align=middle width=307.03524389999995pt height=38.5152603pt/></p>





###### Graphical Representation of Gradient Descent Algorithm

<img align='center' src="https://machinelearningmedium.com/assets/2017-08-15-gradient-descent/fig-2-gradient-descent-steps.gif?raw=true">



###### Graph of y = tan(x)

<img align='center' src="https://amsi.org.au/ESA_Senior_Years/imageSenior/2d_40.png">



Here we can see how the tan(x) value, that is nothing but our gradient which is varying based on the angle or theta value.



###### Deriving the Gradient Descent Formula:

<p align="center"><img src="/tex/a39f01deefeaa913e73b072aac9d054d.svg?invert_in_darkmode&sanitize=true" align=middle width=309.99223529999995pt height=140.86712805pt/></p>

Therefore,
<p align="center"><img src="/tex/a4612ca340775dfa321b326ff132851e.svg?invert_in_darkmode&sanitize=true" align=middle width=233.5511541pt height=44.89738935pt/></p>



[Understanding Correlation Matrix](https://towardsdatascience.com/let-us-understand-the-correlation-matrix-and-covariance-matrix-d42e6b643c22)





<h3 align="center">The Logistic Regression</h3>
Logistic regression is a statistical model that in its basic form uses a logistic function to model a binary dependent variable.

#### Problem Statement:

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



Now the question is how does it work??

The first requirement we can see here is that, the output here is not continuous like linear regression. The output here is binary that is either 0 or 1.

For that we will take the help of **Sigmoid Function**



#### Sigmoid Function:





<img align='center' width='600px' src="https://miro.medium.com/max/1200/1*RqXFpiNGwdiKBWyLJc_E7g.png"/>



If **t** goes to infinity, **sig(t)** will become 1 and if **t** goes to negative infinity, **sig(t)** will become 0.



So, if we put **Sigmoid Function** to the hypothesis of **Linear Regression** the output will be in the range of 0 to 1.



#### Hypothesis Function:

<p align="center"><img src="/tex/6f638a929f97ed064264ff102d256d66.svg?invert_in_darkmode&sanitize=true" align=middle width=195.20195804999997pt height=16.438356pt/></p>



#### Cost Function:

Now for the cost function we could have simply used the cost function of linear regression which is 
<p align="center"><img src="/tex/b1ad1ec07b33ba49ea964257a743d1a3.svg?invert_in_darkmode&sanitize=true" align=middle width=257.36987925pt height=44.89738935pt/></p>
But this cost function can't be used with Logistic Regression. It will result in a non-convex cost function. Which results in cost function with local minimas which is a very big problem for Gradient Descent to compute the global optima.



<img align='center' width='500px' src='https://media.geeksforgeeks.org/wp-content/uploads/20190424185211/Cost_func_Non_Convex.jpg'/>



So, for Logistic Regression the cost function is
<p align="center"><img src="/tex/b053c0053f82c8feed58e9c75227d7b3.svg?invert_in_darkmode&sanitize=true" align=middle width=320.19262935pt height=49.315569599999996pt/></p>

##### Cost Function Explanation:



###### for y = 1,

<p align="center"><img src="/tex/5286b1c69a709ae4e51b14faf0ca5a9a.svg?invert_in_darkmode&sanitize=true" align=middle width=212.913261pt height=16.438356pt/></p>

<img align='center' width='500px' src='https://media.geeksforgeeks.org/wp-content/uploads/20190424192136/For_cost_func_y1_new1.jpg'/>




<p align="center"><img src="/tex/a393ddbbb48c4e6fea0dee37a75c01a5.svg?invert_in_darkmode&sanitize=true" align=middle width=497.36337749999996pt height=46.0273968pt/></p>


###### for y = 0,

<p align="center"><img src="/tex/703ed0b847abd2135ef6fc3782eb408f.svg?invert_in_darkmode&sanitize=true" align=middle width=241.22366234999998pt height=16.438356pt/></p>

<img align='center' width='500px' src="https://media.geeksforgeeks.org/wp-content/uploads/20190424191536/For_cost_func_y0.jpg"/>
<p align="center"><img src="/tex/6911cd4568ee9fce805e097d3e7cc628.svg?invert_in_darkmode&sanitize=true" align=middle width=497.36337749999996pt height=46.0273968pt/></p>





##### Simplified Cost Function:

<p align="center"><img src="/tex/dba505fdf7a3bc745557b072bdecd309.svg?invert_in_darkmode&sanitize=true" align=middle width=395.55580514999997pt height=16.438356pt/></p>

