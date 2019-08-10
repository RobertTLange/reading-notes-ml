# Title: The Lottery Ticket Hypothesis: Finding sparse, trainable NNs

# Author: Frankle & Carbin (2019 - Best paper ICLR) (MIT)

#### General Content:
Authors discover that subnetworks resulting from weight-magnitude based pruning have had weight initialization that makes them capable of training more effectively than others. The resulting hypothesis is that full nets contain winning tickets of subnetworks that on their own perform. In their experiments (MNIST/CIFAR10) they show that aggressive pruning (up to 80%) can even help in performance.

#### Keypoints:

* Motivation: Observation that sparse architecture resulting from pruning of full net are hard to train from start/scratch when randomly reinitialized. Previously argued that this might be due to small capacity.

* The LT hypothesis: A randomly-init dense NN contains a subnetwork that is init such that - when trained in isolation - can match the test accuracy of the original net after training for at most the same number of iters - often generalize better and need less training iters

* Key difference to previous pruning ideas: No random re-init but initialized to previous weight values at beginning of training of the full network. In experiments the authors show that when instead random init, the winning tickets no longer match performance of original nets. Structure alone cannot explain a winning tickets success.

* Ticket identification: Train + prune the smallest-magnitude weights. Remaining unpruned connections constitute architecture of winning ticket.
    1. Random init net
    2. Train net for j iters
    3. Prune p% of params by creating a mask
    4. Reset the remaining params to their init values from 1., creating the winning ticket

* Can do this in one-shot or with iterative pruning (use unstructured pruning). Iterate train - prune - reset loop over n rounds each time only pruning p^(1/n)% of weights. Experiments show iterative pruning allows to reduce number of parameters even more!

* Observation: In deeper architectures the winning ticket identification is sensitive to the learning rate - requires warm up with smaller learning rate

* The LT conjecture: SGD seeks out & trains subset of well-init weights. Dense, random-init nets are easier to train than the sparse nets that result from pruning because there are more possible subnetworks from which training can recover a winning ticket.

* Implications:
    1. Design training schemes that search for winners and prune as early as possible
    2. Design better net archs and init schemes with same properties as winning tickets
    3. Improve theoretical understanding - Implications for optimization and initialization

* Experiments on small architecture: MNIST-Lenet (FC)
    * Connections to outputs are pruned at half of the rate of the rest of the net
    * Iterative pruning: 20% per iteration - use iteration at which early-stopping criterion is reached as indicator for how quickly the net is learning
    * At early stopping training acc increases with pruning  - but no better generalization - need to train longer! But gap between training and test accuracy is smaller for winning tickets -> better generalization
    * Random reinit: Winning tickets learn progressively slower
    * Iterative pruning is costly. One-shot finds winning ticket but further improvement with iterating

* Experiments on larger architecture: CIFAR10-VGG/ResNet (Conv)
    * Scaled down VGG versions: As network is pruned it learns faster and test accuracy rises
    * As before: Train accuracy at early-stopping iteration rises with test accuracy
    * Dropout: Intuition of simultaneously training an ensemble of subnetworks - rate 0.5 - still find winning networks when training with dropout - methods appear complimentary
    * Original dropout paper observes that dropout induces sparse activations in final network - possible that dropout-induced sparsity primes net to be pruned!
    * Future direction: dropout techniques that target weightsor learn per-weight dropout probs might make finding of winning tickets easier?!
    * Full VGG-16/Resnet-18 architectures: Continue to find winning tickets but iterative pruning is sensitive to particular learning rate being used.
    * Before: Use form of local uniform pruning with same rate for each layer. Problem in deeper nets since some layers have more params than others. Smaller layers become bottlenecks. Global pruning instead = remove the smallest magnitude weights from all layers
    * For VGG architecture need an increasing learning rate warmup sequence. Same for Resnet

* Importance of init winning ticket: Winning weights move the most! - Highlights connection to optim procedure
* Extremely pruned less severely overparametrized nets only maintain accuracy
* Hypothesis: Structure of winning tickets encodes an inductive bias customized to learning task at hand
* Larger networks might contain simpler representations
* Role of overparametrization during training

#### Questions:

* How many rounds in iterative pruning schedule?
* Similar as distillation can this be extended to Deep RL?
