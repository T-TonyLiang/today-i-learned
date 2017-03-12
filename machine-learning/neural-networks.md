# Neural Networks
Another learning algorithm with its goal of mimicing the brain. It was widely used in the 80's and 90's and died down in the late 90s. It is now becoming popular as hardware is fast enough to perform large scale neural network calculations.
It was developed as simulating neurons or networks of neurons in the brain.

## Model Representation
At a very simple level, neurons are basically computational units that take inputs (dendrites) as electrical inputs (called "spikes") that are channeled to outputs (axons). In our model, our dendrites are like the input features x<sub>1</sub> ... x<sub>n</sub> and the output is the result of our hypothesis function. In this model our x<sub>0</sub> input node is sometimes called the "bias unit". It is always equal to 1. 

In neural networks, we use the same logistic function as in classification, 1 / (1 + e<sup>-&theta;<sup>T</sup>x</sup>), yet we sometimes call it a sigmoid activation function. Our "theta" parameters from logistic regression are sometimes called "weights".

The model includes multiple **layers**: Our input nodes (layer 1), also known as the "input layer", go into another node (layer 2), which finally outputs the hypothesis function, known as the "output layer". We can have intermediate layers of nodes between the input and output layers called the "hidden layers."

In the example of one *hidden layer* we label these intermediate *hidden layer* nodes **a<sub>i</sub><sup>(j)** and we denote that as *"activation" of unit i in layer j* (or just "activation units in general"). Similarily we can label &theta;<sup>(j)</sup> as the *matrix of weights controlling function mapping from layer j to layer j + 1*.

The values for each of the "activation" nodes is obtained as follows: 
- a<sup>(2)</sup><sub>1</sub> = g(Θ<sup>(1)</sup><sub>10</sub> * x<sub>0</sub> + Θ<sup>(1)</sup><sub>11</sub> * x<sub>1</sub>  + Θ<sup>(1)</sup><sub>12</sub> * x<sub>2</sub> + Θ<sup>(1)</sup><sub>13</sub> * x<sub>3</sub>)
- a<sup>(2)</sup><sub>2</sub> = g(Θ<sup>(1)</sup><sub>20</sub> * x<sub>0</sub> + Θ<sup>(1)</sup><sub>21</sub> * x<sub>1</sub>  + Θ<sup>(1)</sup><sub>22</sub> * x<sub>2</sub> + Θ<sup>(1)</sup><sub>23</sub> * x<sub>3</sub>)
- a<sup>(2)</sup><sub>3</sub> = g(Θ<sup>(1)</sup><sub>30</sub> * x<sub>0</sub> + Θ<sup>(1)</sup><sub>21</sub> * x<sub>1</sub>  + Θ<sup>(1)</sup><sub>32</sub> * x<sub>2</sub> + Θ<sup>(1)</sup><sub>33</sub> * x<sub>3</sub>)
- h(x) = a<sup>(3)</sup><sub>1</sub> = g(Θ<sup>(2)</sup><sub>10</sub> * a<sup>(2)</sup><sub>0</sub> + Θ<sup>(2)</sup><sub>11</sub> * a<sup>(2)</sup><sub>1</sub>  + Θ<sup>(2)</sup><sub>12</sub> * a<sup>(2)</sup><sub>2</sub> + Θ<sup>(2)</sup><sub>13</sub> * a<sup>(2)</sup><sub>3</sub>)

**TLDR**; It's just a series of logistic regression models where the each layer represents 1 set of logistic regression (as denoted by the superscripts).

The dimensions of these matrices of weights is determined as follows:

> If network has s<sub>j</sub> units in layer j, s<sub>j</sub>+1 units in layer j + 1, then Θ<sup>(j)</sup> will be of dimension s<sub>j+1</sub> × (s<sub>j</sub> + 1).

* note that this is because there will always be x0 -- the bias unit in our inputs but not our output*

### Vectorized implementation of Forward Propogation
Define z<sup>(j)</sup> as the argument to the sigmoid function for layer j, where a<sup>(j)</sup> = g(z<sup>(j)</sup>).

Then we can vectorize the inputs as:
> z<sup>(j)</sup> = &theta;<sup>(j-1)T</sup> \* a<sup>(j-1)</sup> *(Matrix Multiplication)*

Where z<sup>(j)</sup> is a vector of size that is the number of activation nodes for the layer *j*.

Then for the computation of the **hypothesis** (given 3 layers) we add another bias unit a<sup>(2)</sup><sub>0</sub> which is equal to 1 and compute:

> h(x) = a<sup>(3)</sup> = g(z<sup>(3)</sup>)
