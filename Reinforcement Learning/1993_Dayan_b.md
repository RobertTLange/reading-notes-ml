# Title: Improving Generalisation for Temporal Difference Learning: The Successor Representation
# Author: Peter Dayan (1993b)

#### General Content: Good representation for state resembles representations for its successors - only small Euclidean distance away. Succesor representation (SR) = expected number of occupancies of state under given policy. Essentially replaces single temporal learning problem (prediction of future reinforcements) by a set of learning problems (prediction of future occupancy of all states. Thereby it factors out temporal component of task/Markov transition matrix. Do not have to solve full problem but can use SR predictions to augment standard (punctuate) representation. Also: Combine with previous reward free exploration phase.


#### Keypoints: 

* Generalizing representations:
	* Static: Similarity in terms of distance in space
	* Dynamic: Similarity of future course of behavior of dynamical systems

$Q^\pi(s,a) = \mathbb{E}[\sum_{t=0}^\infty \gamma^t R(s_t) | s_0=s, a_0=a] = \sum_{s' \in S} M(s,s',a) R(s')$

where $M(s, s', a) = \mathbb{E}[\sum \gamma^t \mathbb{1}[s_t = s'] |s_0=s, a_0=a]$ is the SR

which is untractable due to indicator expectation. Solve by TD learning problem for each state!

* Make fairly loose assumption of linear representation of rewards (still allows for deep nets as state representations): $R(s_t)=\phi_{s_t}$

$Q^\pi (s,a) = \mathbb{E}[\sum_{t=0}^\infty \gamma^t \phi_{s_t} | s_0=s, a_0=a] \cdot w = M^\pi(s,a) \cdot w$

* Have to learn both M, w: M - represents policy-dependent expected features and w - represents goals


#### Questions: 

* Read Kulkarni et al (2017) generalisation to DL!
* Relationship to HRL!!! - good representation for temporal tasks
* How does SR work in stochastic domains/adapt - Dayan hints that it is bad!
* Think of SR as hidden representations