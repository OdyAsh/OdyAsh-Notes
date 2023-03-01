# General Tips
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
