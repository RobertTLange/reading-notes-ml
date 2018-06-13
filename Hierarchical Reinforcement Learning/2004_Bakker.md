# Title: Hierarchical Reinforcement Learning Based on Subgoal Discovery and Subpolicy Specialization

# Author: Bram Bakker and Jürgen Schmidhuber


#### General Content: Idea - let high-level poilicy identify subgoals that precede overall goals. Simultaneously, let low-lebel policies learn to reach subgoals set by higher level. Also learn which subgoals subpolicies are capable of reaching - specialization.


#### Keypoints: 

* HASSL: Hierarchical Assignment of Subgoals to Subpolicies Learning
	* 2 layer hierarchy (can be generalized) 
* Specialization <-> Generalization
	* state-specific reaching of goals <-> single sub-policy to reach multiple goal states
	* focus on parts of obs space relevant to specialization <-> generalize within specialization 

* High level observation and high level goal state are included in input vector ("command" of high-level policy) 
* Time-out-value: max number of low-level actions that policy can execute before control returns to higher level
* Learning done with advantage function learning
	* decrease value of subgoal if it was not reached
	* gradient expressions for advantage function, weights of prarametrized value function amd C-values which measure capability of low level policy to reach high level goal state

* Production of high-level obs - requirement: clustering of primitive low-level obs s.t. locally neighbouring states tend to be clustered together
	* Use unsupervised learning vector quantization technique ARAVQ: Adaptively allocates new model vector if the latter's Euclidean distance to any existing model vector exceeds threshold
	
* Other algorithms: Associate subgoals with primitive, low-level observations rather than high-level obs.    