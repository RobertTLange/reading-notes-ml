# Title: The free-energy principle: A unified brain theory?

# Author: Karl Friston (2010)

#### General Content: 

THE interdisciplinary introduction to the FEP. Biological agents must minimimize there the long-term average of surprise (free energy as the upper bound!) to ensure their sensory entropy to remain low. Biological systems violate the fluctuation theorem (generalization of second law of thermodynamics) -> probability of entropy decrease becomes exponentially smaller with time.


#### Keypoints: 

* FEP is a very flexible/diverse model that allows to model/account for many different brain structures/functions. Thereby it allows us to unify multiple different neuroscientific theories: Bayesian brain hypothesis, Efficient coding, Predictive coding, synaptic pruning, cell assembly theory, attention, neural Darwinism, RL and value learning, optimal control and DP
* 3 PoVs:
	1. Optimizing brain states makes the representation an approx conditional density on the causes of sensory input. This enables action to avoid suprising sensory encounters.
	2. Optimization of sufficient statistics: Free energy = surprise + KL(recognition density || posterior) -> Minimization leads to a better approximation 
	3. Optimization of actions: Free energy = mixture of accuracy and complexity -> action can only affect accuracy -> active learning to minimize prediction error. Selective sampling of sensory inputs that the brain expects.
* The long-term goal of homeostasis leads to a short-term avoidance of surprise.

#### Summary:

* FEP: Any self-organizing system that is at equilibrium with its environment must minimize its free energy (not equiv. to variational free energy!!).
* Entropy: average self-info or surpirse -> agent dependent!!
	* Low entropy density = An outcome is relatively predictable = Uncertainty Measure 
* Free energy: Measure that bounds surprise on sampling events given a generative model
	* Lower bound on log model evidence[]()
* Homeostatsis: Process of self-system-regulation <-> internal system remains in bounded states 
* Surprise: negative log-prob of outcome. Improbable outcome is surprising.
* Attractor: Set (of points/states) to which a dynamical system evolves after a certain amount of time <-> Statitionary State? 
* Recognition density: Approx prob distribution of causes of the data -> product of inverting the generative model
* Bayesian Brain: Brain as inference machine that actively predicts and explains sensations. Perception: Process of inverting the generative model to access the posterior of the causes given sensory input.
* Hierarchical generative models: Min Free energy <=> optimization of empirical priors. Optimization makes every level in hierarchy accountable to others - leads to internally consistent representation of sensory causes at multiple levels of descriptions.
* Laplace Assumption: Free energy = difference between model prediction and sensations/predicted representations - saddle-point approximation of integral of exp function which uses 2nd order taylor - Gaussian Approximation?
	* Predictive Coding: min free energy corresponds to explaining away prediction errors
* Principle of efficient coding - Barlow's redundancy reduction principle - infomax principle: brain optimizes the mutual info between sensorium and its internal representation 
* Cell assembly theory by Hebb - Plasticity: Groups of interconnected neurons are formed through strengthening of synaptic connections that depends on correlated pre- and postsynaptic activity.
* Correlation theory - Metaplasticity: Selective enabling of synaptic efficacy and its plasticity by fast synchronous activity induced by different perceptual attributes of the same object.
* Hebb plasticity and predictive coding - connected by delta learning rule
* GD on free energy <-> Hebbian plasticity
* Biased competition and attention: neuromodulators - prediction errors with high precision have greater impact on units that encode conditional expectations 
	* Optimization of expected precision in terms of synaptic gain links attention to synaptic gain and synchronisation
* Neural Darwinism: 
	1. Epigenetic mechanisms create primary repertoire of neuronal connections, which are refined by experience-dependent plasticity to produce a secondary repertoire of neuronal groups.
	2. These are selected and maintained through reentrant signalling among neuronal groups. Value modulates the plasticity.
	3. Value is signalled by ascending neuromodulatory transmitter systems and controls which neuronal groups are selected and which not.
	4. The capacity of value to do this is assured by natural selection, in the sense that neuronal value systems are subject to selective pressure.
	* Value is inversely prop to surprise
	* Prior expectations describe small set of states in which we expect high value.

#### Questions: 

* How does entropy relate to tail-thickness and concentration bounds? Are we bounding the KL divergence? Or the distance between the two densities (true generative model vs predicted model)?