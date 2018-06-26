# Neural Ordinary Differential Equations
## Overview and Summary
I try to implement the findings in the paper in this repo. Here's a summary of what I think is significant information.

Neural Ordinary Differential Equations introduces an interesting way of specifiying a neural network. Instead of treating the neural network as a sequence of discrete states, the approach parameterizes the derivative of the hidden state using a neural network. This parameterizing of the hidden state provides a continuous depth model provides a bunch of useful properties.

### Useful Properties I Understand
1. Memory Efficiency: The specifications give a constant memory costs wrt to depth
2. Adaptive Computation: Adapt level of error for efficiency, useful for real-time or low-power applications
3. Scalable and Invertible Normalizing Flows: Continuous transformation allows for easier computation of change of variables. The paper derives a new fclass of invertible density models that avoids the bottleneck of normalizing flows, allowing the model to be trained directly by max-likelihood.
4. Scalable and invertible normalizing flows: The continuous transformation makes the change of variables formula easier to compute. This allows the constructuion of a new class of invertible density models that avoids previous bottlenecks. 

5. Continuous Time-series Models: Able to model time-series data that arrive at arbitrary times unlike RNNs.

### What Are Normalizing Flows? I am confused.
I got stumped on this one for a while. My reaction irl the whole time -> ( ・◇・)？ 

If you're a noob like me you would probably get stumped too. Here's what I understand without the math.

Imagine if you were in a conference and someone asked the presenter something really difficult. Making the presenter go ( ・◇・)？ The presenter
doesn't want to cop out and look stupid so he/she tries to answer the question. The presenter then simplifies the question and answers that simpified question instead. Not satisfactory, but it should gets the point across. This is essentially the idea behind Variational Inference. The quantity that describes this is termed as the posterior distribution.

What happens if this explanation seemed to hand wavy or oversimplistic? We need to find a slightly more detailed way of explaning the same thing. How should we tune the complexity of the explanation? This method of tuning the complexity is the idea behind Normalizing Flows. By using these normalizing flows, we can apply a sequence of invertible transformation (we can back and forth and not lose information) to transform that simple posterior distribution (ie. the explanation) into something more complex that captures the idea we want to describe. 

This paper essentially provides a continuous formulation of the normalizing flow concept. While an elegant concept, it can get hard to compute terms, like the change of variables. Using the continuous formulation, the paper offers a method of using the trace of the mapping function, which is more efficient. Check the maths in the paper for a clearer picture.


#### Useful links
1. [Quora explanation by Sam Wang](https://www.quora.com/What-is-variational-inference) I used his analogy
2. [Variational Inference by David  M. Blei](https://www.cs.princeton.edu/courses/archive/fall11/cos597C/lectures/variational-inference-i.pdf)
3. [Variational Inference with Normalizing Flows Paper](https://arxiv.org/abs/1505.05770) 

### Limitations
1. Unstraightforward Minibatching: Though minibatching can still be achieved by concatenating the states of each batch elements together to form an ODE.
2. Uniqueness: A unique solutio only exists if the neural netowrk has finate weights and Lipshitz nonlinearities like tanh or relu.
3. Reversibility: Forward trajectory of the network is invertible in principle, but numerical errors will emerge in forward ODE solver and reverse ODE solver (though this can be reduce at the cost of more computation). Information is lost due to multiple initial value mapping to the final state, this is expected to be a problem if the system dynamics encoded optimization-like, convergent dynamics.


## Link To Arxiv Paper
https://arxiv.org/abs/1806.07366