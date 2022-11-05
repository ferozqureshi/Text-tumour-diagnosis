# Text tumour diagnosis : Comment toxicity classification

## Motivation:
  Lot of hate can be spread through social media. comments and other text post has a great hand beside it. As a precaution, a model which can detect the hate, toxicity, and vulgourness in the text is essential. The model that I posted in the following repository can be a possible solution for that. My model can be integrated alongside personal blogs, or any other social media platform.

## Dataset Description

dataset comes from kaggle from jigsaw
This has series of comments as strings 
sample dataset head:
different labels as mentioned above.

We are provided with a large number of Wikipedia comments which have been labeled by human raters for toxic behavior. The types of toxicity are:

    toxic
    severe_toxic
    obscene
    threat
    insult
    identity_hate

Our aim is to create a model which predicts a probability of each type of toxicity for each comment.
  


## Process followed in solving the problem:
  	1. Loading in data
	2. Preprocessing comments 
	3. Creating a deep NLP model
	4. evaluating model performance
	5. creating a gradio DL app
### 1. Loading in data:
    Pandas has been used to load the csv locally.
### 2. Preprocessing the comments
  This is an important step when comes to NLP. 
  We need to tokenize the our strings before we do
  anything. In keras there is textVecorizer which does
  it for us.These tokens don't actually add more value,
  that is why we need to convert them into word 
  embeddings.
  TextVectorization: A preprocessing layer which maps text features
	to integer sequences.
link for documentation https://www.tensorflow.org/api_docs/python/tf/keras/layers/TextVectorization
I have taken the vocab dictionary in the vectorizer to be 200,000
which is a big dictionary, and I've done it to maximize the accuracy.
by max_tokens=20000)
I've taken the maximum sequence length to be 1800.

#### The pipeline steps that I've followed:
1) .Dataset.from_tensor_slices(X,y)
2) dataset.cache()
3) dataset.shuffle() buffersize
4)dataset.batch(16)
5)dataset.prefetch(8)  helps prevents bottlenecks
-- to squeeze the juice out of my gpu

### 3) Creating a deep NLP model
1) Embedding layer - converts the tokens to embeddings
2)LSTM bidirectional layer ( I've used tanh activation,
I'd 've used relu, but tensorflow dictates to use tanh in specific)
 the reason why I've used bidirectional layer is because 
 the sequences can have modifier words which changes the meaning of
of the sentence.

trained till the losses; training loss:-  , validation loss:-

LSTM, it is well known that LSTM performs better withh 
sequences, and sequences is what we've.

### 4. evaluating model performance
	Precison
	Recall
	CategoricalAccuracy
   - make a note of all metrics

Finally, serialize the model to h5 file (.h5 format uses?)
and integrate it with gradio ( gradio has been lightweight and
powerful)

Final look of Web Api: a gif...
  
