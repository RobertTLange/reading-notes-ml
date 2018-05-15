# Title: Stochastic NNs for HRL (2017)

# Author: Florensa, Duan, Abbeel

#### General Content: Intend to solve exploration problem by combining HRL with intrinsic motivation. First, they learn skills in a pre-training env using proxy rewards which require minimal info (resembles intrinsic motivation - done with the help of SNN with info-theoretic regularization). Afterwards, they train a separate high-level policy for task on top of skills.


#### Keypoints: 

* eps-greedy exploration/uniform Gaussian exploration noise fail in case of sparse rewards - long-term credit assignment problem - Two approaches:
	* HRL: composition of policies - reduce search space exponentially - require domain knowledge 
	* Intrinsic motivation: guide exploration - hard to transfer knowledge

* Stochastic NN: stochastic units in computation graph
	* feed latent variable with simple distribution as extra input to policy network
	* form joint embedding - concatenation (change bias term) or bilinear integration (change weights of layer) - fed to feedforward network
	* encourage diversity in policies by using mutual info as a regularizer

* Lit: Learning skills in discrete domains:
	* Chentanez et al (2004) - Intrinsically motivated RL
	* Vigorito & Barto (2010) - Intrinsically motivated hierarchical skill learning in structured environments
	* Stolle & Precup (2002) - Learning options in reinforcement learning
	* Mannor et al (2004) - Dynamic abstraction via clustering
	* Simsek et al (2005) - Local graph partitioning

* Partition MDPs into two components (one shared and one task specific), all MDPs have same action space - structural assumption: sharing of same agent space

* Pre-training env: minimal setup required - design of proxy reward should encourage existence of locally otpimal solutions - skills  

* Obtaining skills - sample latent code at beginning of every rollout of net - keep constant throughout entire rollout. After training each of the latent codes corresponds to an interpretable skill - use for downstream tasks 

* Regularization: combat problem of different latent codes corresponding to similar skills
	* add additional reward bonus, prop. to mutual info between latent and current state - estimate by discretization - relative count of how often center of mass state was visited when code z was active

* Freeze K skills after pre-training. For all MDPs train a new manager MM on top of frozen common skills
	*   high-level policy gets full state as input and outputs a parametrization of the categorial distr from which a discrete action/skill z out of K is sampled

* Opitimization via trust region policy optimization - Schulman et al (2015)	   

#### Questions: 

* What has to be manually defined? Learning params of TRPO, number of skills K, two network structures