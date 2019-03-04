# Title: Theories of Error Propagation in the Brain

# Author: Whittington & Bogacz (2019)

#### General Content: Review article on bio-plausible alternatives to backprop. Goal is not to state that the brain exactly performs backprop but that other rules that achieve similar performance are plausible alternatives. Differentiate between two main classes of models: Temporal-Error (learning via plasticity and target constraining output activity) vs Explicit-Error (learning via Hebbian rule and explicit error computation/tracking)


#### Keypoints:

* Bio-plausible problems with backprop:
    * Updates depend on activity/comps of all downstream neurons - non-local
    * Symmetry idea of feedforward and back pathways - question of bidirectional connections - still need form of alignment
    * Neurons send continuous output (rate-based) - real neurons spike. Also linear summation as aggregation of inputs

* Alternatives:
    * Neuromodulators may guide plasticity by carrying form of global error. Slow and bad scaling.
    * Pre-/Post-Synaptic activity: STDP/Pyramidal neurons/cortical microcircuits
    * Rely on similar framework: Forward + Back -> energy minimization?

* Temporal-Error Models: Error is def as difference in activity across time.
    * Contrastive learning: Error decomposition into target indep activity part (anti-Hebbian - unlearn associations - only prediction) and target dep activity part (Hebbian - learn new assocs - output layer set to target activity)
        * Problem: Need form of phase signal that is global! Info local via oscillatory rhythms such as hippocampal that oscillations? Neurons in output layer are driven by feedforward inputs in one part of cycle and forced to take value of target pattern in other

    * Continuous Update Model: Local plasticity rule based on rate of change of activity. Still requires signal since no plasticity should take during prediction

* Explicit-Error Models: Close approx of errors that would be computed in backprop setting
    * Predictive Coding Model: Error nodes 1-to-1 association with value nodes. During prediction activity is prop between value nodes via error nodes. Convergence to equilibrium in which the nodes decay to zero and all value nodes have same values as ANN. During training error nodes dont go to zero but to backprop error - adapt weights using Hebbian rule.
        * Problem: Inconsistent 1-to-1 connectivity

    * Dendritic Error Model: Error representation in apical dendrite. Local error computation via cortical microcircuits, i.e. comparison with lateral inhibitory interneuron activity. Plasticity guidance via plateu potentials.
        * PCs are exctitatory <- negativ inhibition is provided by interneurons - hard to train their weights - need higher level projections
        * Show form of intuitive equivalence to backpropagation - like Sacramento

* Computational comparison:
    * T-E: Mechanism for informing whether target pattern constrains output neurons (phase signaling) - not needed for E-E
    * Predictive Coding needs to propagate twice as many neurons (travel via error neuron)! - Evolutionary benefit for fewer neurons and faster propagation
    * Dendritic model: Learning all connections in parallel can lead to problems. Ideally first learn inhibitory neurons

* Experimental data: No evidence for separate error neuron population

* Vogels et al (2011) - learning rule in which the direction of modification depends on neurons in equilibrium as in PC model, can arise from alternate form of STDP

* Martinotti cells - receive inout from pyramidal neurons in same cortical area and project to their apical dendrite

* Question of speed: Pred Coding - slow prediction; Dendritic error model - slow training (but can get faster with time)

* Equilibrium propagation: Energy based models and minimization of free energy - entropy/ELBO optimization. Markov blanket ideas - strong connectivity leads to similar activity

#### Questions:
* Robustness without symmetry in forward and backward weights?
* Efficient one-shot learning support?
* Anti-Hebbian <-> Hebbian: Relationship to target/forward phase in Guergiev et al (2017)
