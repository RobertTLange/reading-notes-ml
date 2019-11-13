# Title: Saliency Benchmarking made easy: Separating models, maps and metrics

# Author: Kümmerer et al. (2018, ECCV - Bethge Lab)

#### General Content:
In current benchmarks no single saliency map can perform well - need to disentangle model, metrics and maps. This allows to derive closed-form optimization solutions for the specific metrics given model as a log probability density over fixation points. By submitting such a model and performing this optimization within the benchmarking setup, all models can be compared in a fair way across all different metrics. Show that if you do so DeepGaze II (their model) performs best!

**Note**: Discussed in vision reading group!

#### Key take-away for own work:

#### Keypoints:

* Salience problem has developed into a prediction of fixation problem.

* DeepGaze II - VGG based with readout network
    - output map + blurring + softmax + center bias = probability distribution
    - How to backpropagate through the gaussian noise?
    - If noise is fixed and stored than simple linear trafo
    - Center bias = form of average fixation across all images
    - 4 layers of 1×1 convolutions readout network
    - Optimizes the information gain

* How to compare models?! Inconsistent variety of metrics
    - Proposition: Disentangle model & map in terms of Bayesian Decision Theory
    - Saliency model: prob model of fixation density prediction = Posterior
    - Saliency map: metric-specific prediction derived from model density. = Prediction
    - Saliency metric: Performance measure for a saliency map on ground truth data = Utility Function

* Task-independent probability distribution
* Task-dependent error metric

* Problem: Optimization - max utility with respect to metric - returns saliency map
    - map that optimizes specific metric is performing best on that metrics
    - show example with model corresponding to true density!

* Proposed solution:
    - Transform model into log probability space
    - Perform optimization for all metrics at evaluation time
    - Compare across models that are all optimized for the same metric.

* Different metrics to evaluate on:
    * AUC = equalized prob distr to yield a uniform histogram over all pixels - 2 alternative forced choice test - two pixels which one attended to which not
    * sAUC = dividing the prob density by center bias density and equalizing
    * NSS/IG = Probability density
    * CC/KL = probability density convolved with Gaussian kernel

* Benchmarks: MIT1000, LSUN

* Argue that IG is "ideal" optimization metric because reflects all info in structure of fixation density independent of particular metric. Can formulate as a multi-task problem?

#### Questions:

* How much is lost in the tansformation to log density space?!
    - DeepGaze directly outputs density while the others have to be transformed
    - How is this transformation actually done? MC sampling and approx distribution?
    - Then problem of high-dim pixel space - cant sample enough.
