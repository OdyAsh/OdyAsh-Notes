# HuggingFace

## Making HF's `datasets` similar to `flow_from_dataframe()`

Step 1:
create large df of 2 columns: `filepath` and `label`:

```python
# Create a dataframe with the file paths and labels of your images
all_images_df = pd.DataFrame({'filepath': [], 'label': []})
for class_name in [cn for cn in os.listdir(dataDir) if not cn.startswith('.')]: # to avoid hidden folders
    class_dir = joinPaths(dataDir, class_name)
    file_names = os.listdir(class_dir)
    file_paths = [joinPaths(class_dir, file_name) for file_name in file_names]
    labels = [class_name] * len(file_names)
    class_data = pd.DataFrame({'filepath': file_paths, 'label': labels})
    all_images_df = pd.concat([all_images_df, class_data])
len(all_images_df), all_images_df['label'].value_counts()
```

Step 2:
train/val/test split:

```python
# Split the dataframe into training (70%), validation (15%), and testing (15%) sets
train_data, val_test_data = train_test_split(all_images_df, test_size=0.3, random_state=42, shuffle=True)
val_data, test_data = train_test_split(val_test_data, test_size=0.5, random_state=42, shuffle=True)

train_data.to_csv(dataReDir+'train_datav01.csv', index=False) # uncomment these 3 lines of code if the images are updated
val_data.to_csv(dataReDir+'val_datav01.csv', index=False) 
test_data.to_csv(dataReDir+'test_datav01.csv', index=False) 
```

then you can later load them like so:

```python
train_data = pd.read_csv(dataReDir+'train_datav01.csv')
val_data = pd.read_csv(dataReDir+'val_datav01.csv')
test_data = pd.read_csv(dataReDir+'test_datav01.csv')
```

Step 3:
use `load_dataset()` with these arguments:

```python
from datasets import load_dataset

data_files = {'train': list(train_data[filepath]),
              'val': list(val_data[filepath]),
              'test': list(test_data[filepath])}

dataset = load_dataset(r'D:\CS\projects\graduation_project\dataset', name='abc', data_files=data_files, streaming=True)
```

then it can be iterated from its generator like so:

```python
next(dataset['train'].iter(batch_size))['image']
```

however, this technique is flawed, as it doesn't encode the labels of each filepath, so we don't know any of the images' classes.



# TensorFlow vs PyTorch

