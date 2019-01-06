# Title: Dendritic cortical microcircuits approximate the backpropagation algorithm

# Author: Sacramento et al (2018)

#### General Content: MLP with simplified dendritic compartments learned in local PE plasticity fashion. No separate phases needed. Errors represent mismatch between pre input from lateral interneurons and top-down feedback. First cortical microcircuit approach. Analytically derive that such a setup/learning rule approximates backprop weight updates and proof basic performance on MNIST.


#### Keypoints:

* Hypothesis: Pred errors are encoded at distal dendrites of pyramidal neurons - receive input from downstream neurons - in model: error arise from mismatch of lateral local interneuron inputs (SST - somatostatin) - Learning via local plasticity

* 3 Compartment Neuron:
    * Soma + Integration zones: Basal/Apical - convergence of top-down/bottum-up synapses on different compartments - Larkum (2013): Preferred connectivity patterns of cortico-cortical projections

* 2nd Population within hidden layer - Interneurons = lateral + cross-layer connectivity: cancel t-d input - only backprop errors remain as apical dendrite activity
    * Predominantly driven by same layer but cross-layer feedback provides weak nudge for interneurons = modeled as conduc-based somatic input current
    * Modeled as one-to-one between layer interneuron and corresponding upper-layer neuron
    * Empirically justified by monosynaptic input mapping experiments: weak interneuron teaching signal

* Neuron/network Model:
    - Simplifications:
        1. Membrane capacity to 1 and resting potential 0; Background activity is white noise
        2. Modeling of layer dynamics - where vectors represent units
        3. No apical compartment in pyramidal output neurons - 3 compartments seem to suffice as comparison mechanism
    - Qualitative dynamics: error = apical voltage deflection -> propagates down soma -> modulates somatic firing rate -> plasticity at bottom-up synapses
    - Somatic conductance acts as nudging conductance
    - Lateral dendritic projections: interneuron is nudged to follow corresponding next layer pyramidal neuron

* Synaptic learning rules = Dendritic Predictive Plasticity Rules
    - Originally: reduction of somatic spiking error
    - conductance based normalization of lateral projections based on dendritic attenuation factors of different compartments
    - Implementation requires subdivision of apical compartment into two distal parts (t-d input and lateral input from interneurons)

* Prev work:
    * Guergiev: View apical dendrites as integration zones - temp difference between activity of apical dendrite in presence/absence of teaching input = error inducing plasticity at forward synapses. Used directly for learning b-u synapses without influencing somatic activity. HERE: apical dendrite has explicit error represnentation by sim integration of t-d excitation and lateral inhibition - No need for separate temporal phases - continuous operation with plasticity always turned on
    * PC based work - Whittington and Bogacz: Only plastic synapses are those connecting prediction and error neurons. HERE: all connections plastic - errors are directly encoded in dendritic compartments

* Main Results/Experiments:
    * Analytic derivation: Somatic MP at layer k integrate feedforward predictions (basal dendritic potentials) and backprop errors (apical dendritic potentials)
    * Analytic derivation: Plasticity rule converges to backprop weight change with weak feedback limit
    * Random/Fixed t-d weights = FA
    * Learned t-d weights minimizing inverse reconstruction loss = TP
    * Experiments:
        * Non-Linear regression task: Use soft rectifying nonlinearity as transfer fct - Tons of hyperparameters - injected noise current (dropout/regularization effect?)
        * MNIST - Deeper architectures: Use convex combination of learning/nudging

* General notes:
    * Kriegeskorte/DiCarlo/RSA - DNNs outperform alternative frameworks in accurately reproducing activity patterns in cortex - What does this mean? Is DL just extremely flexible/expressive?
    * bottom-up = feedforward, top-down = feedback


#### Questions:

* Neural transfer fct = Activation fct!
* Again tons of hyperparameters to be chosen - How?
* Think of learning (accurate gradient approx) vs architecture (depth, number of hyperparameters) complexity
* Different interneuron types (PV = parvalbumin-positive) - different types of errors (generative)
