# Title: Assessing the Scalability of Biologically-Motivated Deep Learning Algorithms and Architectures

# Author: Bartunov et al (2018)

#### General Content: Extent the target propagation algorithm to not require exact gradient at penultimate layer. Test alternative learning rules in more complicated settings (CIFAR/ImageNet) and differentiate between locally and fully connected architectures. Very good review but not much additional innovation. Behavioral + Physiological Realism


#### Keypoints:

* Problems with backpropagation
    * Feedback connections require exact copy of feedforward connections = Weight transport
    * Info propagation does not influence "neural activity" - does not conform to any known biological mechanism

* Feedback alginment: Use random weights in backward pass to deliver info to earlier layers
    * Still requires delivery if signed error via distinct pathway
    * Direct/Broadcast FA - connect feedback from output layer directly to all previous ones

* Contrastive Hebbian Learning/Generalized Recirculation: Use top-down feedback connections to influence neural activity and differences to locally approx gradients
    * Positive/negative phase - need settling process - Likely to slow for brain to compute in real time

* Target Propagation: Trains distinct set of feedback connections defining backward activity propagation
    * Connections trained to approximately invert feedforward connections to compute target activites for each each layer by successive inversion - decoders
        * Reconstruction + Forward loss
        * Different target constructions
    * Vanilla TP: Target computation via propagation from higher layers' targets backwards through layer-wise inverses
    * Difference TP: Standard delta rule with additional stabilization from prev reconstruction error. Still needs explicit grad comp at final layer
    * Not tested on data more complex than MNIST

* Simplified Difference Target Propagation: Computation also for penultimate layer with help of correct label distribution - removes implausible gradient communication
    * Need diversity in targets - problem of low entropy of classification targets
    * Need precision in targets - poor inverse learned
    * Combat both problems/weakness of targets with help of auxiliary output resembling random features from penultilmate hidden layer
    * Parallel vs alternating inverse training - simultaneous more plausible

* Weight-Sharing is not plausible - regularizes by reducing number of free parameters

* Experiments - Mostly negative results:
    1. None of existing algos is able to scale up - Good performance MNIST/Somewhat reasonable on CIFAR/Horrible on ImageNet - Seems like weight-sharing is not key to success
    2. Need for behavioral realism - judged by performance on difficult tasks
    3. Hyperparameter Sensitivity
        * First fix "good" architeture and then optimize
        * Use hyperbolic tanh instead of ReLu - work better


#### Questions:

* How could the brain do weight sharing - is approximate again satisfactory/functional approx?
* Think more about communication: MARL agents learning communication channels
