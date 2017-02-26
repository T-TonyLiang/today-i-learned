# Linear Regression

## Single Variable

Aka. Linear regression with one variable or univariate linear regression . 

This just means that **y** is a linear function of **x**: 
>h<sub>&theta;</sub>(x) = &theta;<sub>0</sub> + &theta;<sub>1</sub>x
where the &theta;'s are called the **parameters** of the model

### Cost Function or Squared Error function

How to figure out what the best possible line fit is for the data.

**Idea**: Choose &theta;<sub>0</sub> and &theta;<sub>1</sub> so that h<sub>&theta;</sub>(x) is close to *y* for our training examples (*x*, *y*)

We can actually minimize 1/2*m* * &Sigma;<sup>i</sup><sub>m</sub>(h<sub>&theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)<sup>2</sup> for all i = 1 to *m*, and plug in the equation for h(x) to this formula and minimize &theta;0 and &theta;1

<br/>Therefore, we say the cost function is: J(&theta;0, &theta;1) = 1/2*m* * &Sigma;<sup>i</sup><sub>m</sub>(h<sub>&theta;</sub>(x<sup>(i)</sup>) - y<sup>(i)</sup>)<sup>2</sup> and we minimize this cost function.

This is a commonly used function for regression problems.

*Note: the graph of h(x) is dependent on the the value of &theta; that is chosen, while the the graph of the cost function is like a bowl shaped function, showing all values of &theta;. The minizing value lies at 0 and is the best possible value for the line of best fit.*

## Gradient Descent
An algorithm to find the minimum of an *n* parameter function where you start off in a place and take baby steps towards the steepest path going in the down direction.

The **gradient descent algorithm** is:

>repeat until convergence: θj := θj − α * (∂/∂θ)J(θ0,θ1)

where j=0,1 represents the feature index number, α a constant that represent how big your "baby steps are" (learning rate) and the last term is the derivative of the cost function at θ0 and θ1.

*Note: at each iteration J one should simultaneously update the parameters θ0 and θ1. (Required of the algorithm)*
*Note: For sufficiently small alpha, gradient descent should decrease on every iteration*

### The learning rate α
The learning rate is responsible for how fast a gradient descent algorithm converges. If the learning rate is too small then the algorithm can be slow. However, if the learning rate is too big, it is possible for the algorithm to overshoot the minimum and fail to converge, or even diverge.

**How does the descent converge with fixed steps of α?**
The key is that the learning rate is multiplied by the derivative part (the slope), and even with a fixed rate, as long as the slope gets smaller and smaller, the algorithm will be taking smaller steps towards the minimum and converge.

### Applying gradient descent to linear regression

When we substitute the derivative part of the gradient descent algorithm it becomes:

>θ0:=θ0 − α \* (1/m) \* ∑<sup>(i)</sup>(hθ(x<sup>(i)</sup>)−y<sup>(i)</sup>)

>θ1:=θ1 − α \* (1/m) \* ∑<sup>(i)</sup>(hθ(x<sup>(i)</sup>)−y<sup>(i)</sup>) \* x<sup>(i)</sup>

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

### New Gradient Descent
>repeat until convergence: θj := θj − α * (∂/∂θj)J(θ)
Where θ is the Theta vector and we simultaneous update for each feature j = 0 .. n

Similarily, the partial derivative with respect to &theta;j is:
>θ<sub>j</sub>:=θ<sub>j</sub> − α \* (1/m) \* ∑<sup>i</sup><sub>m</sub>(hθ(x<sup>(i)</sup>)−y<sup>(i)</sup>) \* x<sup>(i)</sup><sub>j</sub>

### Debugging Gradient Descent
1. **Make a plot of J(&theta;) where the x axis is &theta; and the y is the number of iterations**. Hopefully the plot should be downward sloping (decreasing after every iteration) convering to a certain value since gradient descent seeks to minimize J(&theta;). If it doesnt converge, you should re-adjust alpha. (you may have overshot the minimum).
2. Automatic convergence test. Ex. Declare convergence if J decreases by 10^-3 (episilon) in 1 iteration. But it is difficult to choose a proper epsilon

**Note:** it is very difficult to tell in advance how many iterations to needed. Plotting is the best way to debug whats going on.

## Feature Scaling
**Idea:** Make all features are on a similar scale so that gradient descent can converge better and faster.
Therefore we want to scale the features differently so that they are on a similar scale.

More generally, we would like to get every feature into a -1\<x\<1 range or something close to that. Feel free to use division or multiplication.

### Mean normalization
People use mean normalization to get the feature values into the -1 to 1 range. Mean normalization (similar to z score calculation) is subtracting each value by the mean in the training set and then dividing it by the range (max-min) of the value.
> x<sup>(i)</sup> = (x<sup>(i)</sup> - u<sup>(i)</sup>)/s<sup>(i)</sup>

## Polynomial Regression
It is possible to see that the straight line might not be the best fit for the data. It's possible to use linear regression concepts to apply it to polynomial regression. 

For example if we would like to fit a quadratic function to our data. Our hypothesis becomes:
>h<sub>&theta;</sub>(x) = &theta;0 + &theta;1 * x + &theta;2 * (feature)<sup>2</sup>

but we only know the linear computation. Therefore to fit the polynomial line, we set the features to be:

```
x1 = (property)
x2 = (property)^2
```

and so on for other polynomials (even fractionals!!). Note that x1 and x2 are seperate features but they are dependent on the same property. (ex. size of the house, where you want to predict the housing prices).

*Note:* Be sure to apply feature scaling since in this case, the ranges of the features could be large when exponents are applied to it.

## Normal Equation
Alternative to gradient descent which solves for &theta; iteratively, this solves analytically. In some problems, this will give a much more optimal way to solve for the minimum.

**Intuition:** The intuition behind the idea is that the minimum can be found by finding the derivative of the function and setting it to zero. Similarily we can do that with &theta; vectors and matrices. 

### Applying the normal equation
1. Make a table of all the data. with m examples and n features
  - include x0 as 1 for all the rows as well as a column for each of the features (x0, x1, x2 ... xn) and fill out the values
  - create X, a m by n+1 dimensional matrix by copying all of the feature data over, including x0
  - create Y, a m dimensional vector by copying the y values (result values for learning example)
2. Solve for &theta; = (X<sup>T</sup>X)<sup>-1</sup>X<sup>T</sup>y
  - this value of &theta; is the minimal for the cost function. There is a hard proof for this equation that it always gives the minimum value of the cost function.
3. Dont worry about feature scaling
  - not necessary!! :)
  
*Note:* In octave, the equation becomes: `pinv(X'*X)*X'*y`

## Gradient Descent vs Normal Method
Gradient descent: (disadvantages)
  - Need to choose &alpha;
  - Needs many iterations
  
Normal Equation: (disadvantages)
  - Doesnt work well with n is large as (X<sup>T</sup>X)<sup>-1</sup> is a n by n matrix and inverting the matrix is O(n^3)

*Note:* What is a good cut-off for saying n is too big? ~10000 would be a bit slow for the modern computing power - Andrew Ng

### What if X<sup>T</sup>X is non-invertible?
This is usually because:
  - Linearly dependent features (redundant features)
  - Too many features n >= m (delete some or use regularization)
    - this is also not a good idea as you might not have enough data. Less data than features.
