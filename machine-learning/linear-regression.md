# Linear Regression

## Single Variable

Aka. Linear regression with one variable or univariate linear regression . 

This just means that **y** is a linear function of **x**: h<sub>&theta;</sub>(x) = &theta;<sub>0</sub> + &theta;<sub>1</sub>x, where the &theta;'s are called the **parameters** of the model

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

where j=0,1 represents the feature index number, α a constant that represent how big your "baby steps are" (rate of descent) and the last term is the derivative of the cost function at θ0 and θ1.

*Note: at each iteration J one should simultaneously update the parameters θ0 and θ1. (Required of the algorithm)*
