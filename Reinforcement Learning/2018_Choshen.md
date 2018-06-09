# Title: DORA The Explorer: Directed Outreaching Reinforcement Action-Selection

# Author: Choshen, Fox & Loewenstein (2018)

#### General Content: E-values generalize visit-counters so that they can be used to evaluate propagating exploratory value over state-action trajectories. Provide model-free solution by learning such values using SARSA.


#### Keypoints: 

* Exploration via visit-counters: problem of locality
* Exploitation - necessary for learning: want to have better estimations of valuable state-action values and care less about exact values of actions/parts of space where we already know that they are inferior.
* Limitations of random exploration:
	1. Agent does not utilize current knowledge about world to guide exploration
	2. Agent would not be biased in favor of exploring unvisited trajectories more than visited ones.
* Boltzmann distribution based exploration: Captures preference to learn about actions associated with higher rewards
	* Draw actions from softmax distribution ober learned Q-values
	* Still fail at point 2 - not directed towards gaining more info

* Directed exploration: Estimate value of exploration for different s,a pairs
	* Current approaches: counting, recency, value difference - only evaluated for reward one-step ahead
	* Also want to incorporate estimate of how much knowledge could be gained from trajectory starting with action-state pair
	* Treat problem as separate Q-Learning problem and learn exploration values
	* Problem of model-based approaches: Markov property is violated - exploration value decreases with amount of visitations. Exploration value decreases with amount of visitations

* Introduce second MDP - difference to core: no rewards are associated with any (s,a) - init all values to 1
* Learn using SARSA and not Q - not consider potentially highly informative actions never selected - Guarantee that exploration values will decrease when repeating same trajectory.
* Log of E-values: generalization of visit counter with propagation of values along state-action pairs
	* $\gamma_E = 0$: yields counter when taking log of E
	* $\gamma_E > 0$: slower increase of log E than for counter

* Augmenting of rewards with counter-based exploration bonus - replace counter by log E
* Action-selection rules - Add E-values to Q-Values and select actions greedily from that function
* Given a stochastic action-selection rule, every deterministic policy that does not choose actions that are visited too many times until now is determinization of such rule - in-the-limit equivalence derivation. 

#### Questions: 

* Incorporate with HER?! Add goals to exploration behavior