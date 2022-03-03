# Rich feature hierarchies for accurate object detection and semantic segmentation

R-CNN
- 목표 : 이미지를 넣었을 때, 해당 이미지에 어떤 물체들이(classification) 어디에 있는지(localization) 알아내는 것.
- 기존 object detection보다 simple하고 scalable(확장가능한) 알고리즘

목차
- 배경지식
- Key insights
- R-CNN
- 결과

배경지식

Segmantic Segmentation : 각각의 사물의 종류에만 집중하고 개체에는 관심이 없음. 
Object detection : classification +localization (bounding box 찾아내기)
region proposal : Seletive Search
초기 후보 영역을 다양한 크기와 비율로 생성
모든 영역에 대해 유사도 계산
유사한 영역과 근접한 pixel을 merge, grouping 해나감
Bottom-up
Object detection
- SIFT (Scale-Invariant feature transform) : 이미지의 크기, 회전 변환에도 영향을 받지 않고 비슷한 특징끼리 매칭을 해줌.
- HOG : 각 셀마다 EDGE 픽셀들의 방향에 대한 히스토그램 
PASCAL VOC : 5가지 영상 인식 task를 위한 opensource dataset
(classification, detection, segmentation, action, classification, large scale, recognition)

Key insights
- localize and segment objects를 위해 bottom-up 방식의 region proposal(== seletive search)에 CNN을 적용함.
- label이 지정된 training data가 부족할 때, 보조작업에 대한 supervised pre-training & domain-specific fine-tuning -> 성능향상
- CNN으로 object detection을 잘 구현해 낸 첫 사례 

R-CNN : Regions with CNN features
1. Input image
2. Extract region proposals(~2k)
3. Compute CNN features
4. Classify regions
