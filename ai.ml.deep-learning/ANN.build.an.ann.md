# Building an ANN

Following the udemy, Deep Learning A-Z™: Hands-On Artificial Neural Networks course, we will build an ANN to predict if a customer will leave a bank or not.

For this you need either a `jupyter` notebook or `google colab`.

First install the dependencies for the `jupyter` notebook:

```bash
pip3 install numpy
pip3 install pandas
pip3 install tensorflow
```

installing `sklearn` migth be a bit troublesome. If the line bewlow does not work, and you will see this when you try to import it:

```bash
pip3 install sklearn
```

 try the following:

```bash
pip3 install pytest
pip3 install --pre scikit-learn
```

`numpy` is used for the math operations.<br>
`pandas` for the data manipulation.<br>
`tensorflow` for the ANN.<br>
`sklearn` for the data preprocessing.

import the libraries

```python
import numpy as np
import pandas as pd
import tensorflow as tf
```

# Data Preprocessing

## Basic Data Preprocessing

### Importing the dataset

Read the dataset and split it into `x` and `y`. Also clean the data. The information about index, customer id and surname is not needed for the prediction.
`y` is the dependent variable, the one we want to predict and is the last one in the dataset.

```python
dataset = pd.read_csv('Churn_Modelling.csv')
x = dataset.iloc[:, 3:13].values
y = dataset.iloc[:, 13].values
```

## Advanced Data Preprocessing

### Encoding categorical data

Data such country of residence is a so called categorical data. It is not a number, but a string. We need to encode it to a number. In case of categorical data there is no relationship order between the values.

#### Encode the sex using `LabelEncoder`

The `LabelEncoder` encodes the values to a number.

```python
  from sklearn.preprocessing import LabelEncoder
  labelencoder_x_2 = LabelEncoder()
  # take all the rows and the 2nd column - hence the x[:, 2]
  x[:, 2] = labelencoder_x_2.fit_transform(x[:, 2])
```

#### Encode the country using `OneHotEncoder`

`OneHotEncoder` is used to encode the country. It is a bit more complicated than the `LabelEncoder`. It creates a new column for each country and encodes the country to a 1 or 0. The 1 is for the country and 0 for the other countries.

```python
  from sklearn.compose import ColumnTransformer
  from sklearn.preprocessing import OneHotEncoder
  ct = ColumnTransformer(transformers=[('encoder', OneHotEncoder(), [1])], remainder='passthrough')
  x = np.array(ct.fit_transform(x))
```

In our example there were three countries. The first column is for France, the second for Germany and the third for Spain. And they were encoded like this:<br>
`[1, 0, 0]` for France,<br>
`[0, 1, 0]` for Germany and <br>
`[0, 0, 1]` for Spain.

```output
[[1.0 0.0 0.0 619.0 0.0 42.0 2.0 0.0 1.0 1.0 101348.88 1.0]
 [0.0 0.0 1.0 608.0 0.0 41.0 1.0 83807.86 1.0 0.0 112542.58 0.0]
 [1.0 0.0 0.0 502.0 0.0 42.0 8.0 159660.8 3.0 1.0 113931.57 1.0]
 ...
 [1.0 0.0 0.0 709.0 0.0 36.0 7.0 0.0 2.0 1.0 42085.58 1.0]
 [0.0 1.0 0.0 772.0 0.0 42.0 3.0 75075.31 2.0 0.0 92888.52 1.0]
 [1.0 0.0 0.0 792.0 0.0 28.0 4.0 130142.79 2.0 0.0 38190.78 0.0]]
```

## Splitting the dataset into the Training set and Test set

Splitting the dataset into the Training set and Test set is a must. The model should not be trained on the same data it is tested on. The model should be trained on the training set and tested on the test set. The test set is the data the model has never seen before.

```python
  from sklearn.model_selection import train_test_split
  x_train, x_test, y_train, y_test = train_test_split(x, y, test_size = 0.2, random_state = 0)
```

## Feature Scaling

What is feature scaling ?<br>
Feature scaling is a method used to `normalize` the range of independent variables or features of data. In data processing, it is also known as `data normalization` and is generally performed during the data preprocessing step.

`Feature Scaling` is important because it makes the model converge faster. It is not needed for the ANN, but it is a good practice to do it.

```python
  from sklearn.preprocessing import StandardScaler
  sc = StandardScaler()
  x_train = sc.fit_transform(x_train)
  x_test = sc.transform(x_test)
```

# Building the ANN

## Initializing the ANN

