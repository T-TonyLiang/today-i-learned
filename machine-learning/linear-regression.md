# Linear Regression

## Single Variable

Aka. Linear regression with one variable or univariate linear regression . 

This just means that **y** is a linear function of **x**: 
>h<sub>&theta;</sub>(x) = &theta;<sub>0</sub> + &theta;<sub>1</sub>x, where the &theta;'s are called the **parameters** of the model

### Cost Function or Squared Error function

How to figure out what the best possible line fit is for the data.

**Idea**: Choose &theta;<sub>0</sub> and &theta;<sub>1</sub> so that h<sub>&theta;</sub>(x) is close to *y* for our training examples (*x*, *y*)

We can actually minimize 1/2*m* * &Sigma;(h<sub>&theta;</sub>(xi) - yi)<sup>2</sup> for all i = 1 to *m*, and plug in the equation for h(x) to this formula and minimize &theta;0 and &theta;1

<br/>Therefore, we say the cost function is: J(&theta;0, &theta;1) = 1/2*m* * &Sigma;(h<sub>&theta;</sub>(xi) - yi)<sup>2</sup> and we minimize this cost function.

This is a commonly used function for regression problems.

*Note: the graph of h(x) is dependent on the the value of &theta; that is chosen, while the the graph of the cost function is like a bowl shaped function, showing all values of &theta;. The minizing value lies at 0 and is the best possible value for the line of best fit.*

## Gradient Descent
An algorithm to find the minimum of an *n* parameter function where you start off in a place and take baby steps towards the steepest path going in the down direction.

The **gradient descent algorithm** is:

repeat until convergence: θj:=θj−α*(∂/∂θ)J(θ0,θ1)

where j=0,1 represents the feature index number, α a constant that represent how big your "baby steps are" (learning rate) and the last term is the derivative of the cost function at θ0 and θ1.

*Note: at each iteration J one should simultaneously update the parameters θ0 and θ1. (Required of the algorithm)*

### The learning rate α
The learning rate is responsible for how fast a gradient descent algorithm converges. If the learning rate is too small then the algorithm can be slow. However, if the learning rate is too big, it is possible for the algorithm to overshoot the minimum and fail to converge, or even diverge.

**How does the descent converge with fixed steps of α?**
The key is that the learning rate is multiplied by the derivative part (the slope), and even with a fixed rate, as long as the slope gets smaller and smaller, the algorithm will be taking smaller steps towards the minimum and converge.

### Applying gradient descent to linear regression

When we substitute the derivative part of the gradient descent algorithm it becomes:

>θ0:=θ0−α\*((1/m)\*∑(hθ(xi)−yi))

>θ1:=θ1−α\*((1/m)\*∑(hθ(xi)−yi)xi)

*You can try deriving the partial derivative if you wish, not done here*

**Batch Gradient Descent**: The method of gradient descent that looks at every example in the entire training set on every step.

*Note: Gradient descent can be susceptible to local minima but for the problem of regression gradient descent will always converge to the global minimum. Since J is a convex function*

## Multivariate Linear Regression
More than 1 features affecting the output variable.

let *n* be the number of features, *x<sup>(i)</sup>* be a vector in R<sup>n</sup>representing the input features of a training example and *x<sup>(i)</sup><sub>j</sub>* be the jth feature of the ith training example. 

### New Hypothesis
>h<sub>&theta;</sub>(x) = &theta;<sub>0</sub> + &theta;<sub>1</sub>x<sub>1</sub> + &theta;<sub>2</sub>x<sub>2</sub> + &theta;<sub>3</sub>x<sub>3</sub> ... &theta;<sub>n</sub>x<sub>n</sub>

Another way of writing it is to define x<sub>0</sub> = 1 and let x be a n+1 dimensional vector: [x0, x1, x2, x2 ... xn] and let &theta; be a n+1 dimensional vector: [&theta;0, &theta;1, &theta;2, &theta;3... &theta;n]. Then:

>h<sub>&theta;</sub>(x) = &theta;<sup>T</sup>x 
(Theta transposed x -- where Theta transposed is a 1 by n+1 matrix since it is transposed and x is a n+1 by 1 matrix)

