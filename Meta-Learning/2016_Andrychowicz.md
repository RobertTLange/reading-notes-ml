# Title: Learning to learn by gradient descent by gradient descent

# Author: Andrychowicz et al (2016)

#### General Content: Train an LSTM architecture with GD to perform parameter updates given a gradient. Perform updates coordinate-wise and show improved learning results on MNIST, CIFAR, Neural Art.


#### Keypoints:

* GD: Parameter updates that neglects second order/curvature info
    * More specialized methods when more structure of the problem is known.
    * No free lunch theorems for optimization: setting of combinatorial optimization - no algo can do better than random strategy in expectation

* GD by GD key idea: Substitute the alpha*grad update by a function approximator which takes the gradient as an input - here LSTM
    * Generalization = transfer between problem instances
    * Problem: Having to learn separate set of parameters vs MAML where meta-learning is performed as initial robust param constellation
    * Similar to momentum: Learn to integrate info of gradient histories

* Meta-Objective over whole optimization trajectory with weighting params
    * Weightings=0 for RNN to learn temporal dynamics via BPTT
    * RNN outputs update as well as hidden state
    * Learn by sampling a random function and applying backprop on graph

* Coordinate-wise LSTM updates: Optimizer operates on each dim of params individually.
    * How many forward passes needed for single GD update?
    * Architecture two-layer LSTM

* Training of Optimizer:
    * Sample random datasets/initial param configs
    * Train with ADAM and truncated BPTT with early stopping

* Experiments:
    * Quadratic functions, MNIST, CIFAR-10, Neural Art
    * Does not easily generalize between different function types, i.e. training on sigmoid nonlinearity, generalization to ReLU; Or need for two different LSTMs for fully-connected layer and conv layer in CNN


#### Questions:

* Can we cleverly design the trajectory weightings?
* How is this ever computationally efficient? Train on 100 different MNIST Configs and then deploy single optimization?
* Optimizer unrolled for less than optimization steps... How?
