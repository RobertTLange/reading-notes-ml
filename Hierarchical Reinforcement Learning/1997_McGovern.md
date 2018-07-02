# Title: Roles of Macro-Actions in Accelerating Reinforcement Learning

# Author: McGovern et al (1997)

#### General Content:

Macro-actions are a form of commitment defined by closed-loop policies with termination condition. The appropriateness of construction determines whether or not they make learning faster or slow it down. The influence can be broken down into 2 parts: Effect on exploration and effect on value information propagation/learning. Authors derive basic experiments to test both effects and show that value backprop seems more important.

#### Keypoints:

* Macro-operators: common in robotics and to aid state-space search
* Original literature: Korf (1985) and Iba (1989) - here: application to RL
* Macros: Compress effective length of solution by chunking together primitive actions.
* Macro Def.: Agent can choose macro or primitive action from any state unless agent is already executing a macro-action. Once agent has chosen a macro it must follow actions defined by macro's policy until the termination condition is satisfied/goal is reached.
* The set of available macro-actions often depends on current state of agent.

* **Effect on Exploration**
  * Bias behavior of agent so that he spends most of his time in specific regions of state space.
  * Authors run experiment where actions are uniformly chosen ("random walk") among primitives and macros
  * Agent spends most of time in area where macros lead him to (obvious somewhat)

* **Effect on Propagation of Action Values**
  * Macro action values affect rate of action-value backup
  * Q-Learning: values propagate backwards one step at a time
  * Macro-Q: value info can propagate over several time steps
  * When macro takes agent to a good state, the corresponding value is updated immediately with useful info, despite fact that original state is several primitive actions away from good state
  * Again random walk experiment: value flows further back in state space - mix of macro/Q

* Macros only make learning slower if they alone cant bring the agent to the goal location
  * This is always fulfilled when working with straight-line grammars!
