## Faster R-CNN : Towards Real-Time Object Detection with Region Proposal Networks (NIPS 2015)

1. Background 배경지식
- Fast R-CNN
    - 기존 R-CNN -> region proposal (2000개) warping 후 CNN 연산 : computation cost 비효율적
![rcnn](https://user-images.githubusercontent.com/50908451/157797247-f23de4d6-6b3a-42aa-8138-ac63e923aa12.png)
![fast_rcnn](https://user-images.githubusercontent.com/50908451/157797256-ab65dea9-ebb5-46c5-8b2e-3b536b008439.png)
- Rol Pooling (Region of Interest)

![region_proposal](https://user-images.githubusercontent.com/50908451/157797356-5f52dbe3-ebad-407b-a0af-b05b0e097783.jpg)
![pooling_sections](https://user-images.githubusercontent.com/50908451/157797367-53811bb0-d31a-462c-b010-e13c426582b4.jpg)
![a](https://user-images.githubusercontent.com/50908451/157797373-660c77f8-417a-4320-963c-8e522db38d15.jpg)
- Anchor Box : 사전 정의된 고정된 크기의 Box
    - 해당 Box를 통해 물체의 후보 위치를 뽑고, classification과 regression에 도움을 줌
![anchor_boxes](https://user-images.githubusercontent.com/50908451/157797748-ce907819-2bea-4447-8da1-ceb3f97c08a3.png)
![anchor](https://user-images.githubusercontent.com/50908451/157797756-a893c526-ed2a-47a8-badc-971bf333a81e.png)
2. Methods 방법
- 전체적인 구조
 
![method](https://user-images.githubusercontent.com/50908451/157797582-75dae7e0-c6f6-4cfa-b015-08a47fde3e60.png)
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
![training_step1](https://user-images.githubusercontent.com/50908451/157797474-7d2f2e6b-0b0f-48ee-9c08-e2130cbc77a8.png)
![training_step2](https://user-images.githubusercontent.com/50908451/157797480-8834ef73-04fb-4a77-826b-3079f70c0fa6.png)
- Approximate joint training
    - RPN과 Fast R-CNN 네트워크를 병합해 하나의 네트워크로 만드는 것
    - 한 번에 학습하므로 학습 시간은 빠르지만 BBOX의 derivate 값이 무시될 경향이 있음
- Non-approximate joint training
    - BBOX에 따른 gradient를 고려하여 학습을 진행 (본 논문에선 언급만 하였음)
  
4. Result 결과 
![result](https://user-images.githubusercontent.com/50908451/157797414-52c4d884-b51c-4038-b5d1-1c54727d059c.png)

![KakaoTalk_20220311_131334384](https://user-images.githubusercontent.com/50908451/157800842-7426a8b0-0789-479b-9570-ffa972b95a23.jpg)



