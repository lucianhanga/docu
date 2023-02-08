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

## Implementing tje Neural Network

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
    # parameter state is the input of the neural network
    def forward(self, state):
        # the first layer is a fully connected layer with 30 neurons
        # the activation function is the rectifier function
        # the input is the state, the output is x which is the input of the second layer
        x = F.relu(self.fc1(state))
        # the second layer is a fully connected layer with the number of actions (nb_action) - the output of the neural network - the Q-values for each action
        q_values = self.fc2(x)
        # the output of the neural network is the Q-values for each action
        # of type Variable
        return q_values
```

the `reulu` function is the rectifier function which is defined as:

$$ f(x) = max(0, x) $$

the `forward` method is the method that will be called when the neural network is used to predict the Q-values. The first layer is a fully connected layer with 30 neurons. The activation function is the rectifier function. The input is the state, the output is `x` which is the input of the second layer. The second layer is a fully connected layer with the number of actions (nb_action) - the output of the neural network - the Q-values for each action. The output of the neural network is the Q-values for each action of type `Variable`.

## Implementing the Experience Replay

Keep the last 100 transitions in a memory. The memory is a list of tuples. Each `tuple` contains the **last state, the last action, the last reward and the new state**. The memory is implemented as a class.

```python
class ReplayMemory (object):
  # the parameters of the class are:
  # the capacity of the memory - the number of transitions that will be kept in the memory
  def __init__(self, capacity):
    self.capacity = capacity
    self.memory = [] # initialize the memory as an empty list
  
  # the push method is used to add a new transition to the memory
  # the parameters are a tuple: (last state, last action, the last reward, the new state)
  def push(self, event):
    self.memory.append(event) # add the new transition to the memory
    if len(self.memory) > self.capacity: # if the memory is full
      del self.memory[0] # delete the first transition in the memory

  # the sample method is used to get a random batch of transitions from the memory
  # the parameter is the size of the batch
  def sample(self, batch_size):
    # get a random batch of transitions from the memory
    samples = zip(*random.sample(self.memory, batch_size))
    # return the transitions as a tuple of tensors
    # apply the function torch.cat to each element of the tuple
    return map(lambda x: Variable(torch.cat(x, 0)), samples)
```

the function `random.sample` is used to get a random batch of transitions from the memory. The parameter is the size of the batch. The function `zip` is used to get the transitions as a tuple of tensors.

## Implementing the Deep Q-Learning

```python
class Dqn():
 
  # the parameters of the class are:
  # the input size - the number of states
  # the number of actions - the number of outputs
  # the discount factor - gamma
  # the learning rate - alpha
  def __init__(self, input_size, nb_action, gamma, learning_rate):
    self.gamma = gamma # the discount factor
    # the reward window is used to calculate the average reward of the last 100 episodes
    # to see if the agent is learning - is a measure of the progress of the agent
    self.reward_window = [] # the rewards of the last 100 episodes
    self.model = Network(input_size, nb_action) # the neural network
    self.memory = ReplayMemory(100000) # the memory
    # the optimizer is used to update the weights of the neural network
    # Adam is an optimizer that is based on adaptive estimation of first-order and second-order moments - the learning rate is not fixed - make it 0.001 
    self.optimizer = optim.Adam(self.model.parameters(), lr = learning_rate)
    self.last_state = torch.Tensor(input_size).unsqueeze(0) # the last state
    self.last_action = 0 # the last action
    self.last_reward = 0 # the last reward

  # the select_action method is used to select the action
  # the parameter is the current state
  def select_action(self, state):
    # the probability of the action is calculated by the softmax function
    # the output is the probability of the action
    # temperature parameter is used to increase the probability of the action
    # the temperature will make the small probabilities even smaller and the large probabilities even larger
    probs = F.softmax(self.model(Variable(state, volatile = True))*7) # T=7
    # the action is selected by the probability of the action
    # the output is the action
    action = probs.multinomial(num_samples = 1) # the action is selected by the probability of the action
    return action.data[0, 0] # because the action is a tensor of size 1x1
 ```

 The `softmax` function gives us a **distribution of probabilities for each action**. The probability of the action is calculated by the softmax function. The output is the probability of the action. 
 
 The `temperature` parameter is used to increase the probability of the action. The temperature will make the small probabilities even smaller and the large probabilities even larger. 
 
The `multinomial` function is used to select the action by the probability of the action. The output is the action. Its a random draw from the **multinomial** distribution parameterized by the probabilities of the actions.

```python
  # the learn method is used to update the neural network
  # the parameters are the last state, the last action, the last reward and the new state
  def learn(self, batch_state, batch_next_state, batch_reward, batch_action):
    # the output of the neural network is the Q-values for each action
    outputs = self.model(batch_state).gather(1, batch_action.unsqueeze(1)).squeeze(1)
    # the target is the Q-value of the action that was taken
    next_outputs = self.model(batch_next_state).detach().max(1)[0]
    target = self.gamma*next_outputs + batch_reward
    # the loss is the mean squared error between the target and the output
    td_loss = F.smooth_l1_loss(outputs, target)
    # the optimizer is used to update the weights of the neural network
    self.optimizer.zero_grad() # initialize the gradients to zero
    td_loss.backward(retain_variables = True) # backpropagation
    self.optimizer.step() # update the weights of the neural network

  # the update method is used to update the neural network
  # the parameters are the new state, the new reward and the new action
  def update(self, reward, new_signal):
    new_state = torch.Tensor(new_signal).float().unsqueeze(0) # the new state
    self.memory.push((self.last_state, new_state, torch.LongTensor([int(self.last_action)]), torch.Tensor([self.last_reward]))) # add the new transition to the memory
    action = self.select_action(new_state) # select the action
    if len(self.memory.memory) > 100: # if the memory is full
      # get a random batch of transitions from the memory
      batch_state, batch_next_state, batch_reward, batch_action = self.memory.sample(100)
      # update the neural network
      self.learn(batch_state, batch_next_state, batch_reward, batch_action)
    self.last_action = action # the last action
    self.last_state = new_state # the last state
    self.last_reward = reward # the last reward
    self.reward_window.append(reward) # add the new reward to the reward window
    if len(self.reward_window) > 1000
      del self.reward_window[0] # delete the first reward in the reward window
    return action # return the action
```

