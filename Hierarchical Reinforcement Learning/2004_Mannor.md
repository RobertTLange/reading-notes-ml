# Title: Dynamic Abstraction in Reinforcement Learning via Clustering

# Author: Mannor et al (2004)

#### General Content: Online generation of env map that represents topological structure of state transitions. Afterwards, they use clustering to partition state space into meaningful regions. Furthermore, they consider building a map with preliminary indication of location of interesting (high reward density) regions of state space. A high value gradient indicates significant cluster where additional exploration is potentially beneficial. 


#### Keypoints: 

* Subtask definition in terms of state space - here: consider clusters of states as intermediate stages in learning process, rather than unique states - leads to more robust results.
* Option is then defined as policy that allows agent to efficiently shift from one cluster of states to the other

* Input to clustering algo: agent's recorded state transitions = topological representations of learning task dynamics (+ current value estimates)
	* Algo encourages creation of clusters with small deviation in value function
	* Encourage agent to travel between homogenous clusters <-> increase prob to reach clusters with interesting values

* Process of cluster creation <-> bootstrapping: Clusters are formed early in learning process and are based on rough estimate of env. Using rough est improves exploration.

* Algo:
	1. Interact with env and learn using SMDP Q-learning
	2. Save state transition
	3. If clustering condition is met and clustering not evoked previously:
		* Translate state transition history to graph representation
		* Run clustering algo
		* Learn options for reaching neighbouring clusters

* Activating clustering conditions: Trade-off
	* Want early clustering: Have impact on exploration when most significant 
	* Not too early: Info may not suffice for finding meaningful clusters
	* Solution: Wait until no new staets were encountered for T (task dep param) - indicating stable state-transition model

* Clustering objective: max sum of cluster qualities + sum of separation qualities between clusters
	* Agglomerative approach: start with more clusters than desired and merge clusters by selecting pair whose merging improves objective the most
	* Stop when pre-specified number of clusters is reached

* Topological approach: 
	1. Size of clusters should be roughly the same
	2. Clusters should be well separated

* Value approach: 
	* area with dense concentration of distinct rewards should not be contained in large cluster - careful control for max exploitation   	* area with few rewards - regard as one cluster - agent only wants to exit and explore other areas
