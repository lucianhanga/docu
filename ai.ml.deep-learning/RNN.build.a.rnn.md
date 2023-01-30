# Build a RNN

Library imports:

```python
import numpy as np # for mathematical operations - arrays
import matplotlib.pyplot as plt # visualization - plotting
import pandas as pd # data processing - import and manage datasets
```

# Preprocessing

## Step 1 - Importing the training set

```python
# Importing the training set
dataset_train = pd.read_csv('Google_Stock_Price_Train.csv')
# Selecting the Open column - the only one of interest
training_set = dataset_train.iloc[:, 1:2].values 
```

## Step 2 - Feature Scaling

### Standardization

`Standardization` is a useful technique to transform attributes with a Gaussian distribution and differing means and standard deviations to a standard Gaussian distribution with a `mean` of `0` and a `standard deviation` of `1`.

$$x_{stand} = \frac{x - \mu}{\sigma}$$

where:

$\mu$ is the mean of the dataset and $\sigma$ is the standard deviation.
$$\mu = \frac{1}{m}\sum_{i=1}^{m}x_{i}$$
$$\sigma = \sqrt{\frac{1}{m}\sum_{i=1}^{m}(x_{i} - \mu)^2}$$

### Normalization

`Normalization` is the process of scaling individual samples to have unit norm. This process can be useful if you plan to use a quadratic form such as the dot-product or any other kernel to quantify the similarity of any pair of samples.

$$x_{norm} = \frac{x - x_{min}}{x_{max} - x_{min}}$$

```python
# Feature Scaling
from sklearn.preprocessing import MinMaxScaler
sc = MinMaxScaler(feature_range = (0, 1))
training_set_scaled = sc.fit_transform(training_set)
```

In this case is applied `Normalization` because the sigmoid activation function is used in the output layer.

```python
from sklearn.preprocessing import MinMaxScaler # normalization class
sc = MinMaxScaler(feature_range = (0, 1)) # normalization object
training_set_scaled = sc.fit_transform(training_set) # normalization of the training set
```

Now all the values are between 0 and 1.

## Step 3 - Creating a data structure with 60 timesteps and 1 output

60 timesteps means that the RNN will look at the 60 stock prices before time `t` and based on the trends it detects, it will try to predict the next output.

```python
X_train = [] # 60 timesteps
y_train = [] # 1 output the next stock price
for i in range(60, 1258): 
    X_train.append(training_set_scaled[i-60:i, 0]) # 60 previous stock prices at time t
    y_train.append(training_set_scaled[i, 0]) # next stock price at time t+1

X_train, y_train = np.array(X_train), np.array(y_train) # convert to numpy arrays
```

## Step 4 - Reshaping

Reshaping is required because the RNN expects a 3D input. Also can be used to add more indicators.

3D tensor with shape `(batch_size, timesteps, input_dim)`

```python
X_train = np.reshape(
  X_train,# the data to reshape 
  (  
    X_train.shape[0], # the number of observations
    X_train.shape[1], # the number of time steps
    1 # the number of indicators
  )
)
```

# Building the RNN

## Step 1 - Importing the Keras libraries and packages

```python
from keras.models import Sequential # initialize the RNN
from keras.layers import Dense # add the output layer
from keras.layers import LSTM # add the LSTM layer
from keras.layers import Dropout # add the Dropout regularisation
```

## Step 2 - Initialising the RNN

```python
regressor = Sequential() # initialize the RNN
```

## Step 3 - Adding the first LSTM layer and some Dropout regularisation

LSTM object parameters:

- units: the number of LSTM units
- return_sequences: return the sequences - `true` if there are more LSTM layers, the last one should be `false`
- input_shape: the shape of the input meaning the number of time steps and the number of indicators

```python
regressor.add(LSTM(
  units = 50, # the number of LSTM units (neurons)
  return_sequences = True, # return the sequences
  input_shape = (X_train.shape[1], 1) # the shape of the input
))
regressor.add(Dropout(0.2)) # add the Dropout regularization
```

Droupout regularization is important to avoid `overfitting`. It randomly drops out a fraction of the units in the layer during training.

## Step 4 - Adding a second LSTM layer and some Dropout regularisation

```python
regressor.add(LSTM(units = 50, return_sequences = True))
regressor.add(Dropout(0.2))
```

## Step 5 - Adding a third LSTM layer and some Dropout regularisation

```python
regressor.add(LSTM(units = 50, return_sequences = True))
regressor.add(Dropout(0.2))
```

## Step 6 - Adding a fourth LSTM layer and some Dropout regularisation

```python
regressor.add(LSTM(units = 50)) # the last LSTM layer should not return the sequences
regressor.add(Dropout(0.2))
```

Why 4 LSTM layers?

- The more layers the better the performance
- But the more layers the more the computation time
- But the more layers the more the risk of overfitting

## Step 7 - Adding the output layer

output layer has only one unit because we want to predict only one value - the next stock price.

```python
regressor.add(Dense(units = 1)) # add the output layer
```

# Training the RNN

## Step 8 - Compiling the RNN

```python
regressor.compile(optimizer = 'adam', loss = 'mean_squared_error') # compile the RNN
```

`Adam` is a stochastic gradient descent method that is based on adaptive estimation of first-order and second-order moments.

Mean Squared Error is used because the output is a continuous value.
$$MSE = \frac{1}{n}\sum_{i=1}^{n}(y_{i} - \hat{y_{i}})^2$$

## Step 9 - Fitting the RNN to the Training set

```python
regressor.fit(
  X_train, # the training set
  y_train, # the output set
  epochs = 100, # the number of epochs
  batch_size = 32 # the batch size
)
```

# Making the predictions and visualising the results

## Step 10 - Getting the real stock price of 2017

```python
dataset_test = pd.read_csv('Google_Stock_Price_Test.csv')
real_stock_price = dataset_test.iloc[:, 1:2].values
```

## Step 11 - Getting the predicted stock price of 2017

To predict the stock price for day `t` we need the stock prices for the 60 previous days. For this you need to concatenate the training set (at least the last 60 days from it) and the test set.

```python
dataset_total = pd.concat(
  # concatenate the training set and the test set - original datasets 
  (dataset_train['Open'], dataset_test['Open']), # 
  axis = 0 # concatenate vertically
)

inputs = dataset_total[len(dataset_total) - len(dataset_test) - 60:].values # get the last 60 days from the training set
inputs = inputs.reshape(-1,1) # reshape the inputs - 1 column - 1 indicator
inputs = sc.transform(inputs) # normalize the inputs

X_test = [] # 60 timesteps  
for i in range(60, 80): # 20 days
    X_test.append(inputs[i-60:i, 0]) # 60 previous stock prices at time t
X_test = np.array(X_test) # convert to numpy arrays
X_test = np.reshape(
  X_test, # the data to reshape 
  (  
    X_test.shape[0], # the number of observations
    X_test.shape[1], # the number of time steps
    1 # the number of indicators
  )
)
predicted_stock_price = regressor.predict(X_test) # predict the stock price
predicted_stock_price = sc.inverse_transform(predicted_stock_price) # denormalize the stock price
```

Denomalization is required because the stock price is normalized.
denormalization formula:
$$x_{denormalized} = x_{normalized} * (max - min) + min$$
