---
description: 13기 이유민
---

# \[Lecture 6\] Training Neural Networks I

### CS231n 6강 리뷰

6강에서는 Neural Networks를 학습시키는 방법들을 알아본다. 큰 흐름은 강의의 흐름을 그대로 따라간다.

![](.gitbook/assets/image%20%281%29.png)

![](.gitbook/assets/image%20%2811%29.png)

## Unit 1. Activation Functions

### 1.1. Activation Function

![](.gitbook/assets/image%20%2847%29.png)

Activation function\(활성화 함수\) 신경망의 출력을 결정하는 식이다. 그림과 같이 신경망에서는 뉴런에 연산 값을 계속 전달해주는 방식으로 가중치를 훈련하고 예측을 진행한다. 이 때 각각의 활성화 함수는 네트워크의 각 뉴런에 연결되어 있고, 각 뉴런의 입력이 모델의 예측과 관련되어 있는지의 여부에 따라 활성화된다. 활성화 함수는 훈련과정이나 역전파 과정에서 계산량이 많으므로 효율성이 중요하다.

![](.gitbook/assets/image%20%2876%29.png)

activation function의 종류를 간략하게 살펴보자.

먼저 binary step function은 다중 분류 문제에서 다중 출력을 할 수 없다. 또한 linear activation function\(선형활성화 함수\) 함수는 step function 과 달리 다중 출력이 가능하다. 하지만 몇 가지 문제가 있다.

**1. backpropagation 사용이 불가능**

역전파는 함수를 미분하여 사용하는 과정인데 선형함 수의 미분은 상수이기 때문에 입력값과 무관한 결과가 나오기 때문이다.

**2. hidden layer를 무시하고 얻을 수 있는 정보를 제한**

활성화 함수를 여러 층을 쓰면서 필요한 정보를 얻어야 하는데, 선형함수를 여러 번 사용하는 것은 마지막에 선형함수 한 번 사용하는 정도밖에 안된다. 따라서 hidden layer를 여러 번 사용하는게 의미가 없게 된다.

이러한 단점들 때문에 우리는 보통 비선형 함수를 사용한다. Non-linear activation function을 통해 입출력간의 복잡한 관계를 만들어서 입력에서 필요한 정보를 얻는 것이다. 이는 앞서 본 linear activation function과 달리 backpropagation이 가능하고, hidden layer를 통해 더 많은 핵심 정보들을 얻는 게 가능해지기 때문에 굉장히 유용하다.

{% hint style="success" %}
**강의에서 소개하는 Activation Function**

1. sigmoid
2. tanh
3. ReLU
4. Leaky ReLU
5. ELU
6. Maxout 
{% endhint %}

### 1.2. Sigmoid

![](.gitbook/assets/image%20%28126%29.png)

![](.gitbook/assets/image%20%2871%29.png)

sigmoid 함수는 입력값이 커질수록 1에, 작을수록 0에 수렴하는 형태이다. 출력값의 범위가 \(0,1\)이므로 정규화 관점에서는 gradient 가 발산해버리는 문제를 방지한다.

하지만 몇가지 문제가 있다.

**1.gradient vanishing \(기울기 소실\)**

우측 그림처럼 forward와 back을 반복하며 기울기를 구한다고 하자. 입력값이 -10이나 10인 경우 gradient가 소멸된다. 미분함수에 절대값이 큰 값이 input으로 들어가면 0 이 나 1로 수렴하고, 그 기울기는 0이 되기 때문에 0이 곱해지면 gradient가 사라진다. 결국 역전파는 계속 진행되는데 아래층에는 아무것도 전달이 되지 않는 문제가 생긴다.

**2.출력의 중심이 0이 아님**

우측 하단 그림처럼 경사하강법이 이루어질 때, 직선으로 가지 못하고 지그재그로 수렴한다. 파란선을 따라 쭉 움직이지 않으므로 굉장히 비효율적이다.

**3.지수함수 계산으로 계산 비용이 큼**

\*\*\*\*

### 1.3. tanh

![](.gitbook/assets/image%20%2821%29.png)

