# Title: Capacity and Trainability in Recurrent Neural Networks

# Author: Collins et al (2017) (Google Brain)

#### General Content:
The authors study the differences in capacity/expressiveness (ability to store info about task in parameters + store info about input history in units). Show that all nets (if trained carefully) have same per-task/per-unit capacity bounds. Furthermore, the nets can approx store one real number per hidden unit & task info that is linear in the number of parameters (approx 5 per).

* Main comparison differences driven by trainability and not capacity! I.e. vanilla RNNs harder to train but slightly higher capacity

#### Key take-away for own work:

#### Keypoints:

* Gated models are easier to train but not necessarily more expressive. Here: Evidence that gated models are dominant because of trainability and not capacity related issues.

* Different bottlenecks:
    * Memory capacity: how much of task/input vector can be stored in units
    * How many Computational primitives can be performed. Despite fact that gated architectures are outfitted with multiplicative primative between hiddens, while vanilla RNN not, found no evidence of computational bottleneck. Use per-param capacity.

* Two new architecture designs:
    1. Update Gate RNN: Minimally gated RNN with only coupled gate between recurrent hidden state and update to hidden state. Inspired by large impact of removing forget gate from the LSTM
    2. Intersection RNN: Coupled gates to gate both recurrent and depth dimensions (coupled depth gate)

* Experiments: BO Hyperparam/GP Bandit Spearmint model
    - fixed number of parameters across comparisons
    - Result: capacity of RNNs to remember input history is not a practical limiting factor on their performance.
    - Memorization task: Draw fixed set of random inputs and labels and train RNN to map them via cross-entropy error - but return mutual info. This way treat number of in-out mappings as hyperparmeter! From this compute bits per params - measure of how much RNN learned about the task/stored info about the mapping. Divide mutual info by the number of parameters to standardize - 5 bits for more stable larger architectures
    - Also find that per-param task capacity increases as a function of the number of unrollings (diminishing returns though)
    - Find that gated models have slightly reduced capacity and that relus reduce capacity as well.
    - Every RNN can reconstruct random input at some time in future iff number of hiddens per layer is greater than the input dim
    - Parallel paranthesis task/addition of integers - Hard tasks = problem of trainability became apparent!

* Inshights/Hacks for training RNNs:
    - Initial conditions = learned bias. Well-known to init gates of LSTM/GRU with large bias to induce better gradient flow
    - Fundamental 1-Layer MLP result: N^2 params are able to store at least 2bits of info per parameter - Can implement mapping from 2N, N-dim input vectors to arbitrary N-dim binary output vectors subject to restriction that input vectors are in general position

* Implications:
    - Train vs inference budget: Use RNN if many train resources but few inference. Otherwise use gated model
    - GRUs are most "learnable"

#### Questions:
