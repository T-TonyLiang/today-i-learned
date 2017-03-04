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
where g(z) = 1/(1 + e<sup>-z</sup>)

Therefore the logistical regression model can also be written as:
> h<sub>&theta;</sub>(x) = 1/(1 + e<sup>-&theta;<sup>T</sup>x</sup>)
