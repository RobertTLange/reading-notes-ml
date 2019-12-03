# Reading Notes 2017/2018
# Author: Robert T. Lange

This repository contains simple reading notes, thoughts, questions and summaries of the papers/book chapters, which I ([Robert T. Lange](www.rob-lange.com)) have read in the second half of 2017 and 2018. This includes the summer break, where I attended a Free-Energy Principle summer school organised by Prof. Blankenburg and Prof. Ostwald (both BCCN and FU Berlin), the DS^3 Summer School as well as the European Summer School in Information Retrieval (ESSIR) and the time of my Computing (ML) Master's at Imperial College London.

The documents are grouped by overarching topic. First of all I hope that this way I am able to structure my knowledge gains and have a quick read to remind myself of keypoints. Second, I hope that you are able to follow my current interests and research progress.

**Notes:**

1. If there is a tick in the box, there exists a summary markdown file in the subdirectory. Otherwise, I have only read the document. Furthermore, I list below the chapters of books, while the markdown file contains the summary for the full (or the parts that I have worked in) book.
2. Most papers focus on Deep RL and Hierarchical RL (due to thesis and general interest).

| Read / Notes  | Title  & Author  | Year  | Category | Conference | Paper  |  Notes |
| ------ |:-------------:|  :-----:| :-----:|  :-----:| :-----:|:-----:|
:fire: #12 - 12/19 | Geier & Ha - Weight Agnostic Neural Networks | 2019 | NAS | NeuRIPS | [Click](https://arxiv.org/abs/1906.04358) | [Click](ReadingGroupTU/2019_Geier.md)
:fire: #11 - 11/19 | Kümmerer et al. - Saliency Benchmarking made easy: Separating models, maps and metrics | 2018 | Saliency | EECV | [Click](http://openaccess.thecvf.com/content_ECCV_2018/html/Matthias_Kummerer_Saliency_Benchmarking_Made_ECCV_2018_paper.html) | [Click](Vision/2018_Kuemmerer.md)
:fire: #10 - 08/19 | Baydin et al. - Automatic Differentiation in Machine Learning: a Survey | 2018 | Autodiff | JMLR | [Click](http://www.jmlr.org/papers/volume18/17-468/17-468.pdf) | [Click](Optimization/2018_Baydin.md)
:fire: #9 - 08/19 | Flennerhag et al. -  Transferring Knowledge across Learning Processes| 2019 | Meta-Learning | ICLR | [Click](https://arxiv.org/abs/1812.01054) | [Click](ReadingGroupTU/2019_Flennerhag_pres.pdf)
:fire: #8 - 08/19 | Jacot et al. - Neural Tangent Kernel: Convergence and Generalization in Neural Networks | 2018 | Theory of DL | NeuRIPS | [Click](https://arxiv.org/abs/1806.07572) | [Click](Theory-of-DL/2018_Jacot.md)
:fire: #7 - 08/19 | Collins et al. - Capacity and Trainability in Recurrent Neural Networks | 2017 | RNNs | ICLR | [Click](https://arxiv.org/abs/1611.09913) | [Click](Theory-of-DL/2017_Collins.md)
:fire: #6 - 08/19 | Li et al. - A Generalized Framework for Population Based Training | 2019 | PBT | ArXiv | [Click](https://arxiv.org/abs/1902.01894) | [Click](Hyperparam-Opt/2019_Li.md)
:fire: #5 - 08/19 | Jaderberg et al. - Population Based Training of Neural Networks | 2017 | PBT | ArXiv | [Click](https://arxiv.org/abs/1711.09846) | [Click](Hyperparam-Opt/2017_Jaderberg.md)
:fire: #4 - 08/19 | Frankle et al. - Stabilizing The Lottery Ticket Hypothesis | 2019 | Initialization | ArXiv | [Click](https://arxiv.org/abs/1903.01611) | [Click](Theory-of-DL/2019b_Frankle.md)
:fire: #3 - 08/19 | Frankle & Carbin - The Lottery Ticket Hypothesis: Finding Sparse, Trainable Neural Networks | 2019 | Initialization | ICLR | [Click](https://arxiv.org/abs/1803.03635) | [Click](Theory-of-DL/2019_Frankle.md)
:fire: #2 - 08/19 | Nayebi et al. - Task-Driven Convolutional Recurrent Models of the Visual System | 2018 | RNNs | NeuRIPS | [Click](https://arxiv.org/pdf/1807.00053.pdf) | [Click](ReadingGroupTU/2018_Nayebi_pres.pdf)
:fire: #1 - 07/19 | Bengio et al. - A Meta-Transfer Objective for Learning to Disentangle Causal Mechanisms | 2019 | Meta | ArXiv | [Click](https://arxiv.org/abs/1901.10912) | [Click](ReadingGroupTU/2019_Bengio_pres.pdf)


