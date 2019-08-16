# Title: Neural Tangent Kernel: Convergence and Generalization in Neural Networks

# Author: Jacot et al. (2018) (EPFL)

#### General Content:
Authors connect ANNs to Kernel methods during training and show that the evolution is also described as a kernel - the neural tangent kernel (not only at Initialization)!
* kernel allows to characterize the generalization behavior of the net and allows to study training in the function space instead of param space.
* they show how convergence is related to the positive-definiteness of the kernel.
* they also show that for the regression objective the network function follows a linear differential equation and that training is fastest along largest principal component - relates to early stopping!


#### Key take-away for own work:

#### Keypoints:

* Theoretical results showing that for wide enough nets there are few bad local minima. Corresponds to kernel method properties of good generalization

* Known result - Radford Neal: Infinite hidden layer width - network at Initialization converges to Gaussian distribution - Here: not init but during training

* Show that dynamics of the function characterized by NN follows kernel GD wrt to limiting NTK - only depends upon depth, choice of non-lin and init variance

* Kernel gradient:
    - Cost function may be convex but composition with NN becomes highly non-convex
    - During training the net function follows descent along kernel gradient wrt NTK
    - Multi-dim Kernel = defines bilinear map on function space
    - Dual of function space = linear forms - same linear form means equal on training data
    - Cost functional at certain function can be viewed as element in dual space. Can write down gradient with respect to function
    - Kernel gradient = gradient of cost function wrt to kernel given function - defined by dual to function space map with specific dual elements
    - Main benefit: It is defined outside the dataset
    - During descent algorithm the cost evolves according to linear differential equation
    - Convergence is guaranteed as long as K is positive definite
    - Can be approximated by random sampled functions from function space
    - Show that GD on composition of cost and function is equivalent to Kernel GD with tangent kernel in function space

* Neural Tangent kernel:
    - Difference to previous case: kernel depends on parameters that vary during Training
    - show that NTK becomes deterministic at init and stays constant during training for infinite-width case
    - Least squares result: Diagonalization with exponential rate eigenvalues
    - Motivation for early stopping - convergence is faster along large eigenvalue eigenspaces. Lower eigenvalues are typically ones associated with noise

* Small experiments:
    - wider nets show less variance in the kernel and they are smoother
    - exponential rate of convergence - faster for smaller nets - connection to inflation in kernel - BUT: need to take into account possibility of larger learning rate 

#### Questions:
