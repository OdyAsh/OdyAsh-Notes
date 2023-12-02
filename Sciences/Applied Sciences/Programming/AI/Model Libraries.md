
# PyTorch

## Lightning 

### Implementation Tips

#### When Designing `YourModel(pl.LightningModule)`
##### `__init__()`

```python
def __init__(self, the_device='cuda', , num_classes=10, dummy_input_size=(32,3,306,306)):
	super().__init__()
	self.conv1 = nn.Conv2d(1, 32, kernel_size=3, padding=1)
	...
	self.fc2 = nn.LazyLinear(10)
	
	# useful for writing computational graph in tensorboard, summary(), etc
	self.example_input_array = torch.randn(*dummy_input_size) 

	self.the_device = the_device

	def _create_metric_func(metric_type:str):
		if 'acc' in metric_type.lower():
			return torchmetrics.Accuracy(task='multiclass', 
										 num_classes=num_classes, 
										 average="micro").to(the_device)
		elif 'f1' in metric_type.lower():
			return torchmetrics.F1Score(task="multiclass", 
										num_classes=num_classes, 
										average=None).to(the_device)
	
	# for calculating metric of a step
	self.acc_step_funcs = [_create_metric_func('acc') for _ in range(3)] # for computing train, val, test results respectively
	self.f1_score_step_funcs = [_create_metric_func('f1') for _ in range(3)]
	# for calculating metric of an epoch
	self.acc_epoch_funcs = [_create_metric_func('acc') for _ in range(3)]
	self.f1_score_epoch_funcs = [_create_metric_func('f1') for _ in range(3)]
        
	self.metrics_history = {
		# per epoch
		'loss':[],
		'acc':[],
		'f1_score':[],
		'val_loss':[],
		'val_acc':[],
		'val_f1_score':[],
		'test_loss':[],
		'test_acc':[],
		'test_f1_score':[],
		# per step
		'step_loss':[],
		'step_acc':[],
		'step_f1_score':[],
		'val_step_loss':[],
		'val_step_acc':[],
		'val_step_f1_score':[],
		'test_step_loss':[],
		'test_step_acc':[],
		'test_step_f1_score':[],
        }
```

##### `training_step()` & `training_epoch_end()`
```python
def training_step(self, batch, batch_idx):
	x, y_true = batch
	y_pred = self(x)
	loss, acc, f1_score = self._step_logic(y_pred, y_true, prefix='')
	return {'loss':loss, 'acc':acc, 'f1_score':f1_score}
```
same for `validation_step()` / `test_step()` but change to `prefix='_val'`  / `prefix='_test'`

```python
def training_epoch_end(self, outs): -> None # almost same for validation_step()
	# 'outs' argument here contains values from what was returned from training_step()
	_,_,_ = self._epoch_end_logic(outs, prefix=''/'val') 
```
same for `validation_epoch_end()` / `test_epoch_end()` but change to `prefix='_val'`  / `prefix='_test'`

handlers:

```python
def _store_metric(self, metric_name, metric_val):
	try:
		self.log(metric_name, metric_val)
	except Exception as e:
		# then metric_val is not scalar, then this means:
		# metric_name is an f1 score metric 
		# so, we just take the mean value
		self.log(metric_name, metric_val.mean())
	# putting this here ensures we don't include the mean of f1 score, 
	# but rather the tensor of shape (1, num_classes)
	self.metrics_history[metric_name].append(metric_val)
```

```python
def _step_logic(self, y_pred, y_true, prefix=''):
	if 'val' in prefix:
		func_idx = 1
	elif 'test' in prefix:
		func_idx = 2
	else:
		func_idx = 0
	
	# log step metrics
	loss = F.cross_entropy(y_pred, y_true)
	self._store_metric(f'{prefix}step_loss', loss)

	acc = self.acc_step_funcs[func_idx](y_pred, y_true)
	self._store_metric(f'{prefix}step_acc', acc)
	self.acc_epoch_funcs[func_idx].update(y_pred, y_true)

	f1_score = self.f1_score_step_funcs[func_idx](y_pred, y_true)
	self._store_metric(f'{prefix}step_f1_score', f1_score)
	self.f1_score_epoch_funcs[func_idx].update(y_pred, y_true)

	return loss, acc, f1_score
```

```python
def _epoch_end_logic(self, outs, prefix=''):
	if 'val' in prefix:
		func_idx = 1
	elif 'test' in prefix:
		func_idx = 2
	else:
		func_idx = 0

	# log epoch metrics
	loss_epoch = torch.tensor([x[f'{prefix}loss'] for x in outs], dtype=float, device=self.the_device).mean()
	self._store_metric(f'{prefix}loss', loss_epoch)

	acc_epoch = self.acc_epoch_funcs[func_idx].compute()
	self.acc_epoch_funcs[func_idx].reset()
	self._store_metric(f'{prefix}acc', acc_epoch)

	f1_score_epoch = self.f1_score_epoch_funcs[func_idx].compute()
	self.f1_score_epoch_funcs[func_idx].reset()
	self._store_metric(f'{prefix}f1_score', f1_score_epoch)

	return loss_epoch, acc_epoch, f1_score_epoch
```

