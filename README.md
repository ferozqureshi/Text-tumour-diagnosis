# Text tumour diagnosis : Comment toxicity classification

## Motivation:
&nbsp; &nbsp; Lot of hate can be spread through social media. Comments and other text based posts have a great hand in it. As a precaution, a model which can detect the hate, toxicity, and obscenity in the text is essential. The model that I posted in the following repository can be a possible solution for that. My model can be integrated alongside personal blogs, or any other social media platforms to filter out such comments.

## Dataset Description
&nbsp; &nbsp; This has series of comments as strings where We are provided with a large number of Wikipedia comments which have been labeled by human raters for toxic behavior.
<br/> &nbsp; &nbsp; We are provided with a large number of Wikipedia comments which have been labeled by human raters for toxic behavior. The types of toxicity are:

   - toxic
   - severe_toxic
   - obscene
   - threat
   - insult
   - identity_hate <br/> <br/>
 Our aim is to create a model which predicts a probability of each type of toxicity for each comment.
 
 The sample dataset looks as follows:

![alt text](https://github.com/ferozqureshi/Text-tumour-diagnosis/blob/main/head.png)


  


## Process followed in solving the problem:
&nbsp; &nbsp;1️⃣Loading in data <br/> 
&nbsp; &nbsp;2️⃣Preprocessing comments <br/> 
&nbsp; &nbsp;3️⃣Creating an RNN LSTM model <br/> 
&nbsp; &nbsp;4️⃣evaluating model performance <br/> 
&nbsp; &nbsp;5️⃣creating a gradio DL app
	
	
### 1️⃣Loading in data:
&nbsp; &nbsp;&nbsp; &nbsp;Pandas has been used to load the csv locally.
### 2️⃣Pre-processing the comments
&nbsp; &nbsp;&nbsp; &nbsp;Pre-processing is an important step when comes to NLP. Here, we need to tokenize our strings before we do anything.<br/>
&nbsp;In keras there is [TextVectorization](https://www.tensorflow.org/api_docs/python/tf/keras/layers/TextVectorization) layer which does it for us.These tokens(maps text features to integer sequences)don't actually add more value until we convert them into word embeddings.
<br/> 
&nbsp; &nbsp;&nbsp; &nbsp;I have taken the vocab dictionary in the textvectorizer to be 200,000 (max_tokens=20000)
which is a big dictionary, and I've done it to maximize the accuracy. I've taken the maximum sequence length to be 1800.

#### The pipeline that I've followed:
   - Converted slices of an array in the form of objects by using tf.Dataset.from_tensor_slices()
   - Cached the data dataset.cache()
   - Shuffled the data using dataset.shuffle()
   - Made batches of 16 data points by using dataset.batch(16)
   - To prevent bottleneck, I have done the pre-fetching using dataset.prefetch(8)

### 3️⃣Creating an RNN LSTM model
1) Firstly, I've created an Embedding layer which converts the tokens to embeddings.<br/>
2) Next, I've used LSTM (Long Short-Term Memory) bidirectional layer to fit it.<br/>
&nbsp;&nbsp;&nbsp;&nbsp;It is well known that LSTM performs better with
sequences, and sequences is what we've. <br/>
&nbsp;&nbsp;&nbsp;&nbsp;I've used tanh activation because tensorflow dictates to use tanh in specific to LSTM.
 The reason why I've used bidirectional layer is because 
 the sequences can have modifier words which changes the meaning of
of the sentence.

I've trained for 5 epochs till the losses are ; training loss:- 0.0287 , validation loss:- 0.0239 <br/>
&nbsp; &nbsp;&nbsp; &nbsp;<img src="https://github.com/ferozqureshi/Text-tumour-diagnosis/blob/main/training&validation_loss.png" height=200/>


### 4️⃣Evaluating model performance
The following metrics has been used:<br/>
   - Precison
   - Recall
   - CategoricalAccuracy <br/><br/>
   
  &nbsp;&nbsp;&nbsp;&nbsp;I've achieved these values at the end; Precision: 0.9034322500228882, Recall:0.85329669713974, Accuracy:0.49548646807670593

### 5️⃣Creating a gradio DL app
Finally, I serialized the model to h5 file
and integrated it with gradio.

Final look of Web Api: a gif...
  
