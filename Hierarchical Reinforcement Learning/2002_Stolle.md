# Title: Learning Options in Reinforcement Learning
# Author: Martin Stolle and Doina Precup (2002)


#### General Content: State visitation approach to option discovery. Explicitly construct a set of options and not individual options! They pose a series of random tasks in a static env and let the agent solve them. The agent collects statistics of frequencies of occurance of different states. Intuition: If states occur frequently on trajectories that represent solutions to random tasks, then states may be important.


#### Keypoints: 

* Differences to diverse density approach:
	1. No assumption of what a good/bad trajectory is. Only assume agent to be confronted with different tasks in same env and allow for exploration. Makes sense since we cook in the same kitchen everyday ;)
	2. Explicit construction of set of options and not greedy construction of individual ones.
* Get init and term sets first and then simply learn intra-option policy using pseudo-rewards

* Algorithm:
	1. Select number of start and target states S, T according to some distribution (e.g. uniform)
	2. For each pair (S,T)
		* Perform N_train Q-L episodes to learn policy from S to T
		* Perform N_test episodes using greedy policy eval
		* For all states s count number of total occurances n(s)
	3. Repeat until number of desired options is reached:
		* T_max = argmax_s n(s) as target state for option
		* Compute n(s, T_max): number of times each s occurs on path to T_max
		* Compute rho(T_max) = avg_s n(s, T_max)
		* Select all states s for which n(s, T_max) > rho(T_max) to be in init set
		* Complete init set by interpolating between states (domain specific)
		* Decrease visitation counts for all states by number of visits to states on trajectories going to T_max - prevent several options going to neighbouring subgoals (redundancy)
	4. For each option learn internal policy achieved by giving high reward for entering T_max and no rewards otherwise. Learn by Q.

#### Questions: 

* Need to do a lot of pretraining!!! For each pair of S, T!