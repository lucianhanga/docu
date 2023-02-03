# Build a RBM - Restricted Boltzmann Machine

## dependencies and imports

This example will be build using pytorch. So we need to import the pytorch library.

```python
    import torch
    import torch.nn as nn
    import torch.nn.parallel
    import torch.optim as optim
    import torch.utils.data
    from torch.autograd import Variable

    # also 
    import numpy as np # for the data
    import pandas as pd # for the data 
```

##  load the data 

Check out the Jupiter python file from the `ai.ml-deep-learning` folder

## Converting data to torch tensors

**Tensor** is a generalization of `vectors` and `matrices` to potentially higher dimensions. Internally, `PyTorch` represents tensors as `n-dimensional` arrays. 
`Tensors` are similar to **NumPy’s** `ndarrays`, except that tensors can run on GPUs or other specialized hardware to accelerate computing.

```python
    training_set = torch.FloatTensor(training_set)
    test_set = torch.FloatTensor(test_set)
```


## Bernoulli Sampling

The Bernoulli sampling is a way to sample a random number from a Bernoulli distribution. The Bernoulli distribution is a discrete probability distribution that takes the value `1` with probability `p` and the value `0` with probability `q = 1 − p`.

Take a random number between 0 and 1. If the random number is smaller than the probability of the neuron being activated, then the neuron is activated. If the random number is greater than the probability of the neuron being activated, then the neuron is not activated.

```python
    def sample_h(self, x):
        wx = torch.mm(x, self.W.t())
        activation = wx + self.b
        p_h_given_v = torch.sigmoid(activation)
        return p_h_given_v, torch.bernoulli(p_h_given_v)
```