side note 1: I'm guessing the code above is similar to how TF deals with metrics under the hood ([source](https://www.tensorflow.org/guide/keras/writing_a_training_loop_from_scratch#:~:text=Here%27s%20our%20training%20%26%20evaluation%20loop))

side note 2: you can avoid writing the `xx_epoch_funcs` and do the following in `_epoch_end_logic()`:
```python
acc_epoch = torch.tensor([x[f'{prefix}acc'] for x in outs], dtype=float, device=self.the_device).mean()

f1_score_epoch = torch.stack([x[f'{prefix}f1_score'] for x in outs], dim=0).mean(dim=0)
```

However, this is not advised because of the following:
we are using `.mean(dim=0)` on f1_score of all steps in an epoch, this could lead to misleading results if there are a lot of steps (i.e., batches) that don't include a minority class(es), as their f1 score will be 0 by default, so that will affect the overall average. Summary: This approach is logically different than the approach presented above, but if you insist on using it, at least try to make your dataloader get samples of all classes in each batch, increase batch size, or use accumulated gradients logic in order to increase batch size (but that has to reflect on your code (training_step(), etc) as well).

##### `configure_optimizers()`
```python
def configure_optimizers(self):
	return torch.optim.Adam(self.parameters(), lr=1e-3)
```

#### `pl.Trainer()`

set this `num_sanity_val_steps=0` (default: 2) if you're planning to use an internal history dictionary (e.g., `self.metrics_history` in the code above), otherwise, it will have an additional value for each metric at the start of the lists due to the sanity validation steps that were run.

#### Getting A `history` Dictionary Similar To That in TF