tanh 함수는 들어오는 입력값에 대해 \[-1,1\] 사이의 값을 출력하여 zero center가 된다. 하지만 sigmoid 와 같은 이유로 vanishing gradient 문제가 여전히 존재한다.

### 1.4. ReLU

![](.gitbook/assets/image%20%2857%29.png)

ReLU를 가장 많이 사용하고, 강의에서도 추천하고 있다.

음수 부분은 0, 양수 부분은 linear한 형태이다. 앞서 계속 문제가 되었던 saturation이 ReLU의 \(+\)영역에서는 일어나지 않아 기울기의 절반을 살릴 수 있다.

음수 부분을 일부 정보에 대한 무시와 수용이 일어난다고 볼 수 있고, linear하기 때문에 계산이 매우 효율적이다. 그래서 매우 빠르게 수렴한다.

하지만 zero-center 문제가 다시 발생하고, 또 입력값이 음수인 부분은 아예 학습을 하지 못한다.

{% hint style="info" %}
**Dead ReLU**

역전파 과정에서 ReLU 미분함수의 형태때문에 음수에서 기울기가 0이 되고, 0에서는 미분이 불가능하기 때문에 활성화가 되지 않는 현상
{% endhint %}

### 1.5. Leaky ReLU

![](.gitbook/assets/image%20%2883%29.png)

### 1.6. ELU

![](.gitbook/assets/image%20%2825%29.png)

### 1.7. Maxout

![](.gitbook/assets/image%20%2867%29.png)

Non-linear activation function에서 다룬 내용을 정리하자면,

{% hint style="success" %}
1. **ReLU를 사용하자. 단 learning rate를 잘 설정해야 한다.**
2. **Leaky ReLU / Maxout / ELU를 시도해본다.**
3. **tanh에서는 좋은 성능을 기대하지 말자.**
4. **sigmoid는 쓰지 말자.**
{% endhint %}

## Unit 2. Data Preprocessing

![](.gitbook/assets/image%20%2845%29.png)

![](.gitbook/assets/image%20%28113%29.png)

앞서 언급한 문제들은 데이터 전처리를 통해 해결할 수 있다. zero-center가 아닌 문제를 데이터를 중앙으로 모으는 전처리로 어느 정도 해결할 수 있다. 하지만 레이어가 깊어질수록 zero-center 문제가 계속 나타나기 때문에 일반적으로 이 과정만으로 완벽하게 보정하기는 힘들다.

그래서 normalization 정규화 과정은 같은 영역 내에 데이터들이 위치하도록 만들어서 기여하는 duddgid의 정도를 동일하게 만들어주는 역할을 한다. 하지만 이미지에서는 이미 0~255와 같이 정해져 있기 때문에 쓰지는 않는다. 또한 이미지에서는 pca나 whitening도 굳이 사용하지 않고, 오직 center만 전처리를 한다.

이미지분야의 center 전처리 과정은 다음과 같이 진행한다\(예시\)

1. 알렉스넷은 이미지의 평균을 뺌
2. VGGnet은 채널의 평균값을 뺌
3. ResNet은 평균값을 빼고 분산을 나눔

## Unit 3. Weight Initialization

### 3.1. Weight Initialization?

![](.gitbook/assets/image%20%28103%29.png)

relu에서 weight를 처음에 잘못 초기화시키면 처음부터 gradient가 죽어버리는 Dead relu 현상이 발생한다. 그래서 사실상 초기 가중치를 잘못 설정하면 기울기 소실 문제가 발생한다. 가중치 초기화에서 초기값을 모두 0으로 설정하는 경우 모든 뉴런에서 같은 일이 일어나 동일한 output을 내보내게 되고, 역전파를 할 때에도 모두 같은 gradient를 갖게 된다. 결국은 학습이 제대로 되지 않아 hidden layer를 여러 개 합한 의미가 사라진다. 즉, 뉴런의 비대칭성을 해치게 된다.

따라서 어떻게 초기화를 해야 할까 하는 고민에서 weight initialization이 시작된다.

### 3.2. 임의의 작은 수로 초기화

![](.gitbook/assets/image%20%2854%29.png)

