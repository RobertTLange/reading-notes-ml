# Title: Stabilizing the Lottery Ticket Hypothesis

# Author: Frankle et al (2019) (MIT)

#### General Content:
Iterative Magnitude Pruning does not work on deep networks when resetting remaining weights to their initalization values at k=0/precise initialization. Here the authors show that if we do not reset to 0 but to weights trained with full net at an "early" stage of training we can recover the Lottery Ticket hypothesis! They achieve to scale to ImageNet with this approach. Furthermore, they introduce two notions of stability: Pruning and Data Order. As subnetworks become more stable to gradient noise, they train to params closer to those of full network & and do so robustly.

#### Keypoints:


* LTH: Dense NNs contain sparse subnets capable of training to commensurate accuracy at similar speed. Use IMP do identify such networks ex post.

* Fails on deeper networks and therefore cant scale to Imagenet. Original work tried to overcome this limitation by changing networks learning schedule - warm up! Here: Argue that this is due to fact of initializing back to 0!

* Propose Rewinding instead: Demonstrate that there are subnets at early points in training that are 50-90% smaller and can complete training process to match original nets accuracy

* Where original IMP without rewinding cannot find winning ticket, accuracy benefits of delay in pruning accrue rapidly (only few iterations required!)
    * Resnet 50:
    * Inception:
    * SqueezeNet:

* Stability: Why is this the case? Stability = distance between two trained copies of same subnet subjected to different noise
    * Noise due to pruning - Comparing trained weights of full net and subnet - Full vs Masked on same data ordering
    * Noise due to data ordering - Comparing trained weights of two subnets with different data orders - Masked Order 1 vs Masked Order 2
    * In case where IMP fails to find tickets when resetting to 0 - both stability measures increase rapidly as pruning in delayed - mirroring rise in accuracy
    * Captures extent to which subnetwork arrives at same destination as original net in optimization landscape

* New hypothesis:
    * Improved pruning stability = Subnets come closer to original optimum and thereby accuracy.
    * Improved ordering stability = Subnetwork can do so consistently in spite of noise intrinsic to SGD.

* LTH with Rewinding: A dense randomly init NN that trains to accuracy a* in T* has a subnetwork with weights W_t at iter t so that there exists an iter k and fixed pruning mask such that subnet m dot W_k trains to accuracy a<a* in less than T-k iters!

* Experiments:
    * Random pruning comparison: Random with same layer-wise proportions - are less stable in both terms compared to winning tickets
    * Starting point: IMP finds winning tickets for Lenet but not Resnet/VGG without warming up of learning rate
        * Suggests: High lrate is not detrimental at later stages in training - only init. Hypothesis: For less overparam. subnets optimization is brittle to noise in early stages of training. Networks become more stable later on!
    *  Rewinding to 100 its VGG-19 and 500 its for Resnet-18 works (afterwards benefits saturate in stability and accuracy)! - Benefits of stability decrease with k as random nets become more stable later on!
    * Problem of rewinding to late stages - does not allow enough further training!


* Scaling to ImageNet:
    * As rewinding iteration increases gap in stability emerges - accuracy improves alongside stability - reaches original nets accuracy at epoch 4/90 Resnet-50, 6/171 Inception, 10/150 for Squeezenet.
    * As IMP subnets become more stable - nets reach higher accuracy. LTH still applies but have to use weights later in training.

#### Questions:
* Where to go?
    - Only vision, lots of compute, to which point/iter to rewind?, unstructured pruning procedure problem.
* Somehow exploit knowledge about stability in the pruning procedure!?
