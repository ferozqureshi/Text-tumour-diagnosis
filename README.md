# Text tumour diagnosis : Comment toxicity classification

Motivation:
  Lot of hate can be spread through social media. comments and other text post has a great hand beside it. As a precaution, a model which can detect the hate, toxicity, and vulgourness in the text is essential. The model that I posted in the following repository can be a possible solution for that. My model can be integrated alongside personal blogs, or any other social media platform.

Dataset Description

We are provided with a large number of Wikipedia comments which have been labeled by human raters for toxic behavior. The types of toxicity are:

    toxic
    severe_toxic
    obscene
    threat
    insult
    identity_hate

Our aim is to create a model which predicts a probability of each type of toxicity for each comment.
  


Process followed in solving the problem:
  1. Loading in data
	2. Preprocessing comments 
	3. Creating a deep NLP model
	4. evaluating model performance
	5. creating a gradio DL app
