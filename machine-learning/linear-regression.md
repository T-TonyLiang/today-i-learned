# Linear Regression

## Single Variable

Aka. Linear regression with one variable or univariate linear regression . 

This just means that **y** is a linear function of **x**: h<sub>&theta;</sub>(x) = &theta;<sub>0</sub> + &theta;<sub>1</sub>x, where the &theta;'s are called the **parameters** of the model

### Cost Function

How to figure out what the best possible line fit is for the data.

**Idea**: Choose &theta;<sub>0</sub> and &theta;<sub>1</sub> so that h<sub>&theta;</sub>(x) is close to *y* for our training examples (*x*, *y*)

We can actually minimize 1/2*m* * &Sigma;(h<sub>&theta;</sub>(xi) - yi)<sup>2</sup> for all i = 1 to *m*, and plug in the equation for h(x) to this formula and minimize &theta;0 and &theta;1

<br/>Therefore, we say the cost function is: J(&theta;0, &theta;1) = 1/2*m* * &Sigma;(h<sub>&theta;</sub>(xi) - yi)<sup>2</sup> and we minimize this cost function.

