# Title: Hindsight Experience Replay

# Author: Andrychowicz et al (2018)

#### General Content: Humans learn almost as much from achieving undesired outcome as from desired - Intuition of HER: action sequences would have been successful for task if goal would have been positioned elsewhere. Algorithm is based on universal policies which take state and goal as input. Algorithm replays each episode with different goal than the one the agent was trying to achieve.


#### Keypoints: 

* Often times in hard RL problems: Need to engineer reward function that does not only reflect task at hand but that is also carefully shaped to guide policy optimization. Often times requires domain-specific knowledge.
* DQN: By making GD steps we encourage the approx Q-function to satisfy the Bellman equation
* Polyak-averaged version of parametric model M: Model whose parameters are computed as exponential moving average of parameters of M over time. - used to stabilize learning/slow updating of target network
* Deep Deterministic Policy Gradients (DDPG): Actor-Critic model for continuous action space
	* 2 networks: Actor (target policy), Critic (action-value function approximator)
	* Critic's job: Approx actor's action-value function
	* Critic trained similar to DQN but targets are computed using actions computed by actor.
	* behavioral polciy - noisy versionof target policy
* Universal Function Approximators (UVFA) - incorporate goals in value functions - every episode starts with sampling state-goal pair from distribution

* Sometimes it is easier to train with multiple goals rather than only one - even if we only care about one specific.
* Predicate f function - indicator that states whether or not g is goal for state s
* Map m function - maps a state to a corresponding goal state
* HER - form of implicit curriculum: goals for replay shift from ones easy to achieve by random agent to more difficult ones. But: no explicit control over distribution of initial environment states
* HER performs badly with shaped rewards
	* Discrepancy between optimized shaped reward function and success condition
	* Shaped rewards penalize for inappropriate behavior - hinders exploration!
* How to choose goals which we use for HER part of replay buffer? Also number of goals - k -> FUTURE seems to perform best
	*  FUTURE: replay with k random states from same episode as transition being replayed and obs afterwards
	*  EPISODE: replay with k random states from same episode as transition being replayed
	*  RANDOM: replay with k random states encountered so far in whole training procedure