2025-02-11 19:01

Status:

Tags: [[Intelligence Interactive Systems]]

---

## Summary:

Supervised learning involves training models using labelled data to perform tasks such as classification and regression.

##### Topics Included:

- Classification
- Comparing Classifiers
- Conventional Neural networks (CNNs)
- Recurrent Neural Networks (RNNs)
- Long Short-Term Memory (LSTM)

### Supervised Learning

Machine learning is the science of learning from data to perform a task without it being specifically explained using past experience, against data and a performance metric to improve.

**Supervised Learning** uses training data with desired solution called labels, with data.

Aspects of Supervised learning:

**Regression Models**: Used for continuous labels
**Classification Models**: Used for discreate labels

Application of Supervised Learning:
- Speech Recognition
- NL Understanding
- Sentiment Analysis
- Image recognition.
### Classification

**Classifies problems into different groups**. Uses a set of test data with measurements for many different features/dimensions as well as a **label** with the goal being to get new data without a label and classify/identify it it.

An example of a simple classification algorithm is **Simple Linear Classifier** or simply drawing a line to divide data points

### Measurement of Classification Algorithms

Different classification algorithms can be used for different applications.

Measurements include:
- **Predictive Accuracy**: How accurate the Module is.
- **Speed and Scalability of Model**: Performance both in terms of time and space requirements needed for model
- **Robustness**: How effective it is during errors e.g.
	- Handling of noise/error input
	- Works with missing features/values
	- Handling of unnecessary features.
- **Helpfulness of interpretations**: how useful the model is for the end goal.

### Accuracy Calculations.

Accuracy is fundamentally calculated with

$\text{Accuracy} = \frac{\text{No. Correct Classifications}}{\text{No. Incorrect Classifications}}$

This can be further defined into 4 specific categories:

![[image-17.png]]

- **Accuracy** Proportion of correctly classified instances
- **Precision** or Trustworthiness of Positive predictions
- **Recall** or How many were accurately considered positive
- **F1 Score** or Harmonic mean of precision and recall

Where:
- TP = True Positive
- TN = True Negative
- FP =  False Positive
- FN = False Negative

### Process for Measuring Accuracy of SL Algorithms

K-Fold Cross validation is used to measure Predictive accuracy, to evaluate Performance.

Method:
1. Split Data into K sets
2. 1 segment is validation and k-1 segments being training.
3. Do training with a specific algorithm
4. Repeat from Step 2 K times, with each eventually being a segment.
5. Repeat from beginning with different algorithm

Use simpler model, for algorithms with same accuracy. 

### Underfitting Vs Overfitting

![[image-19.png]]

Description of model based on training and testing performance
- **Underfitting** is when training performance is poor
- **Overfitting** is when training performance is good but testing is poor.

### Supervise Learning Workflow

Data is split into 3 sets:

**Training Set**: To train the model
**Testing Set**: Assessing Model Performance (Typically 20%)
**Validation Set**: To tweak and choose among many prediction functions

### Conventional Neural Network

Special type of neural network that has learnable parameters like weights and biases.

Application:
- Image Classification
- Speech Recognition
- Object Detection

![[image-14.png]]


Comprised of 4 layers:

- **Input Layer**: Entrance for passing training data to model. Data doesn't need to be flattened into 1d vector and can be inputted as 2d vector, making capturing spatial relationships easier.
- **Conventional layer**: Extracts **features** from the input vector by using multiple learnable filters which used against the input matrix to detect presence of specific features/patterns, to then create a feature map.
- **Pooling Layer**: Reduces dimensionality of each features map whilst retaining important information. Done via types like Max Pooling or Average Pooling, dividing measurements into sections and aggregating them.
- **Fully Connected Layer**: Traditional Multilayer Perceptron, taking the reduced feature map. *Note: Fully connected means every neuron in the precious layer is connected to every neuron of the next layer.*

### Recurrent Neural Network (RNN)

CNN struggles with sequential data or time data like video frame recognition to get new data. So data that requires previous information to get the next result. Since CNN can 't store previous information, need for RNN.

Application:
- **Sentiment Analysis** :
	Input: Sequence of words
	Output: Probability of having positive sentiment
- **Machine Translation**:
	Input: Sequence of English words
	Output: Translation to French (made more accurate with greater context of previous words)
- **Music Generation**:
	Input: Sequence of Notes
	Output: Best notes to correspond to that 

![[image-16.png]]


##### How RNN works

RNN loops through the hidden layer. With each time step t, RNN processes current input xt alog with the previous hidden state ht-1. Internally it computes a hidden state ht. Therefore ht serves as memory to carry forward relevant information.

![[image-21.png]]

- Wxh and Whh are learned weight matrices
- bh is a bias vector
- σ is an activation fuctnion.

An output yt can be produced at each step by applying a second weight matrix:

![[image-22.png]]

- W hy and b y project the hidden state into the output space
- ϕ is an appropriate output activation (e.g., softmax for classification)
### Backpropagation Through Time (BPTT)

Training an RNN requires learning all weight matrices by minimizing a sequence-level loss (e.g., cross-entropy summed over all time steps). Since the hidden state depends recursively on earlier states, we “unroll” the RNN across time: each time step becomes a layer in a deep feed-forward network that shares weights across layers. We then apply standard backpropagation over this unrolled network, computing gradients of the loss with respect to each weight at every time step and summing them. This procedure is called Backpropagation Through Time (BPTT) .


As Gradient flows backwards across many time steps they can:

- Vanishing Gradients: Gradients that are too small
- Exploding gradients: Gradients that are too large

Makes it difficult to learn long-range dependencies. LSTM mitigates this.


### Long Short Term Memory (LSTM)

For the issue of long term memory and needing to weigh information from much earlier e.g. "I grew up in France ..... I speak fluent x" and figuring out what x is.

##### How LSTM Works

An LSTM cell replaces the single hidden-state update of an RNN with a series of operations that regulate information flow. It maintains two vectors at each time step:

- **Cell state** ct​: the long-term memory of the cell.
- **Hidden state** ht​: the short-term output at time t.

Four gates—each implemented as a sigmoid layer followed by element-wise multiplication—control how information moves in and out of the cell:

1. **Forget Gate**: Removes irrelevant information from previous state ct-1
2. **Store gate**: To store relevant new information into the cell state
3. **Update gate**: Selectively update cell state values
4. **Output gate**: Decides what information is sent to the next time stamp

![[image-29.png|722x395]]

*Note: Cell state represents Update gate, that updates Cell State Value*


LSTMs can preserve or discard information over arbitrarily long sequences, making them highly effective for tasks requiring long-term context such as **language modelling** and **speech recognition**.


##### Glossary
---

##### References
----
![[Supervised-learning.pdf]]