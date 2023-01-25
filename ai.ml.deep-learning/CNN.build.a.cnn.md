# Build a CNN

check the prerequisites from the `ANN.build.an.ann.md` file.

```python
import tensorflow as tf
from kreas.preprocessing.image import ImageDataGenerator
```

the `ImageDataGenerator` is used to preprocess the images. It will apply some transformations to the images to avoid overfitting. The transformations are random, so the same image will not be transformed the same way every time.

# Data Preprocessing

## Preprocessing the Training set

What is overfitting?

`Overfitting` (overtraining) is when the model is too complex and it memorizes the training set. The model is not able to generalize the results and it will not be able to predict the results for new data.

`Overfitting` is avoided by applying some transformations to the images. The transformations are random, so the same image will not be transformed the same way every time.

The transformations also known as image augmentation are:

- `rescale` - rescale the pixel values from `[0, 255]` to `[0, 1]`
- `shear_range` - is a geometrical transformation of the image
- `zoom_range` - is a random zoom
- `horizontal_flip` - is a random horizontal flip

Check out the `keras.io` documentation, `Keras API Reference`, `Data loading`, `image data loading` section, especially ImageDataGenerator class.

**step 1.** create the `ImageDataGenerator` object and pass the transformations as parameters.

```python
train_datagen = ImageDataGenerator(
  rescale = 1./255, # rescale the pixel values from [0, 255] to [0, 1]
  shear_range=0.2, # shear to 20%
  zoom_range=0.2,  # zoom to 20%
  horizontal_flip=True) # do a horizontal flip
```

How to organize the training set?

The training set should be organized in two folders, one for the cats and one for the dogs. The folder names will be the labels for the images.
  
  ```
  dataset
  ├── training_set
  │   ├── cats
  │   │   ├── cat.1.jpg
  │   │   ├── cat.2.jpg
  │   │   ├── ...
  │   ├── dogs
  │   │   ├── dog.1.jpg
  │   │   ├── dog.2.jpg
  │   │   ├── ...
  ├── test_set
  │   ├── cats
  │   │   ├── cat.1001.jpg
  │   │   ├── cat.1002.jpg
  │   │   ├── ...
  │   ├── dogs
  │   │   ├── dog.1001.jpg
  │   │   ├── dog.1002.jpg
  │   │   ├── ...
  ```

**step 2.** create the training set. The `flow_from_directory` method will load the images from the specified directory and apply the transformations.

```python
# training_set
training_set = train_datagen.flow_from_directory(
  'dataset/training_set', # path to training set
  target_size=(64, 64), # size of images for training
  batch_size=32, # number of images to be processed at a time
  class_mode='binary') # binary classification (cat or dog)
```

## Preprocessing the Test set

```python
# no other transformations are needed for the test set, just rescale the pixel values
test_datagen = ImageDataGenerator(rescale = 1./255)
# load the test set
testing_set = test_datagen.flow_from_directory(
  'dataset/test_set', # path to test set
  target_size=(64, 64), # size of images for training
  batch_size=32, # number of images to be processed at a time
  class_mode='binary') # binary classification (cat or dog)
```

# Building the CNN

The CNN is a sequence of layers. The layers are added to the CNN using the `add` method.

## Initializing the CNN

```python
cnn = tf.keras.models.Sequential()
```

## Step 1 - Convolution

```python
cnn.add( # add a convolution layer
  tf.keras.layers.Conv2D( # 2D convolution layer
    filters=32, # number of filters
    kernel_size=3, # size of the filter 3x3
    activation='relu', # activation function - rectifier function
    strides=1, # stride of the convolution window
    input_shape=[64, 64, 3] # shape of the input images - 64x64 pixels, 3 channels (RGB)
  )
)
```

## Step 2 - Pooling

```python
cnn.add( # add a pooling layer
  tf.keras.layers.MaxPool2D( # 2D max pooling layer
    pool_size=2, # size of the pooling window 2x2
    strides=2 # stride of the pooling window
    ) 
)
```

## Adding a second convolutional layer

The second convolutional layer does not need the `input_shape` parameter, because the input shape is known from the previous layer.

```python
cnn.add(
  tf.keras.layers.Conv2D(
    filters=32,
    kernel_size=3,
    activation='relu',
    # no input shape is needed, the input shape is known from the previous layer
  )
)
cnn.add( tf.keras.layers.MaxPool2D(pool_size=2, strides=2) )
```

## Step 3 - Flattening

Flatting is the process of converting the pooled feature maps to a single vector.

```python
cnn.add( tf.keras.layers.Flatten() )
```

## Step 4 - Full Connection

```python
cnn.add( 
  tf.keras.layers.Dense(
    units=128, # number of neurons
    activation='relu' # activation function - rectifier function
  ) 
)
```

## Step 5 - Output Layer

```python
cnn.add( 
  tf.keras.layers.Dense(
    units=1, # number of neurons
    activation='sigmoid' # activation function - sigmoid function
  ) 
)
```

# Training the CNN

## Compiling the CNN

```python
cnn.compile(
  optimizer='adam', # optimizer - stochastic gradient descent
  loss='binary_crossentropy', # loss function - logarithmic loss
  metrics=['accuracy'] # metrics - accuracy
)
```

## Training the CNN on the Training set and evaluating it on the Test set

```python
cnn.fit(
  x=training_set, # training set
  validation_data=testing_set, # test set
  epochs=25 # number of epochs
)
```

# Making a single prediction

```python
import numpy as np # for mathematical operations


# load image and resize it to 64x64
test_image = tf.keras.utils.load_img(
  'dataset/single_prediction/cat4.jpg', # path to image
  target_size = (64, 64) # size of image - same as training set
)

# convert image to array
test_image = tf.keras.utils.img_to_array(test_image)

# add extra dimension to array because predict method expects a batch of images
test_image = np.expand_dims(
  test_image, 
  axis=0 # add extra dimension at index 0
)

# predict image which is a cat or dog (0 or 1)
# cat is 0 because of the order of the classes in the training set
# /255.0 to normalize the pixel values
result = cnn.predict(test_image/255.0)
training_set.class_indices
if result[0][0] < 0.5: # if result is less than 0.5, then it is a cat
  prediction = 'cat'
else:
  prediction = 'dog'
  
print(prediction)
```
