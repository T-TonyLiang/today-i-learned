# Linear Regression

## Single Variable

Aka. Linear regression with one variable or univariate linear regression

How do we represent the hypothesis function?

This just means that **y** is a linear function of **x**:

h<sub>&theta;</sub>(x) = &theta;<sub>0</sub> + &theta;<sub>1</sub>x

where the &theta;'s are called the **parameters** of the model

### Cost Function

How to figure out what the best possible line fit is for the data.

Idea: Choose &theta;<sub>0</sub> and &theta;<sub>1</sub> so that h<sub>&theta;</sub>(x) is close to *y* for our training examples (*x*, *y*)

Minimize &theta;<sub>0</sub> and &theta;<sub>1</sub>

So we can actually minimize 1/2*m* * &sigma;(h<sub>&theta;</sub>(xi) - yi)<sup>2</sup> for all i = 1 to *m*. 

We can plug in the equation for h(x) to this formula and minimize &theta;0 and &theta;1

We say the cost function is: J(&theta;0, &theta;1) = 1/2*m* * &sigma;(h<sub>&theta;</sub>(xi) - yi)<sup>2</sup> and we minimize.


