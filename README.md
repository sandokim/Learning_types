# Supervised Learning 지도학습

x라는 이미지에 대한 y라는 레이블이 존재하는 상태에서 x가 정답 y에 가깝게 학습하는 방법

# Semi-Supervised Learning 준지도학습

목적은 supervised learning과 같은데 label이 없는 x데이터들이 존재한다.

데이터 분포가 Uniformly distributed된 경우 오히려 Decision boundary를 결정하는데 방해가 될 수도 있다. (마지막 Classify는 Linear classifier(Soft max)를 거치게 된다.)

<img src="https://github.com/sandokim/Learning_types/blob/main/images/Semi Supervised Learning.jpg" width="50%">

# Self-Supervised Learning, BYOL(Bootstrap Your Own Latent), PCL(Prototypical Contrastive Learning)

Keywords: Self Supervision, self supervised learning, do not need labels

Self-Supervised Learning은 Label이 아에없다. Data Augementation(Crop, color jitter, shift, rotation)을 통해 Anchor image에서 transformed된 이미지로 positive pair를 생성하고 나머지 다른 이미지들은 negative pair로 사용하여 loss function을 구성하고 학습시킨다.

--> From an augmented view of an image, we train the online network to predict the target network representation of the same image under a different augmented view. At the same time, we update the target network with a slow-moving average of the online network (Quoted from BYOL Abstract)

# Petext task (2014~2018)

Pretext를 잘 정의해서 주어진 입력 이미지들에 대한 정보를 잘 추출하는 방식

# Contrastive Learning (2018~)

Contrastive learning을 활용하여 주어진 입력 이미지들에 대한 정보를 추출하는 방식

* NPID (2018 CVPR)
* SimCLR (2020 ICML)
* MoCo (2020 CVPR) 
1. MoCo 이전 SSL(Self-Supervised Learning중 Contrastive Learning)은 Memory Bank에 관측치 전체에 대한 embedding 정보를 계속 저장해야하므로 메모리 이슈 존재,
2. Constrastive Learning에서 랜덤 샘플링으로 negative example을 구성하므로 데이터 샘플별로 학습에 기여하는 정도가 다름
-> Memory Queue를 사용 -> First In First Out (FIFO)

# Network구조 또는 Clustering 개념을 도입하여 주어진 입력 이미지들에 대한 정보를 추출하는 방식 (2020~)

* BYOL (2020 NIPS) --> You don't need the negative samples anymore in Self-Supervised Leanring which is cool and it actually doesn't collapse.

What is Collapse? Representation이 close될때 그냥 0이 되버리면 collapse가 발생하고 어떤 이미지가 들어와도 it always map it to the same thing.

--> You will always be close in representation space and you always win.. That doesn't learn a really good representation.

v, v'은 input image로부터 slightly differently augmented된 이미지, f(=ResNet50)를 통과하여 Representation을 얻음, projection을 하여 dimensionality를 줄인다.

ResNet50으로부터 나온 2048-d는 projection을 거치며 4092-d로 pump up되고 다시 256-d로 축소된다.

Represenation을 뽑는 Encoder는 simliar하고 하나는 다른 하나의 exponential moving average (ema)이다.

그리고 마지막에 하나로부터 다른 하나를 predict한다.

이를 통해 representation이 augmentation으로부터 independent하게 만든다. 

-> Representation can only include things that are not destroyed by the augmentations. And if you construct the augmentations smartly that means you only retain the semantic information.

<img src="https://github.com/sandokim/Learning_types/blob/main/images/BYOL Intuition.jpg" width="50%">

<img src="https://github.com/sandokim/Learning_types/blob/main/images/BYOL.PNG" width="80%">

BYOL Loss

q위의 bar는 normalization을 뜻한다.

q simply tries to predict the other representation. You do that for both ways. You get 2 Loss components each time. It's a symmetric loss

<img src="https://github.com/sandokim/Learning_types/blob/main/images/BYOL_Loss.PNG" width="80%">

* PCL (2020 ArXiv)

# SimCLR Contrastive Learning Framework 
(positive pair & negative pair, Anchor, push, pull, representation space, Student&Teacher framework knowledge distillation) 

-> Label이 부족한 상태에서 학습하는 방법

[SimCLR v1 & v2 리뷰](https://rauleun.github.io/SimCLR)

<img src="https://github.com/sandokim/Learning_types/blob/main/images/SimCLRv2.jpg" width="50%">

# [DINO: Emerging Properties in Self-Supervised Vision Transformers](https://arxiv.org/abs/2104.14294)

Self-distillation : Teacher와 Student는 Same architecture를 가진다.

* Global crop : 한 이미지내에서 50% 이상의 영역을 Crop
* Local crop : 한 이미지내에서 50% 이하의 영역을 Crop

아래에서 Student Network는 Global crop, Local crop을 모두 사용하고, Teacher Network는 Global crop만을 사용한다.

아래 그림의 목적은 Student Network와 Teacher Network가 same representation을 예측하기를 기대한다. => 이미지 x에서 다르게 transform한 x1과 x2가 같기를 바란다. 

x1, x2는 class x에서 augmented된 것임.

<img src="https://github.com/sandokim/Learning_types/blob/main/images/Self_distillation.jpg" width="50%">

# Weakly Supervised Learning 약지도 학습

# Unsupervised Learning 비지도 학습

# Representation Learning -> 이미지의 representation을 학습한다.

## Representation learning을 한 뒤 Network를 Freeze 또는 Learnable로 정하여 classficiation을 수행할 수 있다. --> Linear Evalutation & Fine Tuning & Transfer Learning

Linear Evalutation은 dataset에 대해 학습한 모델(Pretrained model)을 Freeze하고 linear classifier만 on the top에 올려서 주어진 테스크를 classification한다.

Transfer Learning은 Large Dataset에서 Training하여 image representation을 배운 네트워크를 small dataset 또는 different dataset에 대해 Training하는 학습방법이다.

Transfer Learning은 가끔 Fine tuning으로 불리기도 한다.

<img src="https://github.com/sandokim/Learning_types/blob/main/images/Linear Evalutation & Fine Tuning & Transfer Learning.jpg" width="70%">
