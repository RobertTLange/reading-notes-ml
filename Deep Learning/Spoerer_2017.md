# Title: Recurrent Convolutional NNs: A Better Model of Biological Object Recognition

# Author: Spoerer et al (2017)

#### General Content: Introduce (?) CNN architecture with lateral as well as recurrent connections. Hypothesize that recurrence is not necessarily used to deal with Gaussian noise but with occlusions. Introduce two new dataset augmentations (debris and jitter). Debris = random crop overlays with task of single digit recognition, Jitter = Multiple digits with task of recognizing all of them. Use deconvolution to deal with recurrent dim inbalance. Train recurrent net over 4 timesteps and learn via BPTT. Performance comparison robustness check with permutation test. Lateral connections only help with strong debris.
    - Extension of original R-CNN work by Liang & Hu (2015) and Liao and Poggio (2016)

#### Keypoints:

* Motivation: Ventral visual pathway with lateral and feedback connections. Feedforward models vary successful - underexploration of recurrence. Visual processing unfolds over time.
    * Fast local recurrent processing =/= attention
    * Occlusion slows down behavioral responses - recurrent processing? = Competitive processing
    * Occlusion - question of border ownership (cells) => require info from outside their classical receptive fields and signals are delayed relative to initial feedforward input - again suggest recurrent processes
    * Hypothesis: Recurrence provides no clear benefit for solely processing noise since linear filter which is learnable in NN can already deal with it! Recurrence useful across a wider range!

* Occlusion Datasets:
    * Debris: Random crops from randomly selected digts add mask and overlay - summing overall features is bad strategy.
    * Jitter: Multiple images sequentially placed in the image - overlap with relative depth order
    * Preprocessing: Pixel-wise normalization (mean/std) for each pixel from stats computed across the entire datasets

* Architecture:
    * 4 different architectures:
        1. B - Pure feedforward
        2. BT - Feedforward + Top-down
        3. BL - Feedforward + Lateral (recurrence)
        4. BLT
    * Define pre-activations for all 4 for each layer, pixel, time point as well as feature map
    * Pass pre-activations through local response normalization and ReLU
    * Need to control for comparable complexity of the models also generalization to case without occlusion: Increase the number of parameters via either number of b-u connections (B-F = better match in terms of params) or large kernel sizes (B-K = more plausible)
    * General architecture: 2 hidden recurrent layers + Readout at every step - problem with top-down connections - dim mismatch need deconvolution/transposed convolution to size up again. Zeiler et al (2011)
    * Unrolled for 4 time steps on full image! - Why 4 timesteps?
    * At each time step feed in the image and make a readout
    * Train via BPTT - Error is propagated throught time for each time point - network trained to converge as soon as possible, rather than final step - As compared to spiking Joram case where network has settling time steps and is only propagated from final loss!
    * Accuracy measured only at final time step - Loss function then defined sum over time steps? Sum over timesteps and final backprop at the end vs backprop for each current loss at t backwards?
    * Deconvolution: Normal conv layer with stride where input and output sides of layer have been switched

* Model comparison:
    * Pairwise McNemar's test (prediction dependence correction), False discovery rate, Benjamini-Hochberg correction
    * Robustness check with permutation test - form of linear regression of test errors on debris/cropping strength

* Experimental results
    * Lateral connections only help with strong debris
    * Support for RNNs also being better in OCR tasks without noise/occlusion
    * Robustness of RNNs - do simple ffw networks overfit? Is this overfitting? More like learning a specific task under quality conditions

#### Questions:

* Extensions to neural data and reaction time distributions
* How much recurrence do we need?
* Why do people in ML dont do more multiple comparison checks to robustify their performance gains?
* Read up on deconvolutions = transposed convolution!
* Recurrence vs larger receptive fields: Similar to DRQN vs frame concatenation discussion.