1. follow [[Model Libraries#When Designing YourModel pl LightningModule|these]] steps
2. train the model
3. run the following:
```python
history = trainer.model.metrics_history.copy()
for metric, tensors_list in history.items():
    if isinstance(tensors_list, list) and len(tensors_list) > 0 and isinstance(tensors_list[0], torch.Tensor):
        history[metric] = np.array([np.array(tens.detach().cpu()) for tens in tensors_list]).round(5)
```

## TorchMetrics

Useful snippets to understand how the code works:

``` python
import torchmetrics
import torch
ff = torchmetrics.F1Score('multiclass', num_classes=3, average=None, top_k=1, threshold=0.5)
ff(torch.tensor([[.2, .70001, .70002], [.2, .7001, .7000]]), torch.tensor([2, 2]))
# output: tensor([0.0000, 0.0000, 0.6667])
```

``` python
import torchmetrics
import torch
ff = torchmetrics.Accuracy('multiclass', num_classes=3, average=None, top_k=1, threshold=0.5)
ff.update(torch.tensor([[.2, .70001, .70002]]), torch.tensor([2]))
ff.update(torch.tensor([[.7005, .7001, .7002]]), torch.tensor([2]))
ff.update(torch.tensor([[.2, .7003, .7002]]), torch.tensor([1]))
res = ff.compute()
ff.reset()
res
# output: tensor([0.0000, 1.0000, 0.5000])
# when using average='micro', the output: tensor(0.6667) (as 2 correct preds / 3 all preds = 0.6667)
# when using average='macro', the output: tensor(0.5000) (as (0+1+0.5)/3 = 0.5)
```

## Debugging

### `torch.cuda.is_available()` Returns `False`

1. make sure the steps [here](https://stackoverflow.com/questions/60987997/why-torch-cuda-is-available-returns-false-even-after-installing-pytorch-with#:~:text=How%20to%20check%20if%20your%20GPU/graphics,with%20support%20for%20the%20newer%20compute%20capabilities.) apply
2. What worked for me personally (if you want to install using conda/mamba): don't install from the generated conda command in [this](https://pytorch.org/get-started/locally/#:~:text=Compute%20Platform-,Run%20this%20Command,-%3A) webpage. Instead, use the following command ([source](https://pytorch.org/get-started/previous-versions/#:~:text=conda%20install%20pytorch%3D%3D1.13.1%20torchvision%3D%3D0.14.1%20torchaudio%3D%3D0.13.1%20%2Dc%20pytorch)) (side note: if you want to use PyTorch Lightning, then conda install it first):
`conda install pytorch==x.x.x torchvision torchaudio -c pytorch`

verify by running this block (`cudnn` is optional I believe, but you should [[../Python/Virtual Environments/Conda Environment#Installing CUDA|get it]]):
``` python
import torch
print(torch.__version__)
print(torch.version.cuda)
print(torch.backends.cudnn.version())
print(torch.cuda.get_device_name(0))
print(torch.cuda.get_device_properties(0))
print(torch.cuda.is_available())
x = torch.randn(1, 3, 224, 224, device='cuda')
conv = torch.nn.Conv2d(3, 3, 3).cuda()

out = conv(x)
print(out.shape)
```

Ok, but why is this the case? Because from what I understand, the PyTorch packages supplied by the generated conda command or by PyTorch Lightning are both for CPU usage, not GPU, and you can check this by running `conda list` and seeing that besides `pytorch` , you'll see a build similar to this: `cpu_py39h5e1f01c_1`, but when running the command in step 2., you'll see the build similar to this: `py3.9_cuda11.8_cudnn8_0`

Side note: I believe `pytorch` and `torch` packages are the same (just different package names for compatibility reasons).

#### `OSError: [WinError 182] The operating system cannot run %1. Error loading "...nvfuser_codegen.dll" or one of its dependencies.`

Fix for me: import torch first, then tensorflow/keras. In other words:
```python
import numpy as np
import torch # torch
first
import keras # then keras/tf, to avoid OSError
import tensorflow as tf
np.random.seed(42)
torch.manual_seed(42)
import html
from bs4 import BeautifulSoup
```

## PyTorch Vs PyTorch Lightning

PyTorch:
![[Attachments - Model Libraries/Pasted image 20230503065504.png|250]]
Example implementation:
![[Attachments - Model Libraries/Pasted image 20230503070424.png]]

PyTorch Lightning:
![[Attachments - Model Libraries/Pasted image 20230503065442.png]]
Example Implementation:
![[Attachments - Model Libraries/Pasted image 20230503070708.png]]

![[Attachments - Model Libraries/Pasted image 20230503070749.png]]

Which is this:

![[Attachments - Model Libraries/Pasted image 20230503070759.png]]

Final look:
![[Attachments - Model Libraries/Pasted image 20230503070942.png]]

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



# TensorFlow

## Debugging

### `AlreadyExistsError: Another metric with the same name already exists.` 

Problem for me: these libraries:
```
 + keras-base           2.7.0  py_0    esri/noarch     Cached
  + tensorflow-addons   0.15.0  py39_8  esri/win-64     Cached
  + typeguard           2.13.0  py_1    esri/noarch     Cached
```
solution: install using pip, not conda

### `model.predict()` Runs Forever 

In newer versions of TF, when you provide a Sequential Data Generator to `model.predict()`, make sure to provide the `steps=st` argument, where:
`st = num_of_samples_in_generator // batch_size` 
Note: `st` means number of steps (i.e., batches) in a single epoch)

## Tips

### Loading Models

if a model has custom metrics, then use this syntax:
`keras.models.load_model(f'models/{model_file_name}.h5', custom_objects={"F1Score": F1Score })`
Where `"F1Score"` is replaced with the metric name that you see (you can check it by receiving an error by running false code), and `F1Score` is the name of the function (i.e., metric) that you previously defined in your code.

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

### Using `flow_from_directory()` and CSV method

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

### Make Sure To Pre-Process The Input Like What Was Done In The Pre-Trained Model
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

## Installation Notes
(Quick note: if you're planning to use GPU, you have to make sure you have the CUDA/cudnn support on your platform that are compatible with the TF version that you will install based on the two options below, you can check more about how to get CUDA/cudnn [[../Python/Virtual Environments/Conda Environment#Installing CUDA|here]])

([source](https://stackoverflow.com/questions/41402409/tensorflow-doesnt-seem-to-see-my-gpu?answertab=modifieddesc#tab-top:~:text=conda%20install%20tensorflow%3D2*%3Dgpu*))
run this command in CMD while in a conda/mamba activated environment:
`mamba install tensorflow=2*=gpu*`
To ensure the version of TF you get has GPU compatibility and is compatible with the rest of your environment.

If the method above is not an option, then you need to be aware that TF 2.10 is the last version that natively supports GPU ([source](https://stackoverflow.com/questions/41402409/tensorflow-doesnt-seem-to-see-my-gpu?answertab=modifieddesc#tab-top:~:text=Caution%3A%20TensorFlow%202.10%20was%20the%20last%20TensorFlow%20release%20that%20supported%20GPU%20on%20native%2DWindows.%20Starting%20with%20TensorFlow%202.11%2C%20you%20will%20need%20to%20install%20TensorFlow%20in%20WSL2%2C%20or%20install%20tensorflow%2Dcpu%20and%2C%20optionally%2C%20try%20the%20TensorFlow%2DDirectML%2DPlugin)), so try to install that version using:
`mamba install tensorflow=2.10.0` then install `cudatoolkit` with a version suitable to it
# Functional API Notes
To Remove last layer from a model:
```python
model_new = Model(model.input, model.layers[-2].output) # removing the last layer (output softmax layer for example)
```
Noting that `model.layers[-2].output` is implicitly connected to all previous layers via function calls

## Data Generation Notes
### Creating a Data Generator Function
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

## Show Details About The Model

Given this structure from `model.summary()`:
![[Attachments - Model Libraries/Pasted image 20230223120308.png]]
...

![[Attachments - Model Libraries/Pasted image 20230223120620.png]]

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

# Code in The Wild
`summary_writer.add_image(caption, transforms.ToTensor()(real_im), epoch)`
in [here](https://github.com/nocholasrift/image-caption-geo/blob/master/Project_Notebooks/Image_Geolocation.ipynb).

