# Title: Universal Value Function Approximators

# Author: Schaul et al (2015)

#### General Content: Authors generalize notion of value fct approx over states and goals $V(s,g;\theta)$. These can be learned in one of two ways: 

1. Using supervised learning and a set of learned values. They factorize the tabular matrix representation into two embedding vectors (one for goals and one for states) assuming a simple dot product activation network. Afterwards, they learn the mapping from state/goal to these vectors.
2. Using RL and a set of value function learners as in the Horde setup (Sutton et al, 2011). In this case the UVFA is directly learned from rewards.

They show that these set-ups lead to good generalization to unseen goals.


#### Keypoints: 

* General value function: $V_g(s)$ - value of any state s in achieving goal g - pseudo-reward
* Horde: Discrete set of value functions (demons)- all learned simultaneously from single stream of experience - bootstrapping from off-policy
* Collection of value functions = Predictive representation of state <-> predicted values = feature vector
* Goal space contains often as much structure if not even more than state space
* UVFA = Infinite Horde of demons - summarize whole class of predictions in single object
	* Takes into account structure between goals:
		1. Similarity encoded in goal representations g
		2. Structure in induced value functions discovered bottom-up
	* Complexity does not depend on number of demons but on domain complexity
* Learning of UVFA. View data as sparse table of values (rows = states, cols = goals)
	1. Low-rank factorization: State embeddings $\phi(s)$, goal embeddings $\mu(g)$
	2. Learn non-linear mappings: $ s \to \phi(s)$ and $g \to \mu(g)$ by minimizing MSE.
* RL Learning of UVFA: 2 Algos - Continual learning: set of goals under consideration expands over time
	* Use finite Horde of $V_g(s)$ to fill table
	* Bootstrap directly from value of UVFA at successor state - end-to-end training
	
* Low-rank approximation can usually already capture much if the structure of UVF
* Extrapolation: If states are represemted with same features as goals and states in new parts of space that have already been encountered, then partially symmetric architecture allows for knowledge transfer from $\phi$ to $\mu$.

* RL learning from rewards:
	* only rewards/obs data available and no knowledge about ground-truth target values
	* Horde to provide targets of UVFA - each demon in Horde approximates value fct for single specific goal - learn off-policy in parallel from shared stream of interactions with env - seed data matric with values - learn embeddings afterwards
	* Problem: data depends on way in which behavior policy explores env.
	* Two performance variables:
		1. Amount of experience Horde has accumulated - quality of targets used in factorization
		2. Amount of computation used to build UVFA from data - training of embeddings  	

#### Questions: 

* Very interesting connection between RL and supervised learning with the same premise: Generalization and fitting the underlying value data-generating process.
* What env-structure does the notion of parameter sharing assume?