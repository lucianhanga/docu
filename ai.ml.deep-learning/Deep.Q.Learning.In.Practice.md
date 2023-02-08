# Deep Q-Learning in Practice

# Prerequisites

To implement it in python the choice for a library would be `pytorch`. 

```python
import torch # pytorch
import torch.nn as nn # neural networks
import torch.nn.functional as F # functions for neural networks
import torch.optim as optim # optimizers which will be used to update the weights of the neural network
import torch.autograd as autograd # to create variables that will contain the states, actions and rewards
from torch.autograd import Variable # to create variables that will contain the states, actions and rewards from tensors
```

in `pytorch` the **neural network** is defined by a class that inherits from `nn.Module` and it has to implement the `forward` method. The `forward` method is the method that will be called when the neural network is used to predict the Q-values.

```python

class Network(nn.Module):
    # the parameters of the class are:
    # the input size - the number of states
    # the number of actions - the number of outputs
    def __init__(self, input_size, nb_action):
        super(Network, self).__init__()
        self.input_size = input_size
        self.nb_action = nb_action
        # the first layer is a fully connected layer with 30 neurons
        self.fc1 = nn.Linear(input_size, 30)
        # the second layer is a fully connected layer with the number of actions (nb_action)
        self.fc2 = nn.Linear(30, nb_action)
    # the forward method is the method that will be called when the neural network is used to predict the Q-values    
    def forward(self, state):
        x = F.relu(self.fc1(state))
        q_values = self.fc2(x)
        return q_values
```
