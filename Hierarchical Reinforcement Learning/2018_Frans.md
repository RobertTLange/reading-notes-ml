# Title: Meta Learning Shared Hierarchies

# Author: Frans, Ho, Chen, Abbeel, Schulman

#### General Content: Combine meta-learning (which uses info from past experiences to learn quickly) with HRL. They generalize the options framework (master policy over subpolicies) to the setting of task distributions (sharing of primitives within).


#### Keypoints: 

* Write hierarchical problem in terms of optimization: set low-level motor primitives such that meta-policy learns quickly
* Then approx problem: repeatedly reset master policy and adapt sub-policies for faster learning.
* MLSH vs meta-learning: MLSH learns quickly over large number of policy gradient updates
* $<\pi_{\phi, \theta}>$
	* $\phi$: params shared between tasks $\{\phi_1,...,\phi_k\}$
	* $\theta$: params learned from scratch per task - state of learning process on that task $\to$ neural network that switches between/chooses subpolicies
		* Master policy that chooses specific $k$ - acts on slower time scale and fixed frequency $N$ 
	* Sample MDP from $P_M$ - then agent is initiated with shared params $\phi$ and randomly initiated $\theta$	
* Max over  $\phi$ the expected reward sequence under prob distr of MDPs

ALGO:

1. Sample M

Repeat:

2. Initialize $agent(\theta, \phi^{t-1})$
3. Warmup period $\to$ optimize master $\theta$
4. Joint update period $\to$ optimize both $\theta, \phi$

* Warmup intuition: Only update $\phi$ if $\theta$ is close to optimal
* Important aspect: No gradient passing between master and subpolicies
* Also: Can easily replace policy gradient used in training with Q-Learning


#### Questions: 

* Possibility of generalizing in one unified network where Master acts as input layer?
* Look at Florensa paper - use info max objective for option discovery - similar to IGGI?
* Problem of still having to specify different learning timescales as well as number of desired subpolicies!