**2019-03**

* [x] [Finn et al (2018) - Probabilistic Model-Agnostic Meta-Learning](Meta-Learning/2018_Finn.md)
* [x] [Andrychowicz et al (2016) - Learning to learn by gradient descent by gradient descent](Meta-Learning/2016_Andrychowicz.md)
* [x] [Finn et al (2017) - Model-Agnostic Meta-Learning for Fast Adaptation of Deep Networks](Meta-Learning/2017_Finn.md)


## Multi-Agent RL

**2018-01**

* [x] Das et al (2019) - TarMAC: Targeted Multi-Agent Communication
* [x] Hausknecht and Stone (2015) - Deep Recurrent Q-Learning for POMDPs

**2018-11**

* [x] Strouse et al (2018) - Learning to Share and Hide Intentions using Info Regularization
* [x] Foerster et al (2016) - Learning to Communicate with Deep MARL


## Biologically-Plausible Deep Learning

**2019-02**
* [x] Whittington & Bogacz (2019) - Theories of Error Propagation in the Brain

**2018-12**

* [x] Sacramento et al (2018) - Dendritic cortical microcircuits approximate the backpropagation algorithm
* [x] Bartunov et al (2018) - Assessing the Scalability of Biologically-Motivated Deep Learning Algorithms and Architectures
* [x] Lillicrap et al (2016) - Random synaptic feedback weights support error backpropagation for deep learning


**2018-11**

* [x] Garnelo et al (2018b) - Neural Processes

## Hierarchical Reinforcement Learning

**2018-08**

* [ ] Pastra and Aloimonos (2012) - The minimalist grammar of action
* [ ] Bacon et al (2017) - The Option-Critic Architecture
* [ ] Daniel et al (2016) - Probabilistic inference for determining options in reinforcement learning
* [ ] Smith et al (2018) - An Inference-Based Policy Gradient Method for Learning Options

**2018-07**

* [x] McGovern & Sutton (1998) - Macro-Actions in Reinforcement Learning: An Empiricial Analysis
* [x] McGovern et al (1997) - Roles of Macro-Actions in Accelerating Reinforcement Learning

**2018-06**

* [x] Yao et al (2014) - Universal Option Models
* [x] Levy et al (2018) - Hierarchical Reinforcement Learning with Hindsight
* [x] Bakker and Schmidhuber (2004) - Hierarchical Reinforcement Learning Based on Subgoal Discovery and Subpolicy Specialization
* [x] Mannor et al (2004) - Dynamic Abstraction in Reinforcement Learning via Clustering
* [x] Menache et al (2002) - Q-Cut - Dynamic Discovery of Sub-Goals in Reinforcement Learning
* [x] Stolle and Barto (2002) - Learning Options in Reinforcement Learning
* [x] McGovern and Barto (2001) - Automatic Discovery of Subgoals in Reinforcement Learning using Diverse Density

**2018-05**

* [x]	Frans et al (2018) - Meta Learning Shared Hierarchies
* [x]	Florensa et al (2017) - Stochastic Neural Networks for Hierarchical Reinforcement Learning


