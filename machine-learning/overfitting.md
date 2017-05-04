# The Problem of Overfitting

### What is overfitting?
Overfitting (or high variance) is a result of having too many features (ex. high order polynomial). The learned hypothesis may fit the training examples very well (J(&theta;) ~ 0) but fail to generalize to new examples.

#### Underfitting
On the other hand, underfitting is a result of having too little features such that the hypothesis fits the data poorly and also fail to create meaningful and useful predictions.

## Addressing overfitting
Overfitting can happen as a result of having too many features and too little training examples.

There are two main options to address overfitting:
  1. Reduce the number of features.
    - Manually select which features to keep (however some of the features we throw away may be useful and this could decrease the accuracy at which we predict)
    - Model selection algorithm.
  2. Regularization
    - Keep all the features, but reduce magnitude/values of the parameters &theta;<sub>j</sub>
    - Works well when we have a lot of features, each of which contribues a bit to predicting y

## Cost function
Regularization helps making the hypothesis more simple by eliminating the influence on certain features, without actually getting rid of these features or changing the form of the hypothesis. We penalize the &theta;s in our cost function if they are too big. 

We modify our cost function like this to regularize all of our theta parameters in a single summation:
> min<sub>θ</sub> (1 / 2m) * ∑<sup>m</sup><sub>i=1</sub> (h<sub>θ</sub>(x<sup>(i)</sup>) − y<sup>(i)</sup>)<sup>2</sup> + λ * ∑<sup>n</sup><sub>j=1</sub> θ<sup>2</sup><sub>j</sub>

where the lambda is the **regularization parameter**. It determines the how much the costs of our theta parameters are inflated. Having a lambda too big could result in underfitting and a lambda too small could not make a change at all. However doing this right could smooth the output of our hypothesis function to reduct overfitting.

*note that we do not penalize &theta;0*

## Regularized Linear Regression
We apply regularization to linear regression with the cost function (as described above):
> J(&theta;) = (1 / 2m) * ∑<sup>m</sup><sub>i=1</sub> (h<sub>θ</sub>(x<sup>(i)</sup>) − y<sup>(i)</sup>)<sup>2</sup> + λ * ∑<sup>n</sup><sub>j=1</sub> θ<sup>2</sup><sub>j</sub>

### Gradient Descent
Since the cost function is modified, our gradient descent algorithm also changes to be:

Repeat until convergence:
>θ<sub>0</sub>:=θ<sub>0</sub> − α \* (1/m) \* ∑<sup>i</sup><sub>m</sub>(h<sub>θ</sub>(x<sup>(i)</sup>) − y<sup>(i)</sup>) \* x<sup>(i)</sup><sub>0</sub>

>θ<sub>j</sub>:=θ<sub>j</sub> − α \* [(1/m) \* ∑<sup>i</sup><sub>m</sub>(h<sub>θ</sub>(x<sup>(i)</sup>) − y<sup>(i)</sup>) \* x<sup>(i)</sup><sub>j</sub> + &lambda; * &theta;<sub>j</sub> / m]

for j is from 1 to n (since we dont penalize 0)

### Normal Equation
To add regularization, the equation is the same as our origina, except that we add another term inside the parentheses:

> &theta; = (X<sup>T</sup> X + &lambda; L)<sup>-1</sup> X<sup>T</sup>y

Where L is a matrix with 0s at the top left and 1's down the diagonal, with 0's everywhere else. It should have dimension n + 1 by n + 1. Intuitively, this is the identity matrix (though we are not including x<sub>0</sub>), multiplied with a real single number &lambda;.

*Note: X is non-invertible if m < n, and may be non-invertible if m = n*

## Regularized Logistic Regression
The cost function for logistic regression using regularization is:
> J(&theta;) = -(1 / m) * ∑<sup>m</sup><sub>i=1</sub> (y<sup>(i)</sup> * log(h<sub>θ</sub>(x<sup>(i)</sup>) + (1 - y<sup>(i)</sup>) * log(1 - h<sub>θ</sub>(x<sup>(i)</sup>))) + λ / 2m * ∑<sup>n</sup><sub>j=1</sub> θ<sup>2</sup><sub>j</sub>

### Gradient Descent
Gradient descent for logistic regression is the same for that of linear regression. Except that the values for the hypothesis changes:

Repeat until convergence:
>θ<sub>0</sub>:=θ<sub>0</sub> − α \* (1/m) \* ∑<sup>i</sup><sub>m</sub>(h<sub>θ</sub>(x<sup>(i)</sup>) − y<sup>(i)</sup>) \* x<sup>(i)</sup><sub>0</sub>

>θ<sub>j</sub>:=θ<sub>j</sub> − α \* [(1/m) \* ∑<sup>i</sup><sub>m</sub>(h<sub>θ</sub>(x<sup>(i)</sup>) − y<sup>(i)</sup>) \* x<sup>(i)</sup><sub>j</sub> + &lambda; * &theta;<sub>j</sub> / m]

where:

> h<sub>&theta;</sub> = 1/(1+ e<sup>-&theta;<sup>T</sup>x</sup>)
