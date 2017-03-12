# Logistic Regression
A classification problem algorithm

## Classification
The simple classification problem has only 2 classes (binary classification problem). ie.
```
y is an element of the set {0,1} where: 
  0: "Negative Class"
  1: "Positive Class"
```

## Hypothesis Representation
We want 0 &le; h<sub>&theta;</sub>(x) &le; 1, where h<sub>&theta;</sub>(x) is the hypothesis function.

The *hypothesis* for Logistical regression model is:
> h<sub>&theta;</sub>(x) = g(&theta;<sup>T</sup>x)
, where g(z) = 1/(1 + e<sup>-z</sup>) -- the sigmoid or logistic function

Therefore the logistical regression model can also be written as:
> h<sub>&theta;</sub>(x) = 1/(1 + e<sup>-&theta;<sup>T</sup>x</sup>)

How do we predict a binary classification with our hypothesis?

> predict y = 1 if h<sub>&theta;</sub>(x) or g(z) &ge; 0.5 (both are equivalent)
    
This is equivalent to saying: z &ge; 0 by definition of g(z)

> predict y = 0 if h<sub>&theta;</sub>(x) or g(z) &lt; 0.5
    
This is equivalent to saying: z &lt; 0 by definition of g(z)

*note: the Sogmoid or logisitic function is between 0 and 1 inclusive.*

### Interpretation of Hypothesis
h<sub>&theta;</sub>(x) = estimated probaility of y = 1 on input x
> h<sub>&theta;</sub>(x) = P(y = 1 | x ; &theta;)

*note: since y = 0 OR y = 1. Since we know P(y = 1 | x ; &theta;) we can also find P(y = 0 | x ; &theta;)*

## Decision Boundary
A line that seperates the region where the hypothesis predicts y = 1 and where it predicts y = 0.
```
Solve for the decision boundary by:
  1) Taking the z parameter of g(z), this would be a function of θ's
  2) Plug in the θ's
  3) Set it equal to zero and solve for x1..xn for n features
```

### Non-linear decision boundaries
You can have these where the x of g(x) is a polynomial function of &theta; (ie. there are polynomial features) instead of a linear one. 

For ex. h&theta;(x) = g(&theta;0 + &theta;1 * x1<sup>2</sup> + &theta;2 * x2<sup>2</sup>) will have a circular decision boundary with radius 1 for &theta;0 = - 1, &theta;1 = 1 and &theta;2 = 1.

*note: the decision boundaries are not determined by the training set but determined by the parameters of theta.*

# Cost Function for Logistic Regression
Remember the cost function J(&theta;) for linear regression. We would like to minimize &theta;. However it turns out that the cost function for linear regression is non-convex. which means that there is no guarentee that gradient descent would reach the absolute minimum if we ran it. What we are looking for is a convex function so that gradient descent can easily find the global minimum of a function.

## The function
J(&theta;) = (1/m) * &Sigma;<sub>1</sub><sup>m</sup>Cost(h&theta;(x),y

**Cost(h<sub>&theta;</sub>(x),y)** =
```
-log(hθ(x))          if y = 1
-log(1-hθ(x))        if y = 0
```
In a more compact/simple method:
> **J(&theta;)** = -(1/m) * &Sigma;<sub>1</sub><sup>m</sup>[y * log(h<sub>&theta;</sub>(x)) + (1 - y) * log(1 - h<sub>&theta;</sub>(x))]

### Cost function properties

1. Cost is 0 if y = 1 and h(x) = 1
2. as h(x) approaches 0, the cost is infinity given y = 1
3. Same vice versa for y = 0

This intuitively makes sense as the cost is exponentially larger if our prediction is different than the actual classification. (the algorithm is penalized by a lot for a wrong prediction)

## Gradient Descent
We apply gradient descent for logistic regression as well to compute the minimum for J(&theta;).

Here the **algorithm** is:
> Repeat until convergence and simultaneously update:

> &theta;<sub>j</sub> := &theta;<sub>j</sub> - &alpha; * &Sigma;<sub>1</sub><sup>m</sup>(h(x<sup>(i)</sup>) - y<sup>(i)</sup>) * x<sup>(i)</sup><sub>j</sub>

A **vectorized** implementation is:
> θ:=θ − α/m * X<sup>T</sup> * (g(Xθ)− Y)

*note: that the definition of h(x) has changed from that of linear regression so the update rule, although it looks alike, is not the exact same as linear regression.*

## Advanced Optimization
To implement logistic regression, we need a way to compute J(&theta;) and the partial derivative of &theta;j with respect to J(&theta;) for j = 0, 1, ... n so that we can give it to gradient descent and let it find the minimum.

There exist other such optimization algorithms:
  - Gradient descent
  - Conjugate gradient
  - BFGS
  - L-BFGS

In comparison with **gradient descent**:
  - Advantages
    - No need to manually pick &alpha;
    - Often faster than gradient descent
  - Disadvantages
    - More complex

## Multiclass Classification
There are multiple classes > 2 involved and we want to classify them. (ex. we want to group incoming emails into these categories: work, friends, family and hobby). We can assign each class a number: y = 0, y = 1 ... etc.

### One vs All (one-vs-rest)
We take any x number of classes and break them up into x binary classification problems. These binary classes represent: y = 0 if the training example is NOT in class z, y = 1 if the training example is in class z. Where z represents 1 to the total number of classes.

In other words:
> Train a logistic regression classifier h<sub>&theta;</sub><sup>(i)</sup>(x) for each class *i* to predict the probability that *y = i*

### Making a prediction
On a new input *x*, we want to pick the class *i* that maximizes: *h<sub>&theta;</sub><sup>(i)</sup>(x)*

(ie. choose the class which is most confident or has the highest probability that *x* is part of their class)