먼저 임의의 작은 수로 초기화시키는 아이디어이다. 이처럼 평균이 0이고 표준편차가 0.01인 가우시안 분포에 대해 무작위의 숫자로 초기화시키는데, 이 방법은 네트워크가 깊어지면 문제가 발생한다.

![](.gitbook/assets/image%20%2819%29.png)

지금부터는 데이터가 적절하게 흐르게 하기 한 초기화 방법을 살펴본다.

### 3.3. Xavier Initialization

![](.gitbook/assets/image%20%2881%29.png)

Xavier 초기화 방법은 activation function이 시그모이드나 tanh를 사용한다고 가정했을 때 gradient vanishing문제를 막기 위한 방법이다. weight를 초기화하여 activation function에 input이 되는 값이 ㅡ saturation 범위에 걸리지 않도록 해 주는 이다.

이 노드와 다음 노드 개수에 의존하는 방법으로, 매우 효과적인 결과를 보이지만 활성화 함수로 ReLU를 용하는 경우 문제가 생긴다. ReLU는 출력의 절반을 죽이기 때에 출력의 분산을 반토막내고, 점점 많은 값들이 0이 된다. 따라서 ReLU와 같은 활성화 함수의 경우에는 다른 초기화 방법을 사용해야 한다.

### 3.4. HE Initialization

![](.gitbook/assets/image%20%2838%29.png)

He initialization은 이 문제를 해결한다. relu 출력을 절반을 줄이므로 2로 한 번 나눠 준다. 결과적으로 더 넓게 분포시켜주어 출력값이 고르게 분포되는 것을 확인할 수 있다.

## Unit 4. Batch Normalization

![](.gitbook/assets/image%20%28124%29.png)

batch normalization은 논문 흐름대로 쭉 설명한다. 

우선 batch normalization은 DNN의 internal covariate shift 성향을 피하기 위해 사용한다. 우리는 트레이닝 데이터를 잘 학습시켜 test 데이터를 잘 분류해야 하기 때문에, DNN 모델이 가지는 가중치 분포가 모두 동일해야 한다. 하지만 서로 다른 분포를 가지는 현상을 상단 ㅡ림고 같이 covariate shift라 한다.

![](.gitbook/assets/image%20%2834%29.png)

internal shift를 좀 더 구체적으로 설명하면 ㅏ래와 같다.

training data를 학습시킬 때, 이전 레이어의 값에 따라 다음 레이어 값들이 영향을 받게 된다. 이 때 dkaㅜ ㅠ제없이 제멋대로 학습이 진행되는 경우 가중치 값들의 범위가 넓어지게 되어 매개변수 값들의 qㅕㄴ동이 심해지게 되는 현상이다. 

![](.gitbook/assets/image%20%284%29.png)

이러한 현상은 whitning으로 해결한다. 하지만 계산량이 고 상수 bias의 값이 무시되는 등의 문제가 생기기 때문에 다른 접근을 하게 된다.

![](.gitbook/assets/image%20%2892%29.png)

whitening의 단점을 보완하고 동시에 internal covariate를 줄이기 위해 batch normalization이 어떻게 접근했는지 살펴 보자.

첫째, 레이어의 인풋이 d차원일 때, d개의 스칼라 값 사이의 상관관계를 무시하고 독립적으로 normalize한다. 즉 각각의 피처들이 이미 uncorelated 되어있다고 가정하는 것이다.

둘째, normalize를 전체 데이터셋이 아닌 mini batch 개념에서 계산해서 사용하는 것이다.

각각의 방법을 차례대로 살펴 보자. 

![](.gitbook/assets/image%20%2890%29.png)

먼저, 각 feature값이 상관없다고 가정하고 각각 독립적으로 normalize하는 경우이다. 따라서 앞선 whitening의 복잡한 식들이 매우 단순한 scalar 계산만으로 normalization이 가능해진다. 하지만 NN이 표현할 수 있는 것들이 제한될 수 밖에 없고 상관관계를 무시하고 학습하기 때문에 제대로 training이 되지 않는 상황이 발생할 수도 있다. 또한 각 피처에 ㅐ해 scalar형태로 평균과 분산을 구하고, 각각 normalize하면 평균 0, 분산 1로 고정되므로 sigmoid와 같은 활성화함수를 사용하는 경우 출력값이 linear한 부분만 나타나 nonlinearity를 애버리는 문제가 발생한다. 