Create a `sequential ANN`. The sequential ANN is a linear stack of layers. It is the most common ANN.

```python
  ann = tf.keras.models.Sequential()
```

## Adding the input layer and the first hidden layer

The number of neurons of the `input layer` is the number of independent variables. The number of neurons of the `hidden layer` is the average of the number of neurons of the input layer and the number of neurons of the output layer. The number of neurons of the output layer is the number of dependent variables.

> **IMPORTANT** However the number of neurons of the hideen layer **is not a rule**. It is a good practice to try different numbers of neurons and see which one gives the best results.

```python
  ann.add(tf.keras.layers.Dense(units=6, activation='relu'))
```

Use the `rectifier function` as the activation function for the hidden layer. The rectifier function is the `relu` function.

## Adding the second hidden layer

Same thing like the first hidden layer.

```python
  ann.add(tf.keras.layers.Dense(units=6, activation='relu'))
```

## Adding the output layer

The number of neurons of the output layer is the number of `dependent variables`. The activation function of the output layer is the `sigmoid` function. The `sigmoid` function is used for a **binary outcome**. For non-binary clasifications should be used the `softmax` function.

```python
  ann.add(tf.keras.layers.Dense(units=1, activation='sigmoid'))
```

# Training the ANN

## Compiling the ANN

The `adam` optimizer is used to optimize the weights. Is using stochastic gradient descent. <br>

The `loss` function is the `binary_crossentropy` function. The loss function is used to calculate the loss between the predicted value and the real value The `binary_crossentropy` function is used for a **binary outcome**. For non-binary clasifications should be used the `categorical_crossentropy` function. <br>

The `metrics` is the `accuracy` function. The accuracy function is used to calculate the accuracy of the model.
Other metrics can be used like the `precision` or the `recall`. `Precision` is the ratio of correctly predicted positive observations to the total predicted positive observations. `Recall` is the ratio of correctly predicted positive observations to the all observations in actual class.

```python
  ann.compile(optimizer = 'adam', loss = 'binary_crossentropy', metrics = ['accuracy'])
```

## Training the ANN on the Training set

```python
  ann.fit(x_train, y_train, batch_size = 32, epochs = 100)
```

# Making the predictions and evaluating the model

## Predicting the result of a single observation

for instance:

- `Geography`: France - encoded as `[1, 0, 0]`
- `Credit Score` : 600
- `Gender` : male - encoded as `1`
- `Age` : 40 years old
- `Tenure` : 3 years
- `Balance` : 60000
- `Number of Products` : 2
- `Has Credit Card` : yes - encoded as `1`
- `Is Active Member` : yes - encoded as `1`
- `Estimated Salary` : 50000

```python
  print(ann.predict(sc.transform([[1, 0, 0, 600, 1, 40, 3, 60000, 2, 1, 1, 50000]])) > 0.5)
```

`sc.transform` is used to scale the data. The data should be scaled before making the prediction.<br>
`ann.predict` is used to make the prediction.
`> 0.5` is used to convert the probability to a boolean value. If the probability is greater than 0.5 the result is `True` else the result is `False`.

## Predicting the Test set results

```python
  y_pred = ann.predict(x_test)
  y_pred = (y_pred > 0.5)
  print(np.concatenate((y_pred.reshape(len(y_pred),1), y_test.reshape(len(y_test),1)),1))
```

result would be something like :
  
  ```python
    [[0 0]
    [0 0]
    [0 0]
    ...
    [0 0]
    [1 1]
    [0 0]]
  ```

  `0` means the customer did not leave the bank and `1` means the customer left the bank.
  The first element is the `predicted value` and the second element is the `real value`.

## Making the Confusion Matrix

What is a confusion matrix ?<br>
A `confusion matrix` is a table that is often used to describe the performance of a classification model (or "classifier") on a set of test data for which the true values are known.

```python
  from sklearn.metrics import confusion_matrix, accuracy_score
  cm = confusion_matrix(y_test, y_pred)
  print(cm)
  accuracy_score(y_test, y_pred)
```

result would be something like :

```python
  [[1528   67]
  [ 197  208]]

  0.8615
```

`First row` is about the customers who did **not** leave the bank. <br>
The `first column` is about the customers who did **not** leave the bank - **correct prediction**<br> and the `second column` is about the customers who left the bank.

The `second row` is about the customers who left the bank.<br> The `first column` is about the customers who did **not** leave the bank<br> and the `second column` is about the customers who left the bank - **correct prediction**.
