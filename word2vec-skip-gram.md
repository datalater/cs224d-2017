
ⓒ JMC 2017

---

## Word2Vec Tutorial - Skip-Gram Model

Source : http://mccormickml.com/2016/04/19/word2vec-tutorial-the-skip-gram-model/

**The Model**:

+ hidden layer 1개를 가진 neural network를 train한다.
+ hidden layer의 학습된 weights가 곧 "word vectors"이다.

**The Fake Task**:

+ neural network가 수행할 "fake" task에 대해 먼저 이야기한다.
+ 문장 중간에 있는 특정 단어가 input word로 주어졌을 때, input word 주변에 어떤 단어들이 있는지 살펴보고 랜덤으로 하나를 선택한다.
+ network는 데이터셋에 있는 모든 단어가 input word의 "nearby word"가 될 확률을 알려준다.
+ output probabilities는 각 단어가 input word 주변에 있을 가능성을 알려준다.

**Model Details**:

+ training documents에 unique word(vocabulary)가 10,000개 있다고 해보자.
+ input word "ants"를 one-hot vector(10,000 차원)로 나타낸다.
+ network의 output은 vocabulary에 있는 각 단어가 input word의 "nearby word"로 선택될 확률값을 가진 10,000 차원 벡터이다.

**Hidden Layer Output**:

Q. weight matrix를 lookup table이라 부르는 이유?

+ `1 by 10,000` one-hot vector와 `10,000 by 300` matrix를 곱하면, one-hot vector의 값이 "1"인 index에 해당하는 weight matrix의 row만 선택된다.

![matmul.png](images/matmul.png)

+ 위 그림에 나타나 있듯이 hidden layer는 lookup table로 쓰인다.
+ hidden layer의 output이 곧 input word의 word vector이다.

**The Output Layer**:

+ input word "ants"가 hidden layer를 거쳐서 나온 output인 `1 by 300` word vector가 output layer의 입력값으로 feed 된다.
+ output layer는 softmax regression classifier이다.
+ `1 by 300` word vector가 `300 by 10,000` output layer와 곱해진 후 softmax function을 거쳐서 0~1 사이의 확률값이 나온다. 각 확률값을 합하면 1이 된다.
+ `300 by 10,000` output layer는 `1 by 10,000` 벡터를 가진 output neuron이 300개 있는 것이다.

![output-layer-operation](images/output-layer-operation.png)

+ 위 그림은 `300 by 10,000` output layer 중 단어 "car"에 대한 neuron 하나만 나타낸 것이다.
+ 위 그림에서 softmax function을 거친 값은 intput word "ants"의 "nearby word"로 "car"가 선택될 확률값이다.

> **Note**: neural network는 input word에 상대적인 output wrod의 오프셋에 대해서는 아무것도 모른다. input word보다 이전에 등장한 단어와 이후에 등장한 단어의 확률을 다르게 학습한다. 이 함의를 이해하기 위해 training corpus에서 모든 'York'라는 단어가 'New'로 시작한다고 가정해보자. 즉, 적어도 training data에 따르면 'New'가 'York' 부근에 있을 확률은 100%이다. 그러나 'York' 부근에서 10개 단어를 무작위로 선택하면 'New'가 선택될 확률은 100%가 아니다. 근처에 있는 다른 단어 중 하나를 골랐을 수도 있기 때문이다.

**Intuition**:

`@@@resume`

---