## Theoretical
Check out [this](https://www.assemblyai.com/blog/pytorch-vs-tensorflow-in-2023/) article

## Practical
### Input to Model
the input shape of the PyTorch model is `(batch_size, num_channels, height, width)`, where `batch_size` can be any positive integer, unlike in TensorFlow where the input shape is fixed at `(width, height, num_channels)`. This is because PyTorch expects the batch dimension to be specified explicitly in the input tensor, whereas TensorFlow implicitly assumes a batch size of 1.



# TensorFlow Tips
## Importing Images and Doing The Train/Val/Test Split

### Using split-folders method
create `split_dataset_folders.py` file with this code to split the dataset into 3 folders:
```python
# source: https://youtu.be/C6wbr1jJvVs

# if you're using a .conda environment, run the following script in the terminal:
# python split_dataset_folders.py

import splitfolders  # or import split_folders

input_folder = 'dataset/'

# Split with a ratio.
# To only split into training and validation set, set a tuple to `ratio`, i.e, `(.8, .2)`.
#Train, val, test
splitfolders.ratio(input_folder, output="dataset_split", 
                   seed=42, ratio=(.7, .15, .15), 
                   group_prefix=None) # default values


# Split val/test with a fixed number of items e.g. 100 for each set.
# To only split into training and validation set, use a single number to `fixed`, i.e., `10`.
# enable oversampling of imbalanced datasets, works only with fixed
# splitfolders.fixed(input_folder, output="dataset2", 
#                    seed=42, fixed=(35, 20), 
#                    oversample=False, group_prefix=None) 
```

Then, use the 3 folders like this:

```python
train_gen = train_datagen.flow_from_directory(f'{dataSplit}train/', classes=None, class_mode='categorical', # classes = None means that the classes will be inferred
                                        target_size=(306,306), seed=42, batch_size=32, color_mode='rgb', shuffle=True) # will later change to color_mode = grayscale

val_gen = val_datagen.flow_from_directory(f'{dataSplit}val/', classes=None, class_mode='categorical',
                                        target_size=(306,306), seed=42, batch_size=32, color_mode='rgb', shuffle=True)

test_gen = test_datagen.flow_from_directory(f'{dataSplit}test/', classes=None, class_mode='categorical',
                                        target_size=(306,306), seed=42, batch_size=32, color_mode='rgb', shuffle=False)
```

such that the `test_gen` is used for this:

```python
from sklearn.metrics import classification_report
yPredOneHotEncoded = model.predict(test_gen, workers=10)
yTrue = test_gen.labels[:len(yPredOneHotEncoded)]
crDict = classification_report(yTrue, np.argmax(yPredOneHotEncoded, axis=1), \
							   target_names=list(test_gen.class_indices.keys()), \
							   output_dict=True)
```

## Using `flow_from_directory()` and CSV method

[source](<https://sharegpt.com/c/CjIgS2c#:~:text=can%20use%20the-,flow_from_dataframe,-()%20method%20of>)

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from keras.preprocessing.image import ImageDataGenerator

# Set the path to the directory containing all the image files
data_dir = '/path/to/dataset'

# Create a dataframe with the file paths and labels of your images
data = pd.DataFrame({'filepath': [], 'label': []})
for class_name in os.listdir(data_dir):
    class_dir = os.path.join(data_dir, class_name)
    file_names = os.listdir(class_dir)
    file_paths = [os.path.join(class_dir, file_name) for file_name in file_names]
    labels = [class_name] * len(file_names)
    class_data = pd.DataFrame({'filepath': file_paths, 'label': labels})
    data = pd.concat([data, class_data])

# Split the dataframe into training, validation, and testing sets
train_data, val_test_data = train_test_split(data, test_size=0.2, random_state=42)
val_data, test_data = train_test_split(val_test_data, test_size=0.5, random_state=42)

# Create an ImageDataGenerator object
datagen = ImageDataGenerator(rescale=1./255,
                             rotation_range=20,
                             width_shift_range=0.2,
                             height_shift_range=0.2,
                             shear_range=0.2,
                             zoom_range=0.2,
                             horizontal_flip=True,
                             fill_mode='nearest')

# Use flow_from_dataframe() to create separate generators for the training, validation, and testing sets
train_generator = datagen.flow_from_dataframe(dataframe=train_data,
                                              x_col='filepath',
                                              y_col='label',
                                              target_size=(224, 224),
                                              batch_size=32,
                                              class_mode='categorical')

val_generator = datagen.flow_from_dataframe(dataframe=val_data,
                                            x_col='filepath',
                                            y_col='label',
                                            target_size=(224, 224),
                                            batch_size=32,
                                            class_mode='categorical')

test_generator = datagen.flow_from_dataframe(dataframe=test_data,
                                             x_col='filepath',
                                             y_col='label',
                                             target_size=(224, 224),
                                             batch_size=32,
                                             class_mode='categorical')
```

## Make Sure To Pre-Process The Input Like What Was Done In The Pre-Trained Model
Example is found here:
```python
def preprocess(imgPath):
	# Convert all the images to size 299x299 as expected by the inception v3 model
    pilImg = preprocessing.image.load_img(imgPath, target_size=(299, 299)) 
	# Convert PIL image to numpy array of 3-dimensions
    x = preprocessing.image.img_to_array(pilImg) 
	# Add one more dimension; from (299, 299, 3) to (1, 299, 299, 3)
    x = np.expand_dims(x, axis=0) 
	# takes in (batch_size, height, width, channels), returns same dimensions, but does some preprocessing operations, like scaling values to be from -1 to 1
    x = inception_v3.preprocess_input(x) 
    return x
```

```python
# Function to encode a given image into a vector of size (2048, )
def encode(imgPath):
    imgPath = preprocess(image) # preprocess the image
    fea_vec = model_new.predict(imgPath) # Get the encoding vector for the image
    fea_vec = np.reshape(fea_vec, fea_vec.shape[1]) # reshape from (1, 2048) to (2048, )
    return fea_vec
```

which is taken from [here](https://towardsdatascience.com/image-captioning-with-keras-teaching-computers-to-describe-pictures-c88a46a311b8#:~:text=feature%20vector%20as-,follows,-%3A), and is explicitly talked about [here](<https://stackoverflow.com/questions/59305025/why-does-keras-inceptionv3-preprocess-input-and-plt-imshowimg-make-pictures-so#:~:text=The%20preprocessing%20is%20(supposed%20to%20be)%20exactly%20the%20one%20used%20to%20train%20the%20Inception%20model.%20So%2C%20if%20you%20are%20going%20to%20use%20a%20pretrained%20Inception%2C%20it%27s%20essential%20to%20have%20this%20preprocessing%2C%20otherwise%20the%20Inception%20model%20will%20have%20terrible%20performance>)

# Functional API Notes
To Remove last layer from a model:
```python
model_new = Model(model.input, model.layers[-2].output) # removing the last layer (output softmax layer for example)
```
Noting that `model.layers[-2].output` is implicitly connected to all previous layers via function calls

# Data Generation Notes
## Creating a Data Generator Function
```python
# data generator, intended to be used in a call to model.fit_generator()
def dataGenerator(imgToCaptions, imgToFeatures, wordToIdx, vocabSize, maxCaptionLength, imgsBatchSize):
    X1, X2, y = list(), list(), list()
    n=0
    # loop forever over images
    while True:
        for imgId, captions in imgToCaptions.items():
            n+=1
            imgFeatures = imgToFeatures[imgId+'.jpg'] # retrieve the image's feature vector
            for caption in captions:
                seq = [wordToIdx[word] for word in caption.split(' ') if word in wordToIdx] # encode the caption into a sequence of numbers instead of words
                for i in range(1, len(seq)): # split one sequence into multiple X, y pairs
                    inSeq, outSeq = seq[:i], seq[i] # split into input and output pair
                    inSeq = preprocessing.sequence.pad_sequences([inSeq], maxlen=maxCaptionLength)[0] # pad input sequence
                    outSeq = to_categorical([outSeq], num_classes=vocabSize)[0] # (one-hot) encodes the output sequence (note: to_categorical() is a keras-related function)
                    X1.append(imgFeatures) # store the values
                    X2.append(inSeq)
                    y.append(outSeq)
            # yield the batch data
            if n == imgsBatchSize:
                yield [[np.array(X1), np.array(X2)], np.array(y)] # "yield" saves the function's state, returns [[..]], then continues function from that statement when function is called again
                X1, X2, y = list(), list(), list()
                n=0
```

and it is called like so:

```python
epochs = 10
number_pics_per_bath = 3
steps = len(train_descriptions)//number_pics_per_batch
for i in range(epochs):
    generator = data_generator(..., ..., ..., ..., number_pics_per_batch)
    model.fit_generator(generator, epochs=1, steps_per_epoch=steps, verbose=1)
    model.save('./model_weights/model_' + str(i) + '.h5')
```

Note about `yield` keyword (source: chatGBT):

In Python, `yield` is a keyword used in generator functions. A generator function is a special type of function that can be paused in the middle of execution and resumed later from where it left off.

When a `yield` statement is encountered inside a generator function, it temporarily suspends the execution of the function and **returns the value specified in the `yield` statement**. **The state of the function is saved, and when the generator is iterated over again, execution resumes from the point where it was paused and continues until the next `yield` statement is reached**.

# Show Details About The Model

Given this structure from `model.summary()`:
![[Pasted image 20230223120308.png]]
...

![[Pasted image 20230223120620.png]]

Typing this:
```python
model.get_config()['layers'][1]['inbound_nodes']
```
will give us this:
`[[['input_3', 0, 0, {}]]]` 
while typing this:
```python
model.get_config()['layers'][-3]['inbound_nodes']
```
will give us this:
`[[['activation_273', 0, 0, {}], ['mixed9_1', 0, 0, {}], ['concatenate_5', 0, 0, {}], ['activation_281', 0, 0, {}]]]`
