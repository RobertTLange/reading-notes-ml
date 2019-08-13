# Title: Population based Training of Neural Networks

# Author: Jaderberg et al (2017) (DeepMind)

#### General Content:
Authors introduce a meta-optimization algorithm (PBT) that jointly learns the parameters of a NN as well as an effective hyperparameter schedule. It is an async algorithm that uses a ficed computational budget. It learns a **schedule** of hyperparameters and they test PBT on A3C, UNREAL, GANs and Transformers.

#### Key take-away for own work:
PBT performs both hyperparam opt as well as model selection at the same time! Very important.

#### Keypoints:

* Motivation of learning a hyperparam schedule: Often times in RL learning problem is non-stationary in itself (e.g. depends on current policy that explores different parts of the state space). THEREFORE: ideal hyperparams are themselves non-stationary!

* PBT - Wall-clock run time is not greater than a single optimisation run! Does not require sequential training as in BO and thereby uses fewer computational resources.

* Main benefit: Sharing information about different learning dynamics across a population of concurrently running optimisation processes. Allows for **online adaptation** of hyperparams between members of the population based on their performance!

* Model selection element of "warm starts" - allows for intermediate good models to receive more computational resources - define basis of further search/optimisation

* Improvements result from:
    1. Automatic selection of hyperparams - explore & exploit
    2. Online model selection to max computation spent on promising models
    3. Ability for online adaptation to accomodate potentially nonstationary training regimes

* Problem BO: Sequential nature - inherently slow!
* Problem Hyperband: Problem of hyperparam selection as many-arm bandit - cant practically be executed within a single training optimisation process!

* PBT:
    * Starts like parallel search - randomly samples hyperparams and weight inits
    * If model in pop in underperforming - will exploit the rest of the better performing population by replacing itself with better performers (both hyperparams + weights)
    * It will also explore new hyperparams by modifying the better models hyperparams before continuing training
    * Idea: Bootstrap the evaluation of new hyperparams furing training on partially trained models. This eliminates the need for sequential optimisation processes

* Comparison to traditional genetic algorithms: Instead of evolving the params of the model - train them partially with SGD. Mix learning with evolution!

* Formalism:
    * `Optimise` consists of many `step` evaluations composed with different hyperparams for each `step`
    * `exploit`: decides whether worker should abandon current solution and focus on more promising one by spawning another run from the population that performs better. Copy weights and hyperparams
    * `explore`: Proposed new hyperparams to better explore solution space. Create by perturbing/resampling hyperparams from previous worker.
    * `ready`: Mark worker to be ready for explore/exploit after sufficient number of steps in between.
    * Overall: Two timescale algorithm that trains locally with SGD and globally selects models and performs genetic hyperparam mutation

* Globally available: current performance info, weights, hyperparams across population! But no syncronisation required!

* DRL experiments:
    * A3c Starcraft II: ready after 10^6, 6x10^6 agent steps
    * Exploit:
        * T-test selection and performance comparison after sampling competitor uniformly at random
        * Truncation selection - rank models and select radnomly from top 20% if current agent is in lower 20%
    * Explore:
        * Perturb by factor 0.8-1.2
        * Resample from original prior distribution on hyperparams
    * Optimise lrate, entropy cost coeff, unroll length for BPTT, intrinsic reward cost

* DRL results:
    * hyperparams focus on best part of sampling range adapted over time
    * Gradually increases number of N-step PG unroll length before BPTT - allows RNN to learn to utilise RNN for memory.
    * Copying of weights - allows the population to quckly propagate agents that got lucky during env exploration - benefits goes to whole population!

* Machine translation: Learns to set layer dependent different dropout rates! + lrate schedule looks very much like the one handtuning obtains!

* GANs: Usually couple gen/discr hyperparam schedule - likely suboptimal
    * Update discriminator more frequently than generator!
    * Exploitation via binary tournament strategy: Each member of population selects another member of population and copies params if the other members score is better - for both discriminator and generator
    * Eval with Inception score of weaker CIFAR10 classifier and not from Imagenet

* Number of workers - need sufficiently large population size: 10 leeds to high variance in PBT and poor performance - since PBT os greedy and can get stuck in local optima
    * Large enough population is rquored to maintain diversity in exploration & population

* Truncation selection on 20% range worked best in terms of exploitation

* Played with transferring only weights or only hyperparams and show that combination of both is required!

* Also if continuing training with final hyperparams of PBT this helps signifacntly!

* In general PBT rule seems to be more aggressive

#### Questions:

* How to choose the number of sgd iterations between steps? Essentially how to define ready?
