# Title: Learning to Communicate with Deep MARL

# Author: Foerster et al (2016)

#### General Content: Introduce Multi-agent RL architectures able to learn communication (cooperative) via centralised learning and decentralized execution. Two architectures - RIAL (parameter sharing communication), DIAL (sharing of gradient info across agents). Differentiable communication + DRL


#### Keypoints:

* General setup
    * All agents max same discounted reward
    * Agents emit two forms of actions: communication messages (discrete limited-bandwidth channel) and env actions
    * Indep DQN - Agent indep and simultaneously learn own Q-function - convergence problems
    * DRQN - No longer fully observable - additional hidden/internal state and observation state

* RIAL
    * 2 Versions:
        * Independent DQN + DRQN - Each agent learns individual network (other agents part of env)
        * Parameter sharing + DRQN - One shared network different hidden state/obs conditioning per agent
    * End-to-end trainable within agent
    * Details:
        * Disabled ER - account for non-stationarity occuring with multiple agents learning simultaneously
        * Split actions env/comm into two different streams - avoid multiplicative dim - two separate value functions are learned and evaluated at every time step
        * Param sharing: Also feed in agents index as part of input vector = conditioning

* DIAL
    * End-to-end trainable across agents -
    * Centralized training: real-valued gradients are passed between agents (while training continuous!)
    * Communication actions as bottleneck connections between agents
    * Decentralized execution: discretization of messages mapped to discrete communication actions
    * Details:
        * not only param sharing but also gradient pushing through communication channel since messages act as any other form of net activation
        * use discretize/regularize units with different functional forms while training/execution
        * One single Q function whose grad is based on DQN loss

* Prototyping in switch riddle/colour-digit MNIST with max 4 agents - scalability?
    * Show how elaborate 1-bit message passing protocols emerge
    * Importance of noisy communication channels - adding boosts performance - relation to discrete language structure?

#### Questions:

* Importance of language in cooperative behavior - regularization through discrete structures

* Communication passing - analogy with federated learning and homomorphic encryption
    * Extension to distributed learning domain in the long-term!

* Translation into policy gradient domain and swarm env domain
    * How can this scale to multiple agents?
