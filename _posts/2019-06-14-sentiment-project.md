---
layout: post
title:  "Sentiment Analysis Project Overview"
date:   2019-06-14 15:08:59 -0400
description: "topics on deep learning"
author: "Khaing Win"
---


#Project overview
In this project, I constructed a recurrent neural network (RNN) for the purpose of determining the sentiment of a review using the IMDB movie dataset. The model was created using `Amazon's SageMaker` service. This model is then deployed and a simple web app is created which then interacts with the deployed model. Although the model was trained on movie reviews, the testing worked well on any kind of reviews.

##Project Rationale:

### Why use a RNN? Why not a typical feedforward neural network? 
>Human language is composed of *sequence* of words, and the next word depends on the previous words in a sentence. When dealing with sequential information, RNN is more accurate.

>Here, I used a dataset of movie reviews, accompanied by sentiment labels, whether the review is positive or negative.

##High-level approach

>***First, we'll pass in words (which are our inputs) to an embedding layer.***

- Word embeddings work better than one-hot encoding since it's more efficient. Think about it: we have tens of thousands of words, we'll need a more efficient representation for our input data. That's why we need an embedding layer than one-hot encoded vectors.

- We can actually train an embedding with the `Skip-gram Word2Vec model` and use those embeddings as input. However, we are just going to use an embedding layer and let our network learn a different embedding table on its own. 

*In this case, the embedding layer is for the purpose of dimensionality reduction, rather than for learning semantic representations.*

>**After input words are passed to an embedding layer, the new embeddings will be passed to LSTM cells.**

- The LSTM cells will add *recurrent* connections to the network.

- This will give us the ability to include information about the *sequence* of words in the movie review data.

>**Finally, the LSTM outputs will go to a sigmoid output layer.**

- Positive review is labeled as `1` and negative review is labeled as `0`.
- A sigmoid function will output predicted, sentiment values between `0`-`1`.
