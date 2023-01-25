# CNN - Convolutional Neural Networks

**Yann Lecun** is the grandfather of the convolution neural networks.

How Convolutional Neural Network works?

```text
Input Image -> CNN -> Output Label (Image Class/classification)
```

For instance a CNN can be trained to recognize emotions from facial expression pictures. The output value is a probability.

## Basic Blocks

The basic blocks of the CNN are images:

- **B/W images** - are `2d arrays` containing bytes with values from `0...255` representing black, gray scales and white for each pixel from the image.

- **Color Images** - are 3d arrays containing on the Z axis 3 planes: `red`, `green`, `blue`. Each of the plane being a  `2d array` containing values from `0...255` which are the intensity of the plane color.

The steps which the images are processed for a CNN are:

- step1. `Convolution`
- step2. `Max Pooling`
- step3. `Flattening`
- step4. `Full Connection`

## Convolution

The `convolution` is a mathematical operation which is used to calculate the `dot product` of two functions.

$$ (f*g)(t) = \int_{-\infty}^{\infty} f(\tau)g(t-\tau) d\tau $$

`Feature Detection Matrix (Filter)` is a `3x3` matrix which is used to detect a feature in the image. The feature detection matrix is applied to the image by the `convolution` operation. The dimensions of the feature detection matrix should not necessary be `3x3`. It can be `5x5` or `7x7` or any other size.

The `convolution` operation is applied to the image by sliding the feature detection matrix over the image.
The values are multiplied (`logical and` operation) by the values of the image and the result is the `dot product` of the two functions. The `dot product` is the sum of the products of the corresponding entries of the two sequences of numbers.

`Stride` is the number of pixels which the feature detection matrix is moved over the image. Usually the stride is `2` pixel. The stride can be `1` pixels or any other number. If the stride is bigger the process is faster but the **accuracy** is lower.

The resulted matrix is called `Feature Map`. Also known as `Activation Map`.

During the training of the CNN the `feature detection matrix (filter)` is updated by the `back propagation` algorithm and more `Feature maps` are created.
All the `Feature maps` are called `Convolution Layer`.

## Convolution - ReLU Layer

The `ReLU` is the `Rectified Linear Unit` function. It is used to add non-linearity to the CNN. The `ReLU` function is applied to the `Convolution Layer` and the resulted matrix is called `ReLU Layer`.

$$ \phi(x) = max(0, x) $$

$$ \sum_{i=1}^{m} w_ix_i $$

## Max Pooling

`Spatial Invariance` is the property of the CNN to recognize the same object in different positions of the image. The `Max Pooling` is used to reduce the size of the `Convolution Layer` and to keep the `Spatial Invariance`.

`Max Pooling` is applied to the `Convolution Layer` by sliding a `2x2` matrix over the `Convolution Layer` and taking the `maximum value` from the matrix. Stride is `2` pixels by default, but it can be any other number.

```text
Feature Map (Convolution Layer) -> Max Pooling -> Pooled Feature Map
```

 `Max Pooling` is preserving the features but account for distortions and variations in the image. Also reduces the size of the `Convolution Layer` by `75%` which reduces the number of the parameters in the `Full Connection` layer.

## Flattening

The `Flattening` is the process of converting the `Pooled Feature Map` to a `1d array` which is used as an input for the ANN Input Layer (the `Full Connection` layer).

## Full Connection

Add the ANN to the Convoluted Neural Network.

- Input Layer - the `Flattened Pooled Feature Map`
- Fully Connected Layer - (in ANN was called `Hidden Layer`)
- Output Layer - the `Output Label` - because is done a classification are going to be more than one output neurons.

In ANN the hidden layers don't necessarily have to be `Fully Connected` but in CNN the the hidden layers are `Fully Connected`.

In case of CNN the back propagation algorithm is used to update the weights of the `Fully Connected` layer and also the `Feature Detection Matrix (Filter)`.

The neurons in the final hidden layer are called `Feature Detector` contain features which are repressive for the results and they `vote` for the `Output Label`. And the output neurons decide on what neurons from the last hidden layer are listen to.

## Summary

```text
Input Image -> Convolution -> ReLU -> Max Pooling -> Flattening -> Full Connection -> Output Label
```

## Softmax & Cross Entropy

The `Softmax` function is used to calculate the probability of the `Output Label`. The `Softmax` function is applied to the `Output Layer` and the resulted matrix is called `Softmax Layer`.

$$ \phi(z_i) = \frac{e^{z_i}}{\sum_{j=1}^{K} e^{z_j}} $$

Softwmax is the `Normalized Exponential Function`.

After applying the softmax function the output layer is converted to a probability distribution. And the sum of all the probabilities is `1`.

Cross Entropy is the `Loss Function` which is used to calculate the error of the `Output Layer`. The `Cross Entropy` is applied to the `Softmax Layer` and the resulted matrix is called `Cross Entropy Layer`.

$$ H(p, q) = - \sum_{x} p(x) \log q(x) $$

`p` is the `Output Label` and `q` is the `Softmax Layer`.

`Classification Error` id the did you get it right or wrong calculation in portents. The `Classification Error` is applied to the `Output Layer` and the resulted matrix is called `Classification Error Layer`.

$$ \frac{1}{n} \sum_{i=1}^{n} 1(y_i \neq \hat{y_i}) $$

`Mean Squared Error` is the error calculation in portents. The `Mean Squared Error` is applied to the `Output Layer` and the resulted matrix is called `Mean Squared Error Layer`.

$$ \frac{1}{2} \sum_{i=1}^{n} (y_i - \hat{y_i})^2 $$

`Cross entry` is used for `classification` and `mean squared error` is used for `regression`.