## Formal Grammars, Grammatical Inference and Surprisal

**2018-07**

* [x] Siyari et al (2016) - Lexis: An Optimization Framework

**2018-06**

* [ ] Stout et al (2018) - Grammars of action in human behavior and evolution

**2018-05**

* [ ] Hale (2014) - Automaton theories of human sentence comprehension
* [x] Schoenhense & Faisal (2017) - Data-efficient inference of hierarchical structure in sequential data by information-greedy grammar inference
* [x] Hale (2001) - A Probabilistic Earley Parser as a Psycholinguistic Model


## (Deep) Reinforcement Learning

**2018-06**

* [x] Schaul et al (2015) - Universal Value Function Approximators
* [ ] Gershman and Daw (2017) - Reinforcement Learning and Episodic Memory in Humans and Animals: An Integrative Framework
* [x] Rusu et al (2016) - Policy Distillation
* [x] Andrychowicz et al (2018) - Hindsight Experience Replay
* [x] Choshen, Fox, Loewenstein (2018) - DORA - Directed Outreaching Reinforcement Action-Selection

**2018-05**

* [ ] Li (2017) - Deep Reinforcement Learning: An Overview
* [ ] Arulkumaran (2017) - A Brief Survey of Deep Reinforcement Learning
* [x] Dayan (1993b) - Improving Generalisation for TemporalDifference Learning: The Successor Representation

**2017-08**

* [ ] Barto & Sutton (2016 - draft) - Ch. 1: The Reinforcement Learning Problem


## Free-Energy Principle

**2017-07**

* [x] Friston (2010) - The free-energy principle: a unified brain theory?
* [ ] Limanowski, Blankenburg (2013) - Minimal self-models and the free energy principle

**2017-08**

* [ ] Ostwald (2015) - The Free Energy Principle for Perception: An Introduction
* [ ] Bogacz (2017) - A tutorial on the free-energy framework for modelling perception and learning


## Variational Inference

**2019-02**

* [x] Zhang et al. (2018) - Advances in Variational Inference

**2017-07**

* [x] Ostwald et al. (2014) - A tutorial on variational Bayes for latent linear stochastic time-series models



## Deep Learning (Application + Theory)

**2019-06**

* [ ] Morcos et al (2018) - Insights on representational similarity in neural networks with canonical correlation

**2019-03**

* [x] Spoerer et al (2017) - Recurrent Convolutional NNs: A Better Model of Biological Object Recognition

**2017-07**

* [ ] Goodfellow et al. (2016) - Ch. 6: Deep Feedforward Networks
* [x] Gal, Ghahramani (2015) - Dropout as a Bayesian Approximation: Insights and Applications

**2017-08**

* [x] Gal & Ghahramani (2016) - On Modern Deep Learning and Variational Inference


## Optimization

**2017-07**

* [x] Ruder (2016) - An overview of gradient descent optimization algorithms



## Bayesian Optimization & Gaussian Processes

**2017-07**

* [ ] Shahriari et al. (2015) - Taking the Human Out of the Loop: A Review of Bayesian Optimization


## Real Intelligence

**2017-08**

* [ ] Jeff Hawkins (2003) - On Intelligence
* [ ] Hassabis (2017) - Neuroscience-Inspired Artificial Intelligence


## Machine Learning Reading Group ICL

**2017-10**

* [x] #1: Daume (2004) - From Zero to Reproducing Kernel Hilbert Spaces in Twelve Pages or Less
* [x] #2: Zhang et al (2017) - Theory of Deep Learning III: Generalization Properties of SGD
* [x] #3: Marco et al (2017) - Virtual vs. Real: Trading Off Simulations and Physical Experiments in Reinforcement Learning with Bayesian Optimization

**2017-11**

* [x] #5: Lee et al (2017) - Deep Neural Networks as Gaussian Processes
