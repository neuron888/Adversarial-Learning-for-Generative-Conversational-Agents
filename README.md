# Adversarial Learning for Generative Conversational Agents
This repository contains a new adversarial training method for the Generative Conversational Agent (GCA) presented here: https://github.com/oswaldoludwig/Seq2seq-Chatbot-for-Keras

Further details on this new training method can be found in the paper: Oswaldo Ludwig, "End-to-end Adversarial Learning for Generative Conversational Agents", arXiv:1711.10122 [cs.CL], Nov 2017. In the case of publication using ideas or pieces of code from this repository, please kindly cite this paper.

Our method assumes the GCA as a generator that aims at fooling a discriminator that labels dialogues as human-generated or machine-generated. In our approach, the discriminator performs token-level classification, i.e. it indicates whether the current token was generated by humans or machines. To do so, the discriminator also receives the context utterances (the dialogue history) and the incomplete answer up to the current token as input. This new approach makes possible the end-to-end training by backpropagation. A self-conversation process enables to produce a set of generated data with more diversity for the adversarial training. This approach improves the performance on questions not related to the training data.

The trained model available here used a dataset collected from dialogues of English courses online, available here: https://www.dropbox.com/sh/o0rze9dulwmon8b/AAA6g6QoKM8hBEHGst6W4JGDa?dl=0 

Our GCA model can be explained by the following flowchart:

![alt tag](https://github.com/oswaldoludwig/Adversarial-Learning-for-Generative-Conversational-Agents/blob/master/model_graph.png)

while the following pseudocode explains the baseline algorithm (teacher forcing):

![alt tag](https://github.com/oswaldoludwig/Adversarial-Learning-for-Generative-Conversational-Agents/blob/master/Algorithm.png)

Our new end-to-end adversarial training can be explained by the following Keras model, which is composed by the generator and the discriminator. The yellow blocks belong to the GCA (the generator), while the green blocks belong to the discriminator. The white blocks are shared between generator and discriminator:

![alt tag](https://github.com/oswaldoludwig/Adversarial-Learning-for-Generative-Conversational-Agents/blob/master/model_GAN.png)

while the following pseudocode explains the new algorithm (see the paper for the definition of the variables):

![alt tag](https://github.com/oswaldoludwig/Adversarial-Learning-for-Generative-Conversational-Agents/blob/master/Algorithm_GAN.png)

**To chat with the pre-trained models:**

1. Download the python file "conversation_GAN.py", the vocabulary file "vocabulary_movie", and the net weights "my_model_weights20.h5" (trained by teacher forcing) and "my_model_weights.h5" (trained by the new adversarial method), which can be found here: https://www.dropbox.com/sh/o0rze9dulwmon8b/AAA6g6QoKM8hBEHGst6W4JGDa?dl=0 ;
2. Run conversation_GAN.py.

**To evaluate dialog lines using the pre-trained discriminator:**

1. Download the python file "run_discriminator_GAN.py", the vocabulary file "vocabulary_movie", and the net weights of the discriminator "my_model_weights_discriminator.h5", which can be found here: https://www.dropbox.com/sh/o0rze9dulwmon8b/AAA6g6QoKM8hBEHGst6W4JGDa?dl=0 ;
2. Run run_discriminator_GAN.py.
 
**To train end-to-end using the new adversarial method:**

1. Download all the files in https://www.dropbox.com/sh/o0rze9dulwmon8b/AAA6g6QoKM8hBEHGst6W4JGDa?dl=0 ;
2. Download the Glove folder 'glove.6B' and include this folder in the directory of the chatbot (you can find this folder here https://nlp.stanford.edu/projects/glove/). This algorithm applies transfer learning by using a pre-trained word embedding;
3. Run GAN_train_script.py. This script is self-explained and summarizes the new adversarial training. If you want to train on your own data, include it in the files "context_simple" and "answers_simple" following the same pattern. As can be seen in the script, I am using Theano backend and GPU, a few modifications are required to run it with TensorFlow backend.

If you want to start the adversarial training from the scratch, make the weight file my_model_weights.h5 (pre-trained the new adversarial method) equal to my_model_weights20.h5 (pre-trained by teacher forcing) and run train_script.py.

