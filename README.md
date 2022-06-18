# Supervised Learning

# Semi-Supervised Learning

# Self-Supervised Learning, BYOL

Label이 아에없다. Data Augementation(Crop, color jitter, shift, rotation)을 통해 Anchor image에서 transformed된 이미지로 positive pair를 생성하고 나머지 다른 이미지들은 negative pair로 사용하여 loss function을 구성하고 학습시킨다. 

# SimCLR Contrastive Learning Framework 
(positive pair & negative pair, Anchor, push, pull, representation space, Student&Teacher framework knowledge distillation) 

-> Label이 부족한 상태에서 학습하는 방법

[SimCLR v1 & v2 리뷰](https://rauleun.github.io/SimCLR)

# [DINO: Emerging Properties in Self-Supervised Vision Transformers](https://arxiv.org/abs/2104.14294)

Self-distillation : Teacher와 Student는 Same architecture를 가진다.

* Global crop : 한 이미지내에서 50% 이상의 영역을 Crop
* Local crop : 한 이미지내에서 50% 이하의 영역을 Crop

아래에서 Student Network는 Global crop, Local crop을 모두 사용하고, Teacher Network는 Global crop만을 사용한다.

아래 그림의 목적은 Student Network와 Teacher Network가 same representation을 예측하기를 기대한다. => 이미지 x에서 다르게 transform한 x1과 x2가 같기를 바란다. 

x1, x2는 class x에서 augmented된 것임.

<img src="https://github.com/sandokim/Learning_types/blob/main/images/Self_distillation.jpg" width="50%">

# Weakly Supervised Learning

# Unsupervised Learning
