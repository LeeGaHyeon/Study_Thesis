## Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks
목적 : 실시간 객체 탐지 

## Abstract  
- 이전에 SPPnet, Fast R-CNN는 running time 감소시켜 병목현상에 노출시킴.  
- RPN(Region Proposal Network) : shares full-image convolutional features with detection network -> cost-free region proposals.
  - 물체의 경계 및 물체의 위치 점수 예측
  - Fast R-CNN에서 사용하는 고품질의 region proposals를 생성하도록 end-to-end로 학습됨.
- VGG-16 모델의 경우, GPU 사용 시 모든 스텝을 포함해 5fps의 속도, PASCAL VOC 2007, 2012 및 MS COCO 데이터셋에서 이미지당 300 proposals만으로도 최첨단 물체 감지 정확도 달성.
- ILSVR와 COCO 2015 대회에서, Faster R-CNN과 RPN은 여러 트랙에서 1위 차지.

## Introduction 
최근 deep ConvNets이 이미지 분류 및 물체 감지 정확도를 크게 향상시켰다. 
이미지 분류와 비교하여, 객체 감지는 보다 복잡한 해결방법이 필요한 까다로운 작업이다.
이러한 복잡성으로 인해 현재 접근 방식은 느리고 우아하지않은 multi-stage 파이프라인에서 모델을 학습시킨다. 
Complexity arises because detection requires the accurate localization of objects, creating two primary challenges. First, numerous candidate object locations (often
called “proposals”) must be processed. Second, these candidates provide only rough localization that must be refined
to achieve precise localization. Solutions to these problems
often compromise speed, accuracy, or simplicity.
In this paper, we streamline the training process for stateof-the-art ConvNet-based object detectors [9, 11]. We propose a single-stage training algorithm that jointly learns to
classify object proposals and refine their spatial locations.
The resulting method can train a very deep detection
network (VGG16 [20]) 9× faster than R-CNN [9] and 3×
faster than SPPnet [11]. At runtime, the detection network
processes images in 0.3s (excluding object proposal time)while achieving top accuracy on PASCAL VOC 2012 [7]
with a mAP of 66% (vs. 62% for R-CNN)
