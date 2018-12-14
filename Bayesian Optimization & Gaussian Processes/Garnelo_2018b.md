# Title: Neural Processes

# Author: Garnelo et al (2018b)

#### General Content: Introduce a framework that balances advantages of both deep learning as well as Gaussian processes. A NP is a network-based approx of a stochastic process. It models a distribution over fcts, estimates uncertainty, shifts workload from training to test and is computationally efficient. In its essence it is an VAE structure with a global latent variable that captures epistemic uncertainty. They show powerful results in different problem setting (self-supervised image completion, Bayesian optimization as well as function approx.).


#### Keypoints:

* Sufficient conditions for definition of stochastic process - Kolmogorov Extension Theorem: Exchangeability (invariance of joint distribution to permutations of elements in sequence) and Consistency (marginalization does not change resulting class of distribution) - de Finetti's theorem

* NP = Encoder (h - NN), Aggregator (a - mean operator), Decoder (g - NN) - check out good graphical model visualization

* z - global uncertainty - distribution characterized by data and context specific prior

* Relationship to other models:
    * Conditional NPs: Lack latent variable - unable to produce different samples for same context - no uncertainty estimate
    * Generalization of generative query network - similar training for prediction of new viewpoints in 3D given some context
    * GPs: Deep Kernel Learning, Kernel Approx
    * Meta-Learning - Workload shift to test time

* Amortized inference - Variational inference procedure in which a powerful predictor (NN) is used to predict optimal value of variational parameters based on features - replace local var parameters by fct of data whose parameters are shared across data points.

* Comparison to GPs: No handcrafted kernel, but learning of implicit measure directly from the data - efficient computation.


#### Questions:

* What does image completion with full set of context points do? samples a noisy version? NP seems to perform a lot better in low data/context-point regimes - as many Bayesian methods do.
* No details about architectures - cant replicate anything - good github repo (https://github.com/geniki/neural-processes)
