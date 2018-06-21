# Neural Ordinary Differential Equations
## Overview and Summary
I try to implement the findings in the paper in this repo. Here's a summary of what I think is significant information.

Neural Ordinary Differential Equations (NODE) introduces an interesting way of specifiying a neural network. Instead of treating the neural network as a sequence of discrete states, the approach parameterizes the derivative of the hidden state using a neural network. This parameterizing of the hidden state provides a continuous depth model provides a bunch of useful properties.

### Useful Properties I Understand
1. Memory Efficiency: The specifications give a constant memory costs wrt to depth
2. Adaptive Computation: Adapt level of error for efficiency, useful for real-time or low-power applications
3. Scalable and Invertible Normalizing Flows: Continuous transformation allows for easier computation of change of variables. The paper derives a new fclass of invertible density models that avoids the bottleneck of normalizing flows, allowing the model to be trained directly by max-likelihood.
4. Continuous Time-series Models: Able to model time-series data that arrive at arbitrary times unlike RNNs.

### Limitations
1. Unstraightforward Minibatching: Though minibatching can still be achieved by concatenating the states of each batch elements together to form an ODE.
2. Uniqueness: A unique solutio only exists if the neural netowrk has finate weights and Lipshitz nonlinearities like tanh or relu.
3. Reversibility: Forward trajectory of the network is invertible in principle, but numerical errors will emerge in forward ODE solver and reverse ODE solver (though this can be reduce at the cost of more computation). Information is lost due to multiple initial value mapping to the final state, this is expected to be a problem if the system dynamics encoded optimization-like, convergent dynamics.


## Link To Arxiv Paper
https://arxiv.org/abs/1806.07366