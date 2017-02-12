# Introduction

What is Machine Learning?

**Machine Learning**: Field of study that gives computers the ability to learn without being explicitly programmed - Arthur Samuel (1959)

**Well-posed learning problem**: A computer program is said to *learn* from experience E with respect to some task T and some performance measure P, if its performance on T, as measured by P, improves with experience E.

## Supervised Learning

*"Supervised learning is the machine learning task of inferring a function from labeled training data. The training data consists of a set of training examples. In supervised learning, each example is a pair consisting of an input object and a desired output value".* - Wikipedia

**Supervised learning** is where the training data contains values of the attribute that we're looking for (ie. the "right answers were given"). The task of the algorithm is to produce more of these values or "right answers". For example: if we were to predict housing prices given their size, the training data already contains the value (housing prices) and our job is to produce more housing prices given the size of the house. 

### Types of problems

**Regression Problem**: Predict results within a continuous valued output

**Classified Problem**: Precit results within a discrete valued output
(ie. map input variables into discrete categories)

## Unsupervised Learning

*Unsupervised learning is a type of machine learning algorithm used to draw inferences from datasets consisting of input data without labeled responses. The most common unsupervised learning method is cluster analysis, which is used for exploratory data analysis to find hidden patterns or grouping in data.* - Mathworks

**Unsupervised learning** is approaching problems with little or no idea of what the results should look like. It is the task of deriving structure from data where we dont know the effects of the variables. 

We can find structure by clustering data based on relationships among variables in the data.

There is no feedback based on the prediction results

### Examples

**Clustering** grouping data into clusters that are related by different variables 

**Non-clustering** find structure in data sets that may seem chaotic
(ie. Cocktail Party Algorithm -- identifying individual voices from various audio overlaps)

## Terminology and Notation

**Training Set**: The set of data that are given

**Training Example**: Each row of data of the training set

**m** = Number of training examples

**x**'s = "input" variable / features

**y**'s = "output" variables / "target" variable

**(x,y)** - one training example

**(x<sup>i</sup>, y<sup>i</sup>)** - i<sup>th</sup> training example

Training Set --> *feeds into* Learning Algorithm --> *outputs* a function **h**

**h** - hypothesis; a function that maps from x's to y's
