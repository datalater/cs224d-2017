
ⓒ JMC 2017

---

## L02 Word Vector Representation

### 01 단어의 의미 재현하기

**단어간의 유사성을 어떻게 측정할 수 있을까**.

단어의 의미는 함께 쓰이는 단어를 보면 알 수 있다.

1. government debt problems turning into **banking** crises as happend in
2. saying that Europe needs unified **banking** regulation to replace the hodgepodge

단어 banking의 의미를 알기 위해서 banking이 쓰인 수천 개 문장을 찾고, 각 문장을 살펴본다.
가령, 위 2가지 문장을 보면 debt problems, governments, regulation, Europe, saying unified 등이 있다.
banking과 함께 쓰이는 모든 단어들의 개수를 카운팅한다.
함께 쓰이는 단어들은 banking의 의미를 represent하는 context words로 사용할 수 있다.
이러한 방식으로 단어의 의미를 찾는 방법을 distributional similarity라고 한다.

**단어의 의미를 벡터로 정의할 수 있다**:

각 단어는 dense vector로 표현할 수 있다.
가령, 단어 A의 dense vector는 단어 A가 사용되는 문장에 등장하는 다른 단어를 예측할 수 있도록 만들어야 한다.

단어 A와 함께 쓰이는 다른 단어들을 "context words"라고 하면, "context words"도 함께 쓰이는 단어들이 있다.
이때 유사도를 측정하기 위해 단어 A를 나타내는 벡터와 "other words"를 나타내는 벡터의 내적을 구한다.
그 다음 예측이 잘 되도록 두 벡터의 값을 조절한다.
재귀적인 연산이 포함되는 알고리즘을 통해 단어 A가 해당 context words를 잘 예측하고, context words가 단어 A를 잘 예측하도록 만든다.

**[주의] distributional vs. distributed representation**:

distributional similarity와 distributed representation은 혼동되는 개념이다.
distributed representation은 단어의 의미를 represent하는 dense vector에서 사용한다.

distributed representation은 distributional similarity는 개념을 사용해서 만들어진다.

distributional similarity는 단어의 의미에 대한 이론으로써 단어가 등장하는 context를 통해 단어의 의미를 파악하는 이론이다.

distributional은 denotational과 대조되는 개념이다.
단어의 의미에 대해 denotational은, 예를 들어, "안경"이라는 단어는 수많은 "안경"을 통해 의미가 정해진다.
(The deonotational idea of word meaning is the meaning of "glasses" is the set of pairs of glasses that are around the place. That's different from distributional meaning.)
즉, denotational은 단어의 개념적인 내용(conceptual content)을 전달한다.

> **Note**: Denotational Meaning 예시 : notorious - widely known, celebrated - widely known.

distributed는 one-hot word vector와 대조되는 개념이다.
one-hot word vector는 특정 샘플만 지역적(locally)으로 살펴본 representation이다.
가령, "안경"이라는 단어는 one-hot vector에서 값이 1인 index에 저장되어 있다고 말한다.
반면에 distributed representation에서는 아주 큰 벡터 공간에서 어떤 단어의 의미를 smearing(?)한다. (we're smearing the meaning of something over a large vector space.)

## 02 Word2Vec

**word2vec의 핵심 아이디어**.

word2vec의 원리는 모든 단어와 그 단어와 같이 쓰이는 단어의 관계를 예측하는 것이다.

`@@@resume` https://youtu.be/ERibwqs9p38?t=18m34s


---


---
