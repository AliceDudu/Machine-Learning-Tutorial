学习资料：
https://www.youtube.com/watch?v=si8zZHkufRY&list=PL2-dafEMk2A7YdKv4XfKpfbTH5z6rEEj3&index=5

---

**情感分析，**
就是要识别出用户对一件事一个物或一个人的看法、态度，比如一个电影的评论，一个商品的评价，一次体验的感想等等。根据对带有情感色彩的主观性文本进行分析，识别出用户的态度，是喜欢，讨厌，还是中立。

![](http://upload-images.jianshu.io/upload_images/1667471-9f70bad300487c54.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**关于情感分析，之前有一篇 cs224d 的小项目:**
里面用 skipgram 学习出 word vector，然后用 softmax regression 进行识别：
[怎样做情感分析](http://www.jianshu.com/p/1909031bb1f2)

**今天的方法是用 20 行代码实现这个过程：**
用 tflearn.data_utils 的 pad_sequences 将 strings 转化成向量，用 tflearn.embedding 得到 word vector，再传递给 LSTM 得到 feature vector，经过全联接层后，再用一个分类器，loss 为 categorical_crossentropy

---

- 数据用 tflearn 里面预先处理好的 imdb，IMDB 是一个电影评论的数据库。

```
from __future__ import division, print_function, absolute_import
import tflearn
from tflearn.data_utils import to_categorical, pad_sequences
from tflearn.datasets import imdb
```

- path 是存储的路经，pkl 是 byte stream 格式，用这个格式在后面比较容易转换成 list 或者 tuple。
n_words 为从数据库中取出来的词个数。

```
# IMDB Dataset loading
train, test, _ = imdb.load_data(path='imdb.pkl', n_words=10000,
                                valid_portion=0.1)
trainX, trainY = train
testX, testY = test
```

- pad sequence 将 inputs 转化成矩阵形式，并用 0 补齐到最大维度，这样可以保持维度的一致性。
![](http://upload-images.jianshu.io/upload_images/1667471-742edc78eebe282f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
# Data preprocessing
# Sequence padding
trainX = pad_sequences(trainX, maxlen=100, value=0.)
testX = pad_sequences(testX, maxlen=100, value=0.)
```

- to_categorical 将 labels 转化为 01 向量

```
# Converting labels to binary vectors
trainY = to_categorical(trainY, nb_classes=2)
testY = to_categorical(testY, nb_classes=2)
```

- 输入层，batch size 设为 None，length＝100=前面的max sequence length

```
# Network building
net = tflearn.input_data([None, 100])
```

- 上一层的输出作为下一层的输入，input_dim 是前面设定的从数据库中取了多少个单词，output_dim 就是得到 embedding 向量的维度

![](http://upload-images.jianshu.io/upload_images/1667471-0e0894b83f6cb05f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


```
net = tflearn.embedding(net, input_dim=10000, output_dim=128)
```

- 模型用的 LSTM，可以保持记忆，dropout 为了减小过拟合

```
net = tflearn.lstm(net, 128, dropout=0.8)
```

- fully_connected 是指前一层的每一个神经元都和后一层的所有神经元相连，
将前面 LSTM 学习到的 feature vectors 传到全网络中，可以很轻松地学习它们的非线性组合关系
激活函数用 softmax 来得到概率值

![](http://upload-images.jianshu.io/upload_images/1667471-9c15822fecc9e8b4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
net = tflearn.fully_connected(net, 2, activation='softmax')
```

- 最后应用一个分类器，定义优化器，学习率，损失函数

```
net = tflearn.regression(net, optimizer='adam', learning_rate=0.001,
                         loss='categorical_crossentropy')

# Training
模型初始化
model = tflearn.DNN(net, tensorboard_verbose=0)

show_metric=True 可以看到过程中的准确率
model.fit(trainX, trainY, validation_set=(testX, testY), show_metric=True,
          batch_size=32)
```

---
推荐阅读
[历史技术博文链接汇总](http://blog.csdn.net/aliceyangxi1987/article/details/71911003)
也许可以找到你想要的：
[入门问题][TensorFlow][深度学习][强化学习][神经网络][机器学习][自然语言处理][聊天机器人]
