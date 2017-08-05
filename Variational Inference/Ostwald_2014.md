# Title: A tutorial on variational Bayes for latent linear stochastic time-series models

# Author: Ostwald et al. (2014)

#### General Content: 

Tutorial introduces the Linear Gaussian State Space model (LGSSM) framework and discusses inference using Variational Inference as a computationally efficient alternative to posterior sampling algos such as MCMC.


#### Keypoints: 

* VI as Bayesian identification framework for LGSSM
* Difference between filtering and smoothing:
	* Filtering: P(x_t | y_{1:t}) - preceeding
	* Smoothing: P(x_t | y_{1:T}) - both preceeding and succeeding
* Mean-field approximation: variational distribution over latents factorizes into a set of variables - assumption: respective variables form stochastically independent contributions to the multivariate posterior, which, depending on the true form of the generative model, may have weak or strong implications for the validity of the ensuing posterior inference.
* VB inference theorem for mean-field approximations: Variational free energy is max wrt to latent partition, if the variational distribution is set prop. to exp of expected log joint probability of the target and the params under the variational distribution


#### Summary:
	
* Problem: Want to estimate a continous time process for which only observe a discrete set of point in a bayesian manner.
* Bayesian model identification: Bayesian posterior distribution and model evidence approximation.
* VB for latent stochastic time-series models: Unification of stochastic differential equation modeling and approximate-deterministic Bayesian inference 
* LGSSM:
	* Discretized approx. to a latent linear stochastic differential equation (SDE) 
	* Simple AR(1) model
	* Posterior distributions over the discrete time LGSSM parameter vars may be transferred to posterior distr over the corresponding continuous time latent SDE system using the integral trafo theorem for prob. density functions
* Augmented linear diffusion process <-> Langevin-Equation <-> represents autonomous linear SDE
* Euler-Maruyama discretization: Family of approximations to the solution of SDEs - including the Euler approximation
* Frequentists (log LH - no latents over which we integrate) vs. Bayesians (log marginal LH/model evidence)
* Log model decomposition: Free-energy + KL divergence term
* Variational free energy is always <= than the log model evidence
* Variational calculus: Optimization of functions with respect to functions -> functionals
* VB inference theorem for mean-field approximations suggests an iterative coordinate-wise variational free energy ascent algorithm
* Empirical Bayes: priors are learned from the data
 

#### Questions/To-Do:

* Learn more about Kalman Filters/ 
