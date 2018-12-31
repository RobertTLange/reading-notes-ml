# Title: Random synaptic feedback weights support error backpropagation for deep learning

# Author: Lillicrap et al (2016)

#### General Content: Introduce a first feedback alignment approach to solve the weight transport problem of backpropagation. Forward and backward weights are modeled separately - backward weights align with weight matrix transpose through learning process. Argument follows from positive definiteness of weight and random matrix product and a rotation line of thought.


#### Keypoints:

* Weight transport Problem: downstream errors are fed back to upstream neurons via exact symmetric copy of downstream synaptic weight matrix - neuron "deep" within network has to have precise knowledge of all downstream synapses!

* Possible solutions:
    1. Retrograde transmission of info along axons - problem of slow timescale
    2. Feedback of errors via second network - problem of symmetry assumption of feedforward and feedback connections
    3. Here: Show that even fixed random connections can allow for learning - symmetry not required! Instead implicit dynamics lead to soft alignment between forward and backward weights

* Observations:
    * Feedback weights does not have to be exact: $B \approx W^T$ with $e^TWBe > 0$. rotation within 90 degrees of backprop signal. Learning speed depends on degree!
    * Alignment of $B$ and $W^T$ via adjustment of W (and B) possible

* Feedback alignment:
    * Modulator signal (error-FA) does not impact forward pass post-synaptic activity bu acts to alter plasticity at the forward synapses.
    * FA may encourage W to align with Moore-Penrose pseudoinverse of B - approximate functional symmetry
    * Inference vs learning - towards bayesian approaches

* Experiments:
    * Learns linear function with single hidden layer - learning not slower than backprop
    * Sigmoid nonlinearity and classification task - altered function of post-synaptic activity - learned also to communicate info when 50% of weights were randomly removed
    * More layers 3 hidden layers - as well as backprop and making use of depth - froze layers and trained alternatingly - positive/negative phase?
    * Neurons that integrate activity over time and spike stochastically - synchronous pathways

* Possible Extensions:
    * Fixed spike thresholds/refractory period
    * Dropout/stochasticity

#### Questions:

* Still signed error signal has to be transferred which remains illusive - see target propagation.
* Is result related to Johnson-Lindenstrauss concentration ineq ideas?
* Usage of intricate/more complex architectures of communication of backward error - relation to multi-agent RL
* Relationship to predictive coding
