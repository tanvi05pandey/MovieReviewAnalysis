# MovieReviewAnalysis
Predictive RNN model determines whether a review is positive or negative

**Objective:**
Develop predictive RNN models that can determine, given a review, whether it is positive or negative. 

**Approach:**
I used Keras to implement the RNN models for this task.

**Methodology:**
1. Data preparation – The input data consists of 25000 reviews. There is a lot of punctuation, special characters, digits, empty spaces etc., which do not contribute anything to the model predictions and hence can be removed. I removed these from the data, changed everything to lower case and split each review based on new line character (\n). I also removed stop words from the reviews (however, my final submission does not include this as I got better F1 score with the stop words). I changed the label encoding from -1,1 to 0,1. Then, using Keras’ Tokenizer, I tokenized the reviews, converted them to sequences. I used a maximum length of 500 words for input features and padded the reviews that were shorter. After that I split the data into training and validation sets (80% training and 20% validation).
2. Model creation and training – I experimented with 3 different implementations using – LSTM, Bidirectional and GRU layers. Each model’s hyperparameters are shown below-

**GRU (best performance):**
- dropout=0.6 
- activation='softmax'
- optimizer = rmsprop 
- loss='categorical_crossentropy' 
- epochs=10
- hidden units=20

**LSTM layer:**
- dropout=0.5 
- activation='softmax'
- optimizer = Adam 
- loss='categorical_crossentropy' 
- epochs=10
- hidden units=15

**Bidirectional layer with LSTM:**
- dropout=0.6 
- activation='softmax'
- optimizer = rmsprop 
- loss='categorical_crossentropy’ 
- epochs=10
- hidden units=20

3. Architecture:
I have implemented Keras Sequential model and stacked layers. LSTM layers (as well as all other RNN layers) can take several arguments but the ones that I defined are 15 which is the number of hidden units within the layer and the dropout rate of the layer. There are several other arguments to pass but for this assignment, these settings achieved good results. In my LSTM, Bidirectional and GRU experiments, I’m stacking a Dense layer with two output units that would be the two possible classes of the dataset. To make probabilistic outputs, I’m using ‘softmax’ as activation function in the final layer. When compiling the model, I experimented with Adam and RMSprop optimizer with their default learning rates. I got better results with RMSprop and that is what I used in my final submission. As loss function, I use categorical_crossentropy for the classification task at hand. Finally, I’m using checkpoints to save the best model achieved in the training process. Then I use model.fit to complete training iterations.

4. Training/Val accuracy and loss:
Below are the accuracy and loss graph of my experiments. Note that my model preforms better when I do not remove stop words vs after removal. My final submission consists of a model that does not have any stop words removed.
In most cases, training for 5-10 epochs was sufficient without overfitting and prevent high variance.

<img width="666" alt="image" src="https://user-images.githubusercontent.com/4620848/187345600-8f13ccb8-5291-43f4-9f1e-9549d4895195.png">
<img width="688" alt="image" src="https://user-images.githubusercontent.com/4620848/187345657-ac260717-97c4-494f-bc69-5545afeee416.png">
