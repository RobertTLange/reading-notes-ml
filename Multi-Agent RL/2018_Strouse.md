# Title: Learning to Share and Hide Intentions using Info Regularization

# Author: Strouse et al (2018)

#### General Content: Introduce minimal observer model in form of info-sharing/hiding regularizer which controls incentives to share intentions. 2 versions: goal-state (less observational capabilities required) and goal-action (easier to optimize). Derive Monte Carlo PG estimates and prototype in specific pre-built environments. Info reg breaks symmetries between equally preferred policies (in terms of rewards) towards those which are less/more diffuse.


#### Keypoints:
* Go away from strong observer model as in Machine ToM
* Often times regularizer as entropy of policy - incentivizes exploration

* Information quantities: Measure ease in inferring goal from Alice  from action/states - Sharing: Alice should choose policy with high info
 	* Action: Assumes bob can observe alice's states and actions (easier to optimize)
	* State: Inly state - cost of alice counting goal-dependent state frequencies

* $\beta$ controls tradeoff:
	* sign determines if agent/alice wants to signal or hide info
	* magnitude determines relative preference for rewards and intention hiding/sharing

* Monte Carlo PG update:
	* rewrite as expectation over trajectories - use log derivative
	* specific information discount factor
	* State info case - need to keep track of state goal frequencies

* Experiments:
	* Spatial navigation 5x5 grid with changing goal position
		* sign of beta influences how "complicated"/diffuse the observed policy is - cooperative - very clear difference between policies depending on goal
		* First train Alice and then introduce Bob who is processes Alice trajectories with RNN to form belief of goal - feed into his policy traned end-to-end via REINFORCE
		* Training without info reg - results between cooperation and competitive behavior
	* Key-door-game: Alice can delay informing with special key - does so if she wants to hide info

#### Questions:
* Interesting connection to econ - moral hazard/assymmetric info sharing
	* What could a regularizer correspond to in a simple econ model?

* Come up with mixing between both regularizers - what could others be?

* Importance of designing environments which are suited to validate your approach
