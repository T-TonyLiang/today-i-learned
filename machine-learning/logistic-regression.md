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

*note: the Sogmoid or logisitic function is between 0 and 1 inclusive.*

#### Interpretation of Hypothesis
h<sub>&theta;</sub>(x) = estimated probaility of y = 1 on input x
> h<sub>&theta;</sub>(x) = P(y = 1 | x ; &theta;)

*note: since y = 0 OR y = 1. Since we know P(y = 1 | x ; &theta;) we can also find P(y = 0 | x ; &theta;)*

