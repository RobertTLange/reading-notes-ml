# Title: Automatic Differentiation in Machine Learning: a Survey

# Author: Baydin et al (2018)

#### General Content:
Provide a somewhat high-level review on automatic differentiation (forward & backward mode), its applications and implementation considerations.

#### Key take-away for own work:
AD is not equal to backprop. But the gradient problem in Deep Learning naturally leads itself to backward mode ad since we have many inputs and few outputs! Ultimately the ratio of input dim to output dim determines which method is more computationally efficient.

#### Keypoints:

* AD = efficient and accurate eval of derivatives of numeric functions expressed as computer programs

* Different types of derivative computations:
    - Manual: time consuming, error prone
    - Numerical (finite differences): round-off and truncation errors, scales poorly
    - Symbolic (computer algebra - expression manipulation): complex expressions - "expression" swell, requires models to be defined as closed-form expressions - limits expressability and control flow
    - Algorithmic/AD: Non-standard interpretation of computer program. Replaces domain of vars to incorporate derivate values and redefining semantics of operators to propagate derivatives per chain rule of differential calculus

* AD = Family of techniques that compute derivatives through accumulation of values during code exec to generate numerical derivative evaluations rather than derivative expressions. Evaluation at machine precision
    * Application to regular code - allows for branching, loops and recursion
    * Backprop = gradient obtained by backward propagation (via chain rule) of sensitivity of objective value at the output. Equivalent to transforming the net evaluation function composed with the objective function under reverse mode AD
    * Important: Provides numerical values of the derivative and not derivative expressions. Does so by using symbolic rules of differentiation

* Numerical Differentiation: finite diff approx of deriv using values of original function at some sample point based on limit definition of derivative
    * Advantage: easy to eval, Disadvantage: Need as many evals as there are input dims
    * Ill conditioned and unstable due to truncation and round-off errors (limited precision)
    * Center difference approximation: More numerically stable! But needs also more function evals

* Symbolic Differentiation: Automatic manipulation of expressions for obtaining derivative expressions - apply trafos representing rules of differentiation - Mathematica, etc.
    * Problem of nested duplications that can lead to exponentially large symbolic expressions - taking long to evaluate! = expression swell
    * Try to simplify by storing only values of intermediate sub-expressions in memory. Interleave differentiation and simplification as much as possible. Forms basis of AD: Apply symbolic differentiation at elementary operation level and keep intermediate numerical results linked to evaluation of the main function

* General idea: Augmentation of standard computation with calculation of various derivatives. All numerical computations are ultimately compositions of finite set of elementary operations for which derivatives are known. Combining the derivatives of constituent operations through chain rule gives derivative of overall composition

* Important: AD is blind with respect to any operation including control flow statements which do not direclty alter the numeric values

* Forward accumulation mode: Applying the chain rule to each elementary operation in the forward primal trace generates the corresponding tangent derivative trace.
    * Evaluating the primals in lockstep with their corresponding tangents gives the required final derivative
    * Full Jacobian requires n evaluations! Set x dot to vector in order to compute Jacobian vector product
    * Mathematically = forward mode AD is equal to evaluating a function using dual numbers - defined as truncated Taylor series. Can extract derivative from the coefficient in front of the dual number - Simultaneous computation!

* Reverse accumulation mode: Propagates derivatives backward from a given output
    * Complement every intermediate variable with an adjoint - represents the sensitivity of considered output with respect to changes in intermediate variable
    * Two phase procedure - run function forward and populate/store intermediate variables
    * While doing so record the dependencies in the computational graph through a bookeeping procedure
    * 2nd phase: calculate derivatives by propagating adjoints in reverse from output to input
    * Advantage: Significantly less costly to evaluate than forward mode if number of inputs is large. Comes at cost of increased storage requirements in proportion to number of operations in the evaluated function

* Hessian computation tricks:
    * quasi-Newton = numerical approx using first-order updates from gradient evals
    * L-BFGS = limited-memory Broyden-Fletcher-Goldfarb-Shannon
    * Often dont need full Hessian but a vector product - reverse-on-forward configuration of AD. Run first forward and then backward on result

* Dynamic computational graph = define-by-run: execution dynamically constructs graph on the fly that can freely change over iterations

#### Questions:
