
ⓒ JMC 2017

**Source**  
+ Stanford CS224N (2017)  
+ [Chris McCormick](http://mccormickml.com/2016/04/19/word2vec-tutorial-the-skip-gram-model/)  
+ [Deep learning for NLP](https://www.dropbox.com/s/ca748gr9i91tn8f/NLP_with_Deep_Learning_%ED%95%9C%EA%B5%AD%EC%96%B4.pdf?dl=0)

---

## Skip-Gram Model

**모델**:

$$p(context | w_{t})$$

Skip-gram model은 단어($w_{t}$)로부터 문맥($context$)을 예측하는 모델이다.
input으로 center word가 주어지면 center word의 context word를 예측한다.
예를 들어, center word로 "Soviet"가 주어지면, $p(Union|Soviet)$는 $p(Sasquatch|Soviet)$보다 확률이 더 클 것이다.
실제 corpus에서 "Union"이 "Soviet"의 context word라면, 모델은 $p(Union|Soviet)=1$에 가깝게 만들어야 한다.
모델을 실제로 계산하는 방법은 다음과 같다.  

$$P(o | c) = \frac{\exp(u_o^{T}v_{c})}{\Sigma_{w=1}^{V} \exp(u_w^{T}v_{c})}$$

+ $o$ : output word(=labeled context word)
+ $c$ : center word
+ $u_o$ : output word(=labeled context word)를 나타내는 vector
+ $u_w$ : 모든 context word를 나타내는 vector
+ $v_c$ : center word를 나타내는 vector
+ $V$ : 단어 종류 개수

> **Note**: center word 주변에 있는 모든 단어를 context word($u_w$)라고 했을 때, 특정 window size 안에 속한 context word를 labeled context word($u_o$)라고 구분지었다.

내적($u_o^{T}v_{c}$)은 두 벡터의 유사함을 측정하는 loose한 기준으로 쓸 수 있다.
왜냐하면 벡터 $v_1$과 벡터 $v_2$가 유사할수록 내적한 값($v_{1} \cdot v_{2}$)이 크기 때문이다.
가령, center word로써 "Soviet"을 나타내는 벡터가 $v_{c}$이고, context word로써 "Union"을 나타내는 벡터가 $u_1$, "Sasquatch"를 나타내는 벡터가 $u_2$라면, $u_1^{T}v_{c} > u_2^{T}v_c$일 것이다.

마지막으로 center word 벡터와 context word 벡터를 내적한 스칼라값으로 구성된 $V$차원 벡터의 요소를 확률값으로 만들기 위해 softmax function을 취한다.

**Fake Task**:

사실 모델이 수행하는 학습은 fake task이다.
오차 함수에 의해 모델은 단어로부터 문맥을 잘 예측하는 것을 목표로 삼지만, 우리의 목표는 모델이 목표를 달성하는 과정에서 만들어지는 word vector를 얻는 것이다.
모델의 학습 과정은 다음과 같다.

+ 모델은 center word의 context word를 알고 있는 상태에서 학습(supervised learning)한다.
+ 학습 과정에서 center vector와 context vector의 내적을 계산한다.
+ 이때 모델은 center vector와 output vector를 내적한 값을 exponetiate해서 확률값으로 만들고, 그 값이 최대한 1이 되도록 학습한다.
+ 내적을 exponentiate한 확률값이 최대한 1이 되도록 center vector와 output vector의 값을 조절한다.

학습이 끝나면 center vector가 곧 우리의 관심사인 word vector가 된다.

**Loss Function**:

$$J^{\prime} (\theta) = \Pi_{t=1}^{T}\Pi_{-m \leq j \leq m, \ j \neq 0}p(w_{t+j} | w_t ; \theta)$$

단, 계산의 효율을 고려해서 곱셈 연산은 $\log$의 덧셈으로 바꿔준다.
그리고 $J^{\prime}$ 값은 클수록 좋지만, 일반적으로 오차 함수의 값은 최소화하는 형태로 만드는 것이 기계학습의 관례이므로 $-\log$를 취해서 negative log likelihood로 바꿔준다.

$$J(\theta) = -\frac{1}{T} \Sigma_{t=1}^{T}\Sigma_{-m \leq j \leq m, \ j \neq 0}\log p(w_{t+j} | w_t ; \theta)$$

$$J(\theta) = -\frac{1}{T} \Sigma_{t=1}^{T}\Sigma_{-m \leq j \leq m, \ j \neq 0}\log \frac{\exp(u_o^{T}v_{c})}{\Sigma_{w=1}^{V} \exp(u_w^{T}v_{c})}$$

**Optimization(#inProgress)**:

derivatives for the center vector parameters.

derivatives for the output vector parameters.

---


---
