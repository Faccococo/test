### GRU model

#### introduce

GRU(Gated Recurrent Unit) is a kind of Recurrent Neural Network. aiming to solve the vanishing gradients and short-term memory problem where traditional RNNs often exists.

GRU is first introduced by Cho, Kyunghyun's group in "On the Properties of Neural Machine Translation: Encoder-Decoder Approaches"(2014). GRU's fundamental concept is to utilize a gating mechanism to regulate the information flow through the network. Two gates—an update gate and a reset gate—make up the gating system. The reset gate determines how much of the previous hidden state should be forgotten, while the update gate determines how much of the hidden state should be carried over to the current time step.

Both the reset gate and the update gate are sigmoid gates, producing values between 0 and 1. The final hidden state is created by combining the input at the current time step with the intermediate hidden state computed using the output of the update gate and reset gate.

Machine translation, speech recognition, and text synthesis are just a few of the sequence modeling tasks for which the GRU has been proven to be effective. GRU contains fewer parameters than other RNNs like LSTM, which makes it quicker and simpler to train.



Here is the steps of using GRU to processing reported numbers.

First, we convert the data to a proper format. Since GRU is a kind of supervision machine learning algorithm, a training data with time sequencial format is needed to train the model. In a single row of a srquencial format data, label as a give time point and features at a specific "time step" before the point of label is included. As an optimize way, regularization is used to avoid overfitting. Loss function will be like as following formular:

$$
\sum_{i=1}^n loss(y_i,f(x_i))+C*R(f)
$$
 Where $loss$ is the origin loss function, $C$ and $R(f)$ is the regular element to convert data into a spefic  interval.

Then, we need to train GRU. Optimizer used in this project is Adam. An pseudo code of Adam is list below:

![image-20230221022958553](C:\Users\Zitong\AppData\Roaming\Typora\typora-user-images\image-20230221022958553.png)

 Here we use the adam implecation in Tensorflow.

公式（带说明）

![image-20230221015014520](C:\Users\Zitong\AppData\Roaming\Typora\typora-user-images\image-20230221015014520.png)

where U projects the input into a hidden space.

![image-20230221015052004](C:\Users\Zitong\AppData\Roaming\Typora\typora-user-images\image-20230221015052004.png)

图片



分析



We divide 20% percent of total data as test part. By using data of test dataset as model input, we can evaluate the accuracy more precisely since model input is not a infect factor. After training, the prediction of model is figured out below:

//此处插入图片





敏感性分析

