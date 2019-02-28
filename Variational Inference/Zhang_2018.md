# Title: Advances in Variational Inference

# Author: Zhang et al. (2018)

#### General Content: Provides a review of the developments in VI during the last 10 years. Review - Scalability - Beyond Conjugacy - Beyond KL/Mean Field - Amortized/Inference Networks - VAEs. Very well written and right level of abstraction.


#### Keypoints:

* MCMC/Sampling unbiased - slow; VI/Optimization fast - oversimplified posterior approx
    * Based on generative process p(x,z) - latents can be shared among multiple data points, and data points can have multiple latents.
    * Idea: Approx complicated posterior by simpler variational distribution parametrized by set of variational params. Tuning via min of KL divergence. Circumvents knowledge of posterior normalization. Every latent has its own variational param
    * Expectation propagation <-> the reverse KL of VI - local moment matching
    * Usually var distribution is underparametrized - not flexible enough: Trade-off between expressive var distr and tractable approximation
    * Derive objective ELBO via log model decomposition and jensen's ineq - conservative estimate of marginal = model fit -> comparison
    * Traditional VI: analytical solve expectation over var distribution - restriction to class of conjugate exp models
    * Mean Field VI: Full factorization of var distribution across the latent variables
        * Allows for separation of expectation into inner and outer which allows for form of coordinate descent updates - relates to var message passing and Markov blankets

* Scalable VI: Use SGD to scale to large data
    * Closed-form gradient expression might be too comp exp to eval for whole dataset. Instead subsample data batch and perform optimization with approx gradient
    * Natural gradients: Simplification for models in conditionally conjugate exponential family - take geometry into account. Pre-multiply gradient with inverse Fisher info matrix
    * Split into global and local params: Global params want larger batches while local params want smaller!
    * Smaller variance in grads allows for larger learning rate and faster convergence
        * Optimally adapt batchsize or learning rate and fix the other.
            * Idea of RMSprop/others: adapt learning rate inversely proportional to gradient noise
            * Choose batchsize proportionately to value of objective relative to its optimum
    * Variance Reduction:
        * Control variates: Stochastic term that when added to grad does not change exp but reduces the variance - needs to be correlated with grad.    
            * SVRG: Use prev taken grad over all datapoints and exploit fact that gradients along optimization path are correlated - Requires full pass after discrete set of iterations
        * Importance sampling: Non-uniform sampling of batches with smaller grad variance
        * Rao-Blackwellization: Reduce variance by conditioning on some valid statistic
    * Collapsed inference: Analytically integrate out certain model params. Tightens lower bound wrt specific params
    * Sparse inference: Additional low-rank approx. T inducing points - pseudo-inputs that represent original data but yield sparser representation

* Generic/Blackbox VI
    * BBVI - Away from conjugate exponential family
    * Laplac approx: Gaussian approx at mode of posterior (=mean). Fit an inverse Hessian for a cov matrix appox. Bernstein von Mises theorem: approx becomes exact in the limit.
        * Problem: Purely local and depending on curvature
    * REINFORCE like gradients: Only generative process needed - represent gradient as expectation and approximate via MC samples. No analytical eval of ELBO. Via log ratio trick. Again techniques for var reduction are applicable
    * Reparametrization trick: Represent random var as det function of noise distribution. Construct stochastic estimator by pulling gradient into expectation. Key to VAEs. Gumbel-Max trick: replace argmax by softmax to make things work for categorical distribution

* Corrections/Different Divergences
    * Thouless-Anderson-Palmer: Pertubative correction to var free energy from stat physics
    * All versions of Stein's discrepancy: f-div -> alpha-dic -> KL div
    * Structured VI: Not fully factorized - more expressive but higher comp cost
    * Hierarchical VI: E.g. Var GP - applies GP prior on variational params and then allows to sample

* Amortized Inference
    * Idea: Approx the latent var as a fct of the data that optimally predicts it. Utilize idea of parameter sharing to reduce num of var params. Amortized: Utilize past computations for future comps

* Variational Autoencoders
    * Generative + Recognition network with amortized mean field var distr - objective is KL divergence
    * Exploits reparam trick - reduces grad var? How?
    * Normalizing flows = Transform simple approx posterior into more expressive distribution by successive trafos
    * Dying Units Problem: If decoder is too strong - inference fails to learn informative posterior - some dimensions of latent z will simply be ignored.

#### Questions:

* Look into hybrid sampling/optimization approaches
