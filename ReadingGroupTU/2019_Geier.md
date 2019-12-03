# Title: Weight Agnostic Neural Networks

# Author: Geier & Ha (2019; NeuRIPS)

#### General Content:
WA-NN = NAS + Weight Sharing without SGD afterwards. By not doing SGD a lot of architectural choices are freed (i.e. non-ReLU activations) because no gradients have to flow through the architecture. GD as a search algorithm is replaced by this new architecture search

#### Key take-away for own work:
Residual RL: use simple controller from WANN and then learn a correction network on top

#### Keypoints:

* Fixed weight and variable architecture search - bypass the costly inner loop SGD training via neural architecture search (NAS)
    * replace SGD by sampling from uniform distribution - single weight
    * sampling every weight is sample inefficient

* Motivation via few-shot learning in mammals - search for inductive biases that generalize across tasks

* Algorithmic details - WANN
    - Start with minimal network
    - evaluate the performance of the Network
    - alter/increase complexity via NEAT formalism

* NEAT - insert node, add connection, change activation - for
    - tournament in batches (tournament size) - winner pool and mutation for next round

* Performance objective: Sample weights and average over performance - how weight agnostic is the network

* Complexity Objective: Connection cost technique. Sum of all connections

* Ranking via dominance relation - no adding of objectives
    - 80% both performance & complexity, 20% only performance (also max)

* Testing on 3 envs: CartPoleSwingUp, BipedalWalker, CarRacing
    - increase dimensionality/complexity
    - CarRacing with pretrained VAE for dimensionality reduction
    - Awesome visualizations with GUI to play-around with
    - Performance around 0 weight is strongly diminished

* Evaluation:
    - random weights - sample all weights [-2, 2]
    - random shared weight
    - tuned shared weight
    - tuned weights via population-based REINFORCE

* Population-based REINFORCE:
    - No parameters updated - integrated out!
    - Step taken wrt probability distribution of policy parameters - i.e. normal distribution (mean, variance)
    - MC trajectory - sample parameters and afterwards policy execution is deterministic - apparently this reduces the variance
    - Motivation: landscape defined by WANN maybe not well suited

* MNIST Testing: Think of each weight value as an individual classifier - ensemble - not better than simple CNN

* Think of WANN as a form of pretraining/search and then continue training afterwards

#### Questions:

* Relationship to Lottery ticket networks: Weights change very much!
* How much would we have to put in to get something like a convolution out of this?
