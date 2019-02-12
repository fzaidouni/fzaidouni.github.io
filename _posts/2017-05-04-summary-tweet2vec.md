---
title: "Summary of 'Tweet2Vec : Character-Based Distributed Representations for Social Media'"
permalink: /portfolio/2017/05/summary-tweet2vec
date: 2017-05-04
tags:
  - word2vec
  - bi-gru
  - rnn
  - lstm
  - neural-networks
  - architecture
excerpt: "Tweet2Vec, 2016 is a character composition model, which aims to find the vector space representations of whole tweets analogous to the popular paper by Mikolov et. al, Word2Vec, 2013"
---

#### Authors:
Bhuwan Dhingra, Zhong Zhou, Dylan Fitzpatrick, Michael Muehl & William W. Cohen

---
### Summary
[**Tweet2Vec, 2016**][1] is a character composition model, which aims to find the vector space representations of whole tweets analogous to the popular paper by Mikolov et. al, [**Word2Vec, 2013**][2]. By learning the non-local dependencies in character sequences, the authors aim to build a **Hashtag Recommendation System** for Microblogging platforms. The authors were kind enough to share there implementation, which you can find [here][4].

#### It highlights the following issues with Neural Network Language Models (NNLMs):
1. Traditional NNLMs treat words as the basic unit of language which cannot generalize the out of vocabulary words at test time.
2. Forming a dataset of words requires extensive memory for vocabulary and large dataset for training, which is practically not possible in a noisy environment like twitter.
3. It refers to [**(Ling et. al, 2015)**][3] which raises the issue that it is not sensible for each word type to have the same number of parameters. **Eg.** The word *banana*, in general would only refer to the fruit whereas the word *board* can be used to refer a whiteboard, the board of directors of a company, as well as to refer the act of boarding a ship. Judging them with the same number of parameters is not justified.

---

### Model Description
The authors use a **Bi-Directional Gated Recurrent Unit (Bi-GRU)** as the basis of the model. I think that giving preference to a Bi-GRU over a Bi-LSTM was based on results than any theoretical principles. The input to the network is a stream of characters of the tweet each of which is represented by a $$1 \times |C|$$ encoding where $$C$$ is our vocabulary (The characters used in the whole dataset). Theses one-hot encoded vectors are transformed into a dense vector representation using a character lookup table $$P_c \in \mathbb{R}^{|C| \times d_c}$$ where $$d_c$$ is a hyperparameter describing the size of the character embedding. We'll learn the parameters in the matrix $$P_c$$ during the training process.

Each of the GRU units process these vectors sequentially. The final hidden state in both the directions is used to calculate the final tweet embedding $$e_t$$. Any success this model has for using an RNN is due to the fact that the microblog posts are small in length and the hidden state can capture the essence of the whole sentence.

Considering $$x_1, x_2, .... x_m$$ be the set of sequence of vectors that are fed to the NN, which will generate the hidden states: $$h_1, h2, ..., h_m$$. The GRU process an input $$x_t$$ as follows:
\\[r_t = \sigma(W_r x_t + U_r h_{t-1} + b_r)\\]
\\[z_t = \sigma(W_z x_t + U_z h_{t-1} + b_z)\\]
\\[ \tilde{h_t} = \tanh(W_h x_t + U_h (r_t \odot h_{t-1}) + b_h)\\]
\\[h_t = (1-z_t) \odot h_{t-1} + z_t \odot \tilde{h_t} \\]
where the $$\odot$$ represents the element-wise multiplication (Hamadard Product), $$x_t \in \mathbb{R}^{d_c \times 1}$$, $$W_r, W_z, W_h \in \mathbb{R}^{d^h \times d_c}$$, $$U_r, U_z, U_h \in \mathbb{R}^{d_h \times d_h}$$ where $$d_h$$ is the hidden state dimension.
The final hidden state from the forward pass is $$h^f_m$$ and the final hidden state from the backward pass is $$h^b_0$$. These are combined to give the final embedding as:
\\[ e_t = W^f h^f_m + W^b h^b_0 + b\\]
where $$W^f, W_b \in \mathbb{R}^{d_t \times d_h}$$

##### NOTE: I added the bias term, $$b \in d_t \times 1$$ which is not mentioned in the equation written in the paper.

The tweet embeddings are then fed to a linear layer of softmax with $$L$$ outputs (The number of posssible hashtags from the model.) The output is given by:
\\[ P(y = j|e) = \dfrac{exp(w_j^T e + b_j)}{\sum_{i=1}^L exp(w_i^T e + b_i)}\\]
where $$w_i$$ is a vector representing the weights of the $$i^{th}$$ hashtag and $$b \in L \times 1$$ is the vector representing the bias w.r.t to each of the $$L$$ hashtags.

The objective function is defined as categorical cross entropy loss between the predicted and true hashtags:
\\[ J = \dfrac{1}{B} \sum_{i=1}^B \sum_{j=1}^{L} -t_{i,j}\log(p(i, j)) + \lambda ||\Theta||^{2}\\]
Here, $$B$$ is the Batch size of the tweet embeddings, $$p(i,j)$$ is the probability calculated by the softmax for the $$i^{th}$$ tweet in the batch and $$j^{th}$$ hashtag class. The L-2 regularization is weighted by $$\lambda$$ over the parameters of the linear layer.

[1]: https://arxiv.org/abs/1605.03481
[2]: https://arxiv.org/abs/1301.3781
[3]: https://arxiv.org/abs/1508.02096
[4]: https://github.com/bdhingra/tweet2vec
