---
description: 13기 고유경
---

# \[MIT\] Introduction to Human-Centered Artificial Intelligence \(AI\)

#### 

![](.gitbook/assets/1%20%281%29.png)

이번 주차는 특별 시간으로 MIT 컴퓨터공학과 Lex Fridman 교수의 **인간 중심\(Human-Centered\) AI 개론 강의**\([Lecture Video](https://www.youtube.com/watch?v=bmjamLZ3v8A)\)를 리뷰하고자 한다.

![](.gitbook/assets/2%20%281%29.png)

## 1. Human-Centered AI

![](.gitbook/assets/6%20%281%29.png)

AI는 필연적으로 **불확실성\(uncertainty\)**이라는 특성을 갖는다. 때로는 공정하지 않고 안전에 반하는 결과를 내뱉는 모델의 학습 과정을 완전하게 설명하는 것이 불가능하기 때문이다. 따라서, **데이터 가공 과정과 학습된 모델을 real-world에 적용하는 과정에서 인간의 감독, 관리가 필요**하다는 것이 인간중심AI의 핵심 주장이다. 

![](.gitbook/assets/7%20%281%29.png)

조금 더 구체적으로 살펴보자면, 

**\[Training Process\]** 기존 학습 과정에서는 ImageNET과 같이 이미지들의 라벨을 지정하는 등 인간이 완전한 데이터 가공 작업을 수행하고 그 이후에 모델이 알고리즘을 학습해나가는 식으로 진행되었다. 반면,  HCAI의 데이터 가공 과정에서는 모델이 데이터의 일부를 뽑아 인간에게 질문하고 인간은 이에 대한 답을 제공하므로서 machine teaching을 수행한다. 

**\[Real-World Operation\]** 모델의 학습 결과를 실제로 적용할 때에도 모델의 결정을 그대로 따라가는게 아닌 인간의 감독, 결정이 개입한다. 인간의 적절한 가치 판단이 개입해야 안전한 방향으로 적용될 수 있기 때문이다.

## 2. 5 Grand Challenges of HCAI

Learning Phase와 Real-World Operation로 나누어 HCAI의 주요 챌린지들을 살펴보자.

### 1. HCAI during Learning Phase

![](.gitbook/assets/9%20%281%29.png)

{% tabs %}
{% tab title="1. Machine Teaching" %}
더욱 효과적인 지도학습을 위하여 적용되는 machine teaching은 적은 양의 예시를 통해 모델이 묻고 인간이 답하는 annotation 과정을 포함한다. 또한, 전체 데이터 중 어떤 부분을 활용할 것인지 학습 과정 중에 결정하는 active learning, 데이터를 여러 형태로 변형하는 data augmentation, 하나의 예시만 가지고 학습을 진행하는 one-shot learning과 강화학습의 self-play 등 모델이 직접 답을 찾아나가고 인간은 맞고 틀리다의 정답을 제시하는 학습 알고리즘을 활용한다.

Grand challenge의 예시로, 위키피디아의 데이터로만 학습된 모델이 COCO object detection 챌린지에서 sota를 갱신했다. 또한 0~9까지의 숫자 이미지로 이루어진 MNIST 데이터셋에서 숫자 당 오직 1개의 이미지만 가지고 학습한 모델이 0.3% 정도 밖에 되지 않는 오류를 기록했다.
{% endtab %}

{% tab title="2. Human-in-the-Loop Reward Engineering" %}
슬라이드 속 두 그림은 각각 인간과 강화학습 모델의 게임 화면을 캡쳐한 것이다. 왼쪽 인간의 화면처럼 배는 물길을 따라 앞으로 나아가야 하는데 RL agent의 화면을 보면 보상을 최대화하기 위해 원을 돌면서 순환하고 있음을 확인할 수 있다. 이러한 학습 과정의 오류를 방지하기 위하여 인간의 가치들을 학습 과정에 주입시켜 모델이 끝까지 완주를 마치도록 하면서, 보상을 얻을 수 있는 적절한 방식을 터득해나가도록 하는 것이다.

이와 비슷한 예시로 자동화된 추천시스템을 통해 의사결정을 내리도록하는 새로운 접근 방식이 있을 수 다.
{% endtab %}
{% endtabs %}

### 2. HCAI during Real-World Operation

![](.gitbook/assets/10%20%281%29.png)

{% tabs %}
{% tab title="3. Human Sensing" %}
모델의 학습 결과를 실제 세계에 반영할 때 중요한 점은 모델이 인간을 제대로 이해하고 있느냐의 문제이다. 인간의 음성, 이미지, 텍스트 데이터를 기반으로 인간의 신체적, 심리적 상태와 더불어 상황의 맥락을 정확히 인지하고, 장기적인 관점에서는 모델이 인간화되도록 하는 human sensing을 HCAI의 또 다른 챌린지 볼 수 있다.

관련 예시로는 특정 사람과 30일간의 상호작용 이후 이 사람이 퇴사를 원하는지 아닌지를 95%의 정확도로 예측한 모델이 있다고 다.
{% endtab %}

{% tab title="4. Human-Robot Interaction Experience" %}
HCAI에서 인간과 로봇의 상호작용은 매우 중요한 영역이다. 모델의 학습결과를 그대로 반영하여 보여주는 것이 로봇이라 했을 때, 인간과 로봇 두 객체가 모두 성장할 수 있는 방향으로 상호작용하도록 해야 한다.

관련 예시로 1000억 마일 주행에 성공한 semi 자율주행 기술과 소셜 챌린지에서 우승한 아마존의 AI 비서 렉사가 있다.
{% endtab %}
{% endtabs %}

![](.gitbook/assets/11%20%281%29.png)

**5. AI Safety**

마지막으로 가장 중요하게 여겨야 할 **안성** 관련 문제이다.  세상을 이롭게 하기 위하여 연구되는 AI 기술이 자율주행차의 사고처럼 인간의 생명에 직결되는 치명적인 결과를 낼 때가 있고, 얼굴인식 기술이 인종차별적 결과를 내놓는 등 윤리에 위배될 때도 있다.

이는 모두 AI의 불확실성에 기반한 결과이기 때문에, 불확실성이라는 특성에 따른 의도하지 않은 결과를 피기 위해서 **2개 이상의 독립적인 모델을 학습**시키고 **모델들의 결과가 상충**되는 경우 **인간의 판단이 개입**하는 방법을 활용할 수 있다. 우측 하단의 표를 보면 앞서 설명한 **Arguing Machines** 방법을 사용했을 때 오류가 급격히 줄어든 것을 확인할 수 있다.



## 3. Deep Learning for Understanding Human

![](.gitbook/assets/13%20%281%29.png)

인간을 이해하기 위한 딥러닝 기술은 그동안 여러 분야로 나뉘어서 발전해왔다. 얼굴 탐지, 포즈 인식, 음성 인식, 추천시스템, 감성분석, 언어 이해, 대화 시스템 등 우리에게 익숙한 연구 분야들이 인간중심AI라는 대주제로 묶일 수 있다. 지금부터는 강의에서 다뤘던 파란색 파트 6개 중 비전 분야와 연관된 **얼굴 인식, 동작 인식, 포즈 추정** 순으로 연구 흐름을 살펴보고자 한다.



### 1. Face Recognition \(얼굴 인식\)

![](.gitbook/assets/14%20%281%29.png)

**Detection**\(Where is head?\)과 **Recognition**\(Who is this?\)는 다르다. 

체 탐지는 사진이나 영상 속 객체가 어디에 있는지 위치 자체를 탐색하는 것이라면, 얼굴 인식은 탐지된 얼굴이 누구인지를 인식하는 태스크이다.

**얼굴 인식이 어려운 이유**는 비슷한 외모의 사람들을 구별하기 어렵다는 점, 얼굴 사진 데이터를 얻기가 까다롭다는 점, 동일한 사람일지라도 각도나 표정에 따라 다양한 얼굴 형상이 나타난다는 점, 스마트폰 얼굴인식 잠금해제와 같이 보안과 직결된 태스크에서는 거의 100에 가까운 정확도를 기록해야 한다는 점 등이 있다.

슬라이드 아래 화살표를 따라 **얼굴 인식 분야의 연구 흐름**을 살펴보자.

**2014년 페이스북**에서 발표한 논문 [DeepFace: Closing the Gap to Human-Level Performance in Face Verification](https://www.cs.toronto.edu/~ranzato/publications/taigman_cvpr14.pdf) 은 딥 뉴럴넷 구조를 이용한 얼굴인식 연구의 물꼬를 트며 CVPR에 등재되었다.

이어서 **2015년 SOTA**를 기록하며 CVPR에 등재된 **구글**의 논문  [FaceNet: A Unified Embedding for Face Recognition and Clustering](https://arxiv.org/pdf/1503.03832.pdf)에서는 Embedding\(임베딩\)을 통해 feature representation\(이미지의 특징을 숫자 벡터로 재표현하는 것\)을 직접적으로 최적화하는 방법을 선보였다.

**2017년** 마찬가지로 CVPR에 등재된 **워싱턴대**의 논문 [Level Playing Field for Million Scale Face Recognition](https://openaccess.thecvf.com/content_cvpr_2017/papers/Nech_Level_Playing_Field_CVPR_2017_paper.pdf)에서는 기존 연구들의 데이터 사이즈를 크게 윗도는 약 **67만명의 사진 470만장**으로 연구를 진행하여 대량의 이미지 데이터로 대표되는 앞으로의 연구 방향을 시사했다.

앞으로 얼굴 인식 분야의 연구는 모델이 어떻게 사람간의 얼굴 차이를 구분하고 인식하는지 블랙박스와도 같은 모델의 학습 과정을 해석하고 개인정보 이슈를 풀어나가는데에 집중하게 될 것이다.

 



### 2. Activity Recognition \(동작 인식\)

![](.gitbook/assets/15%20%281%29.png)

**동작 인식\(Activity Recognition\)**은 이미지나 비디오에 나타나는 사람의 동작을 분류하는 태스크이다.

**동작 인식이 어려운 이유**는 우선 동작의 종류가 셀 수 없이 많아 유한한 클래스로 분류할 수 없고, 비슷한 동작이라 하더라도 다른 범주로 분류되어야 하는 경우 모델이 구분하기 어렵다. 복잡하고 모호한 기준으로 인해 학습의 명확성을 보장하기 어렵다.

슬라이드 아래 화살표를 따라 **동작 인식 분야의 연구 흐름**을 살펴보자.

**2017년** CVPR에 등재된 **딥마인드**의 논문 [Quo Vadis, Action Recognition? A New Model and the Kinetics Datas](https://arxiv.org/pdf/1705.07750.pdf)에서는 action classification을 위한 새로운 데이터셋인 Kinetics 데이터셋을 만들고 이를 기반으로 I3학습을 진행하였다. 3d ConvNet을 two stream으로 구성하여 RGB 뿐 아니라 optical flow 정보도 넣어줌으로써 motion 정보에 대해 더 잘 예측할 수 있도록 하여 Sota를 기록하다.

**2018년** 마찬가지로 CVPR에 등재된 **오스틴대**의 논문 [Im2Flow: Motion Hallucination from Static Images for Action Recognition](https://www.groundai.com/project/im2flow-motion-hallucination-from-static-images-for-action-recognition/1)에서는 동작 이미지에서 이어지는 동작 flow까지 예측하면서 동작 분류를 수행하였다.

이처럼 앞으로 동작 인식 분야의 연구는 동작의 complexity를 줄이고 단순한 동작 분류를 넘어 이어지는 동작 예측까지 수행할 수 있도록 발전될 것이고 그 과정에서 모델이 '문맥', 즉 상황적 배경을 고려할 수 있도록 하는데에 집중할 것이다.





### 3. Body Pose Estimation

![](.gitbook/assets/16%20%281%29.png)

동작 인식과 별개로 더욱 정교하게 자세를 추정하는 **Pose Estimation** 태스크있다.

**자세 추정이 어려운 이유**는 매우 고차원적인 최적화를 수행해야 한다는 점과, 손이나 발 등 몸에서 관절이 겹치는 경우 모델이 정확하게 자세를 잡아내기 어렵다는 점이 있다.

슬라이드 아래 화살표를 따라 **자세 추정 분야의 연구 흐름**을 살펴보자.

우선 **2014년 Google**은 [DeepPose: Human Pose Estimation via Deep Neural Networks](https://arxiv.org/pdf/1312.4659.pdf) 논문에서  딥 뉴럴넷 구조를 이용한 자세추정 연구의 물꼬를  네트워크 DeepPose를 고안하여 CVPR에 등재되었다.

이어서 **2017년** Sota를 기록한 **카네기멜런의** 논문 [Realtime Multi-Person 2D Pose Estimation using Part Affinity Fields](https://arxiv.org/pdf/1611.08050.pdf)에서는 PAFs\(Part Affinity Fields\)라는 새로운 개념을 도입하여, 이전 연구들의 receptive field size를 증가시키는 방법과는 다르게 part 사이의 상관 관계를 보다 명시적으로 네트워크에 반영하였다. 그림에서 볼 수 있듯이, 다리는 다리끼리, 팔은 팔끼리 bottom up 구조로 자세를 추정한다.

2018년 CVPR에 등재된 논문 [Total Capture: A 3D Deformation Model for Tracking Faces, Hands, and Bodies](https://arxiv.org/pdf/1801.01615.pdf)에서는 2d를 넘어서 3d로 자세를 추정하여  연구의 폭을 넓혔다. 자세와 더불어 개인의 모양, 공간에서의 위치까지 고려하는 Deformation model을 고안하였고 PCA를 이용하여 차원을 축소하였다.

앞으로의 자세 추청 연구는 3d estimation과 더불어, 같은 자세 내에서의 dynamic한 속성을 어떻게 잡아낼 것인지, 또 동작의 변형을 어떻게 구분할 것인지에 집중하게 될 것이다.







![](.gitbook/assets/18%20%282%29.png)

이처럼 Human-Centered AI는 다양한 태스크를 바탕으로 사회 전반적인 영역에서 인간을 이해하고 인간과 상호작용할 수 있는 지평을 넓힐 것으로 기대된다. 본 강의는 MIT 컴퓨터공학과 교수 Lex Fridman의 유튜브 채널에서 만나 수 있다.

개인적으로 덧붙이면, 프리드만 교수님의 유튜브 채널은 강의 영상 뿐만 아니라 AI 유명 인사와의 인터뷰, 그리고 ~~교수님의 감미로운 기타연주까지~~ 다양한 컨텐츠로 구성되어 있으니, 구독하여 소식들을 팔로업하기를 추천한다.







