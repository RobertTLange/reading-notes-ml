# Title: Q-Cut - Dynamic Discovery of Sub-Goals in Reinforcement Learning

# Author: Ishai Menache, Shie Mannor, and Nahum Shimkin (2002)

#### General Content: Graph theoretic approach for automatic detection of subgoals in dynamic envs. Agent creates online map of process history and uses max-flow/min-cut algo to identify bottlenecks. Policies to reach those are learned separately. Segemented Q-Cut generalizes this by using previously identified bottlenecks for state space partitioning. This seems necessary to identify additional bottlenecks in complex environments


#### Keypoints: 

* Approaches to subgoal discovery:
	* landmark states
	* states with non-typical reinforcement - high reinforcement gradient
		* problem: hard to find meaningful subgoals when sparse rewards 
	* bottleneck = freq of appearance + success condition
		* problem: needs lots of exploration to distinguish bottlenecks and "regular" states

* Here: Consider bottlenecks as "border states" of strongly connected areas
	* local criterion: choose bottlenecks based on qualities of state itself
	* global criterion: choose bottlenecks based on all state transitions
	* think of MDP as flow problem:
		* Nodes = States
		* Arcs = State transitions
		* Bottlenecks = accumulation nodes where many paths coincide - support between loosely connected areas    

* Cut procedure for recursive decomposition of state space:
	* Divide state space into segments to simplify overall learning task
	* Separate consideration of each segment

* Algo:
	1. Interact with env, learn using SMDP Q-learning
	2. Save state transition history
	3. If activating cut conditions are met, choose $s,t \in S$ and perform Cut(s,t)

* Cut(s,t):
	1. Translate state transition history into graph representation
	2. Find MinCut partition $[N_s, N_t]$ between s and t 
	3. If cut quality good: create option, learn policy with ER

* Choosing s,t: Task dependent
	* use distance metric between states
	* use env reset structure

* Activating cut conditions: constant rate slower than actual experience frequency
	* depends on computational resources/goodness of found s,t pair

* Graph construction - capacity:
	* frequency based: too much weight to freq visited states that might not be bottlenecks
	* fixed: same significance to all visited states
	* relative frequency - seems to perform best

* Cut quality: "significant" s-t cuts: small number of arcs <-> enough states in $N_s$ and $N_t$
	* Look for small number of bottleneck states, separating significant balanced areas in state space
	* Use metric called ratiocut bipartitioning metric related to size of both sets and number of arcs between them.     
	* Only consider cuts whose quality is above threshold

* Q-Cut works well when one bottleneck sequentially leads to the other.
	* Segmented version: Use discovered bottlenecks as segmentation tool - divide and conquer: work on small segments of states in order to find additional bottlenecks and corresponding options   	       