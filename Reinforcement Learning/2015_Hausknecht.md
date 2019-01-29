# Title: Deep Recurrent Q-Learning for POMDPs

# Author: Hausknecht and Stone (2015)

#### General Content: Add recurrence to standard DQN architecture by replacing fully connected after convolutions by LSTM layer. Layer takes previous hidden states as input. Afterwards, another fully connected layers maps to action values. Provides alternative to stacking frames to induce Markovity. Show that recurrent is more robust to occlusion/noise than DQN.


#### Keypoints:

* Most ATARI games are not directly Markovian - example pong and velocity of the ball. DQN combats this by feeding multiple frames at a time. Mnih et al show that 4 frames suffice to ensure Markovity.
* At training time: All parameters are learned via backprop through time. Two different updating schemes:
    1. Bootstrapped Sequential Updates: Sample complete episodes. Instantiate hidden state to zeros. Begin at start of episode and process complete sequence.
    2. Bootstrapped Random Updates: Sample random point of episode and process block starting from there and lasting for "unroll iterations timesteps" (here chosen to be 10) - zero hidden state at beginning of update.
* Test approach by altering Atari games to flickr with prob 0.5 - need to infer velocity etc.
    * DRQN takes one frame at a time, while DQN takes 10 - recurrent layer needs to compensate for both flickering state as well as conv velocity detection.
* Train on MDP (non-flickering) data and test generalization on noisy data - DRQN outperforms significantly! - Hypothesis: Recurrent controller are robust to missing info even when trained on fully obs info

#### Questions:

* Authors state that two update schemes perform similiar! and use random strategy.
* Scalability? Is it faster just to feed more channels/frames to conv net or to unroll the DRQN for a timestep for each frame?
