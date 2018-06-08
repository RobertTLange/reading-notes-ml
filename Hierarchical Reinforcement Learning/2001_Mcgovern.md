# Title: Automatic Discovery of Subgoals in Reinforcement Learning using Diverse Density

# Author: Amy McGivern and Andrew Barto (2001)

#### General Content: Discover subgoals online based on commonalities across multiple paths to solution. View problem as multiple-instance learning and use diverse density approach to solve it.


#### Keypoints: 
	
* Bottleneck = region in observation space that is visited often on successful paths but not on unsuccessful paths. Interested in "early" (in successful traces) bottlenecks that are persistent throughout learning.
* Idea: Essentially fix exploration tree up to subgoal and continue exploration from there on!
* Multiple-instance learning: Supervised learning problem - system attempts to identify target concept on basis of "bags" of instances (e.g. successful and unsuccessful traces)
* Option = macro but without fixed sequence of actions but policy which allows to interact with env
* 2 room problem - 2 strongly connected regions. Random exploration spends most time within component - unlikely to leave! But bottleneck connects!
* Simple approach to options: randomly generate based on heuristic and add to set of actions - problem: too many actions - bad exploration - need more structure
* Alternative - visitation/count-based approaches: Only use first visitation - agent spends little time in actual bottleneck and more in component
	* Problems: Noisy process, hard to generalize to continouos/large state spaces, no incorporation of negative feedback

* Multiple-instance learning - Diet-terich et al. (1997)
	* Positive bag: Contains at least one positive instance from "target concept" - bottleneck
	* Negative bag: Contains only negative instances
	* Learn concept based on evidence collected from different bags
	* Each trajectory defines a bag - observation vectors correspond to instances within bag
	* Bottleneck = Target concept - agent experiences region somewhere on every successful trajectory and not on all unsuccessful ones

* Diverse Density (DD) approach - Maron, 1998; Maron & Lozano-Pe ́rez, 1998
	* Most diversely dense region in feature space = region with instances from most positive bags and least negative bags
	* DD = posterior of state being concept given positive and negative bags
	* Probability of state being in target concept - gaussian based on distance from particular distance to the target concept
	* Concept with max DD value is output of DD search - for small state spaces use exhaustive search
	* Can use abstract notions of concepts. Most simple: Individual states

* Option Construction:
	* Detect regions which appear early and persist as peaks - keep running average of how often each state appears as a peak - Init to 0 for each state
	* Convergence to series ratio
	* I: if target concept c is reached at t, add all visited states from time t-n to t to set. Do this for all added traces that lead to same target concept - augmentation of option set throughout time
	* $\beta$: Set to 1 when goal is reached or agent no longer in input set. 0 otherwise.
	* $\pi$: Create new value function for option. Give -1 reward on each step and 0 when termination. Learn policy using experience replay.   

#### Questions: 

* To obtain Gaussian do we have to know the target location? - Then not automatic identification!
* How to choose n? - number of states we go for init set - somewhat like length of prod rules
* Static filter (Iba, 1989) to filter option set and throw away unsuccessful ones.
* Improvements seem very small. Why is that?!
* Do we simply augment action set and add options or do we substitute?