이러한 문제들을 보완하기 위해 normalize한 값에 scale factor로 gamma를 shift factor로 추가한다. 이 수는 back-propagation 과정에서 함께 train된다. 이 때 네트워크를 그대로 사용하고  싶다면 gamma는 분산, beta는 평균으로 사용하면 된다.

![](.gitbook/assets/image%20%2874%29.png)

![](.gitbook/assets/image%20%2888%29.png)

두번째 접근은 1\)번으로 인해 가능한데, 관련 수식은 참고자료로 확인할 수 있다.

두번째 방법은 training data 전체에 대해 mean 과 variance를 구하는 것 이 아니라, mini batch 단위로 접근하여 계산한다. 현재 택한 mini batch 안에서만 mean과 variance를 구해서 그 값으로 normalize를 k므로 훨씬 효율적이다.

![](.gitbook/assets/image%20%2855%29.png)

일반적으로 batch normalization은 fully connected나 convolutional layer바로 다음 활성화 함수를 통과하기 전에 사용한다.

![](.gitbook/assets/image%20%28118%29.png)

batch normalization의 train 시 알 고 리 즘 을 살 펴 보 면 다 음 과 같 습 니다 . 미니배치 단위에서 평균과 분산을 구하고, 그 값 으로 normalize 시킨 후 gamma와 beta 파라미터를 통해 scale 과 shift도 시켜 준다.

![](.gitbook/assets/image%20%28102%29.png)

![](.gitbook/assets/image%20%28117%29.png)

![](.gitbook/assets/image%20%2866%29.png)

![](.gitbook/assets/image%20%2843%29.png)

batch normalization 을 사용함으로써 얻는 장점들을 정리하면 상단과 같다.

![](.gitbook/assets/image%20%288%29.png)

## Unit 5. Babysitting the Learning Process

![](.gitbook/assets/image%20%287%29.png)

## Unit 6. Hyperparameter Optimization

![](.gitbook/assets/image.png)

![](.gitbook/assets/image%20%28112%29.png)

![](.gitbook/assets/image%20%2860%29.png)

![](.gitbook/assets/image%20%285%29.png)

![](.gitbook/assets/image%20%28106%29.png)

hyperparameter tuning은 다음 강의에서 중점적으로 다루고 있기 때문에 크게 다루지는 않았다.

이번 강의에서 살펴 본 내용은 다음처럼 정리할 수 있다.

{% hint style="success" %}
Summary

1. Activation function은 ReLU를 사용하자
2. Data Processing - 이미지에서는 subtract mean
3. weight initialization을 사용하자
4. batch normalization을 사용하자
5. hyperparameter optimization 
   * random sample hyperparams
   * in log space when appropriate 
{% endhint %}

## References

* **\(💛\) 투빅스 13기 최혜빈님 12&13기 이미지 세미나 강의자료 \(💛\)**
* Stanford cs231n 6강
  * Slide [http://cs231n.stanford.edu/syllabus.html](http://cs231n.stanford.edu/syllabus.html)
  * Video [https://www.youtube.com/watch?v=wEoyxE0GP2M](https://www.youtube.com/watch?v=wEoyxE0GP2M)
* 12&13기 정규세션 12기 이승현님 NN심화 강의자료
* Activation function
* weight initialization [https://nittaku.tistory.com/269?category=742607](https://nittaku.tistory.com/269?category=742607)
* Batch Normalization
  * 논문 [https://arxiv.org/abs/1502.03167](https://arxiv.org/abs/1502.03167)
  * CNN BN 
    * [https://m.blog.naver.com/laonple/220811172205](https://m.blog.naver.com/laonple/220811172205) 
    * [https://wwiiiii.tistory.com/entry/Batch-Normalization](https://wwiiiii.tistory.com/entry/Batch)
    * [https://www.youtube.com/watch?v=TDx8iZHwFtM](https://www.youtube.com/watch?v=TDx8iZHwFtM)

