# ANN - Artificial Neural Network

Geoffrey Hinton is the grandfather of the Artificial Neural Networks.

## The Neuron

---
Input Signal(s) $x_i$-> weights(synapses) $w_i$-> **NEURON** -> Output Signal $y$

The **input signals** can come from the `input layer of neurons` which in real life would be the senses. The **input signals** are actually some `input values`, numerical values. The neuron has an `output value` also known as `dependant variable` which will be passed further on the chain of neural network layers.

The `input values` are `independent variables` from a **single observation**. The values should be standardized and normalized.

The `output value` can be:

- continuous - a numerical value
- binary - true/false
- Categorical - there will be a set of output values - representing the categories

`weights` are the values associated to the neuron synapses. By learning a neural network it means **adjusting** the `weights` of neurons.

In the `neuron` it is calculated the `weighted sum` of all the inputs that is getting:
$$\sum_{n=1}^{m}w_ix_i$$
and the it applies an `activation function`:
$$\phi(\sum_{n=1}^{m}w_ix_i)$$

## The Activation Function

---
There are a lot of types of activation functions, but there are 4 types which are the predominant ones:

- The `threshold function` - yes/no function:

$$
\phi(x) = \left\{
  \begin{array}{ll}
    1 \text{ if } x \ge 0 \\
    0 \text{ if } x \lt 0
  \end{array}
\right.
$$

- the `sigmoid function` - continuos function which yields results in the `(0,1)` interval.
  Used in the output layer when you try to predict probabilities.

$$ \phi(x) = \frac{1}{1+e^{-x}} $$

- `rectifier function` - the most popular function in the neural networks:

$$ \phi(x) = max(x,0) $$

- `hyperbolic tangent (tanh)` function, similar with the sigmoid function but it yields results in the interval `(-1,1)`.

$$ \phi(x) = \frac{1-e^{-2x}}{1+e^{-2x}}$$

### Example 1

If the `dependent variable` should be `0 or 1` then the `threshold function` can be used because you get exactly `0` or `1` as output:

$$ \hat{y} = \phi(\sum_{n=1}^{m}w_ix_i) $$

But it could be used also the `sigmoid function` which will yield the **probability** of the output being `1`.
$$ P(y=1) = \phi(\sum_{n=1}^{m}w_ix_i) $$

### Example 2

If there is a network which has:

- Input Layer
- Hidden Layer
- Output Layer

In the **hidden layer** is applied the `rectifier function` as activation function and in the **output layer** is applied the `sigmoid function`.

## How does NNs work?

---

Since all the input layer neurons are connected to all the neurons from the hidden layer, the neurons from the hidden layer might pick up only one independent variable or a group of them or all of them depending on the weight $w$ associated with the synapse which is adjusted during the training/learning process.

This can be thought as each neuron from the hidden layer focuses on some traits of the observation and tries to emphasize in the result the importance of the combination of that particular trait.

## How do NNs learn?

---

There are two different approaches to obtain a result using a computer program:

- `hardcoding` the algorithm which goes step by step through the data and takes decisions on how to modify the data to obtain the result.

- `create a facility` for the program to understand what it needs to understand what should do by its own.

**Single Layer FeedForward Neural Network** - **Perceptron**

- input layer with $m$ `independent variables`
- **NO** hidden layers
- one neuron output layer which calculates the `Output Value`: $\hat{y}$.

$y$ - is the actual value

$\hat{y}$ - is the ANN output value

`Cost function` is the function which calculates the difference between the `actual value` and the `output value`. The most commonly used one is:
$$ C=\frac{1}{2}(\hat{y} - y)^2 $$

The `Cost function` tells what is the error between the `actual value` and the `output value`. Our goal is to **minimize** the `cost function`.

Once the `difference` is calculated, is feed back in the neural network and the `weights` are being updated.

**1 Epoch** is called the process of training a Neural Network with `one data set` `once`.

For instance there are 10 `single observations`:

- step 1. For each observation will be calculated: $\hat{y}$.
- step 2. When the feeding is done and $\hat{y}$ is calculated for each then the 1`cost function` is calculated:
$$C=\sum_{i=1}^{10}(\hat{y}-y)^2$$
- step 3. Go back and update the weights $w_i, i=\overline{1,n}$
- step 4. this process is repeated in the `next epoch`. The goal is to find a **minimum** of the `C` cost function.

This whole process described above is called: `back propagation`.

## Gradient Descent

---

The example of the `perceptron` is taking further is this chapter:

### `Brute force` method

Take for instance 1000 weight combinations, calculate the `C` for all and map the values on a chart and find out the best (minimal) one by observation method.

This could get you in the `curse of dimensionality`.

e.g. For a ANN with:

- 4 neurons in the input layer
- 5 neurons in the `1` hidden layer
- 1 neuron in the output layer

Are a total of 25 synapses (`weights`).
For this network the total number of combinations is: $1000^{25}$. This would take more than $10^{50}$ FLOPS which is more than $10^{50}$ years to complete all the calculations.

### `(Batch) Gradient Descent` method

Calculate the slope of the `C` function a a point. If the slope is negative move towards `right`, if the slope is positive move towards `left` and so on, going `downhill` until you get to a `minimum`.

Is named `gradient descent` because you descend into the `minimum` of the cost function.

This works good for `convex functions`,  e.g. Binomial cost functions.

### `Stochastic Gradient Descent` method

If the cost function is not binomial, of is applied for a two dimensional space or bigger then you could run  into `local minimum`s instead of `global minimum`.

In this method, the back propagation is applied for each `observation`.

- the data from `one` observation is feed in
- the $\hat{y}$ - output value - is calculated.
- the $C$ function is computed
- the $w_i$ are adjusted.
- the process is repeated for all the `observations` from the `epoch`

This method is better then the `Batch Gradient Descent` because it has much bigger fluctuations and this helps avoiding the `local minimums`.
Also this method is faster.

The **advantage** of the `Batch Gradient Descent` is a **deterministic algorithm**, rather then the `Stochastic Gradient Descent` is a **random algorithm** method.

## Backpropagation

---

During the `backpropagation` process **ALL** the `weights` are adjusted at the same time.

Training a ANN with `Stochastic Gradient Descent`:

- step1. - Randomly initialize the `weights` to small numbers close to 0 but **not** 0.
- step2. - Feed the data from the `first observation`
- step3. - `Forward Propagation` -  from left to right, the neurons are activated. Propagate the activations until the predicted result $\hat{y}$ is calculated.
- step4. - Compare the `predicted result` with the `actual result` and measure the `generated error`.
- step5. - `Back Propagation` - from right to left, the error is back-propagated into the network. Update the `weights` according to how much are they responsible for the error.
- step6. - repeat  step1-step5 and update weights after **each observation** - `reinforcement learning`. or repeat step1-step5 but update the weights only after a batch of observations - `batch learning`.
- step7. - when the whole set passed through the ANN, that makes an `epoch`. Redo more `epochs`.
