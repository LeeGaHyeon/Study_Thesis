## Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks
목적 : 실시간 객체 탐지 

## Abstract  
- 이전에 SPPnet, Fast R-CNN는 running time 감소시켜 병목현상에 노출시킴.  
- RPN(Region Proposal Network) : shares full-image convolutional features with detection network -> cost-free region proposals.
  - 물체의 경계 및 물체의 위치 점수 예측
  - Fast R-CNN에서 사용하는 고품질의 region proposals를 생성하도록 end-to-end로 학습됨.
- VGG-16 모델의 경우, GPU 사용 시 모든 스텝을 포함해 5fps의 속도, PASCAL VOC 2007, 2012 및 MS COCO 데이터셋에서 이미지당 300 proposals만으로도 최첨단 물체 감지 정확도 달성.
- ILSVR와 COCO 2015 대회에서, Faster R-CNN과 RPN은 여러 트랙에서 1위 차지.
