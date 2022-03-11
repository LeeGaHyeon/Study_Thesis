## Faster R-CNN : Towards Real-Time Object Detection with Region Proposal Networks (NIPS 2015)

1. Background 배경지식
- Fast R-CNN
    - 기존 R-CNN -> region proposal (2000개) warping 후 CNN 연산 : computation cost 비효율적
- Rol Pooling (Region of Interest)
- Anchor Box : 사전 정의된 고정된 크기의 Box
    - 해당 Box를 통해 물체의 후보 위치를 뽑고, classification과 regression에 도움을 줌

2. Methods 방법
- 전체적인 구조 
- RPN (Region Proposal Network)
    - 1. 출력된 feature map에서 nxn의 filter를 사용하여 각 anchor별 Region Proposal(bbox 후보)을 구함.
    - 2. 1x1 conv를 사용하여 10x10x(9x2), 10x10x(9x4)의 output 즉, anchor x class(true prob, flase prob), anchor x cordinates(bbox 좌표)
    - * Rol : Region of Interest * objectness score : Box confidence score로 Box가 객체가 있는지에 대한 가능성과 정확도를 판단
    - Positive label, Negative label
    - Positive 조건
        - a. IoU > 0.7    * IoU : Intersection Over Union
        - b. 그 외엔 모두 Negative label을 붙여 loss 계산 시 학습에 영향을 미치지 않도록 설계
- Detection (Fast R-CNN)
    - RPN에서 추출한 region을 Detection Network의 Input으로 사용
    - Feature map에 Rol을 투영시킨 후, Rol pooling layer를 통해 고정된 vector로 classification과 regression을 진행

3. Training 학습과정
- Alternative training 번갈아 가며 학습하는 것
    - RPN학습 -> Fast R-CNN 학습 반복
    - 즉, Fast R-CNN은 RPN으로 초기화된 네트워크를 사용하며 이 단계를 반복
- Approximate joint training
    - RPN과 Fast R-CNN 네트워크를 병합해 하나의 네트워크로 만드는 것
    - 한 번에 학습하므로 학습 시간은 빠르지만 BBOX의 derivate 값이 무시될 경향이 있음
- Non-approximate joint training
    - BBOX에 따른 gradient를 고려하여 학습을 진행 (본 논문에선 언급만 하였음)
  
4. Result 결과 


