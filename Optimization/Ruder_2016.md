# Title: An Overview of Gradient Descent Optimization Algorithms (2016)

# Author: Sebastian Ruder

#### General Content: 

Paper summarizes different GD algorithms. Introduces batch GD as well as minibatch and plain SGD. Afterwards, the paper discusses pros/cons of adaptive learning rates and outlines Adagrad, Adadelta, RMSprop and Adam. 

#### Keypoints: 

Adaptive learning rates for non-convex DL optimization schemes outperform vanilla SGD with annealing in terms of speed of convergence. But SGD seems to prevail as the "simple" dominant non-convex optimization algorithm.

#### Summary:
	
* **Batch GD**: Performs one update for the full dataset. This means that the the gradient of the loss function is evaluated for all input/output training pairs. There is no stochastic element. Guaranteed to converge to optimum (global if fct convex, otw. to local)

* **SGD**: Performs parameter updates for each datapoint. One epoch corresponds to an update performed for each single (x,y) pair (for loop). It is stochastic in the order in which the updates are performed. It is important to shuffle the data before the next epoch.

* **Mini-batch GD**: Combines Batch GB with plain SGD and performs update for random batches of datapoints. Benefits: reduces update variance - more stable convergence; can use optimized matrix operations - speeds up computation time
	
* **Adaptive Learning Rates**:
	* *Momentum*: Adds fraction of previous update vector in order to build up speed. Momentum term increases if multiple gradients point in the same direction. Danger of blindly going to fast.
	* *Nesterov Accelerated Gradient (NAG)*: Does not only look at the previous gradients but tries to anticipate future by evaluating the gradient of the loss function at a point that is close to the next parameter value. "Anticipatory" update prevents us from going to fast.
	* *Adagrad*: Larger learning rate for parameters which change infrequently. Smaller updates for parameters that change frequently. Learning rate is set inversely to the sum of previous squared gradients. Performs best for sparse data. Eliminates need to manually tune the learning rate.
	* *Adadelta*: Restricts the window of previous gradients. Sum of gradients is recursively defined as a decaying average of all past squared gradients. - RMS: root mean squared error criterion
	* *RMSprop*: Almost identical to Adadelta. Specific parameter suggestions.
	* *Adam*: Adaptive Moment Estimation - Does not only store squared gradients (variance) but also the simple gradients (mean) again with exponential decay. Initialization pulls parameters to zero - bias-corrected version exists.

* **Random stuff**:
	* Curriculum Learning: supply training examples in a "meaningful" manner - increase the degree of difficulty (don't shuffle)
	* Batch Normalization: Zero mean, unit variance - reapply normalization for every mini-batch. Allows for higher learning rates without having to worry about initialization parameters. Also acts as a form of regularization.
	* Early Stopping: Check convergence with the behavior of the validation set error and not with the parameter change.
	* Gradient noise: Adding noise to gradient update makes algo more robust

#### Questions: 

* What is automatic differentiation? - Same as backprop? Allows to easily obtain gradients
* Exploration-Exploitation trade-off/Bayesian Optimization framework