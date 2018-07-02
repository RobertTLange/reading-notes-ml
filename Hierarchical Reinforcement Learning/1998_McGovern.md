# Title: Macro-Actions in Reinforcement Learning: An Empirical Analysis

# Author: McGovern and Sutton (1998)

#### General Content:

Extend 1997 paper with comparison to eligibility traces. Authors show that Macro-Q converges faster to optimal policy while $Q(\lambda)$ converges faster to optimal action values (accounts for all Q-values and not only relative ordering).

#### Keypoints:

* Eligibility traces and macros both provide mechanism for speeding up value propagation.

* Eligibility traces: Each state-action pair is marked as eligible for backup with  a trace indicating how recently it has been experienced.
  * On each step the values of all state-action pairs are updated in porportion of their E traces at the time.
  * Because many recent state-action pairs have non-zero traces, value info is propagated backwards many steps

* $Q(\lambda)$ disseminates value info at an even more rapid rate at the cost of getting the policy right.
* Authors propose to combine both approaches - when is Q more important than policy?

* "Large scale" experiment with random walk robot - random walk exhibits higher variance in traces when only choosing among primitive actions  

#### Questions:

* Read more on eligibility traces - try to merge!
