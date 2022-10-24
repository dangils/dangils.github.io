---
title: "[AI] Object Detection 문제영역 정리"
date: "2022-09-27 22:33:12"
categories: [AI,Object detection]
tags: [AI,vision,object detection]


---


### 컴퓨터 비전의 대표적인 문제
1) Image Classification
- 이미지를 알고리즘에 입력하여 그 이미지가 어떤 클래스 라벨에 속하는지 분류 하는것

2) Semantic Image Segmentation
![image](https://user-images.githubusercontent.com/74512114/197518572-7d1ff66a-6004-44aa-aa53-9dd63516f604.png)

- 단순히 사진을 보고 분류하는 것에 그치지 않고 그 장면을 완벽하게 이해하는 수준의 문제
- 위의 사진 처럼 모든 픽셀을 해당하는 class로 분류 하는 것(이미지에 있는 모든 픽셀에 대한 예측을 하는 것이기 때문에 dense prediction 이라고도 불림)

3) Object Detection
![image](https://user-images.githubusercontent.com/74512114/197519131-0370bcc8-1725-49da-8258-2f0dcca35c67.png)

- 물체 검출은 이미지 내에서 알고리즘을 훈련시킬 때 사용된 라벨에 속하는 모든 물체를 검출하는 것
- 물체가 있는 영역의 위치 정보를 Bounding Box로 찾고 사물의 라벨을 분류


------

### Object Detection 문제 영역의 출력값
> x_min, y_min, x_max, y_max, class, confidence

![image](https://user-images.githubusercontent.com/74512114/197519847-c7d76ba1-ac8f-4a15-8abf-c2ef71e437dd.png)
- ex) 사람의 경우 좌표가 `(15,5), (240,297)` 지점으로 바운딩 박스가 그려져 있다,
`class`는 'person'이고 `confidence`는 0.92

------

[참고 용어]
**Ground Truth 란?**
- 문제 영역의 Ground Truth 데이터는 사람이 지정한 Bounding Box 와 Class Label


### Object Detection의 성능 비교를 위한 정량적 지표
> Intersection over Union(IoU) Metric
>
![image](https://user-images.githubusercontent.com/74512114/197522543-869bbeff-7b10-4c1f-a9e7-4622c5400f9b.png)

- 1개의 Bounding Box와 1개의 Bounding Box가 얼마나 일치하는 지를 0.0 ~ 1.0 사이로 표현
- 분모 부분엔 두 영역의 합집합, 분자 부분엔 두 영역의 교집합에 해당


<br>

**Metric 참고**
![image](https://user-images.githubusercontent.com/74512114/197524990-f1116b1f-6117-4b2f-b4ac-2373761827df.png)


> Precision, Recall, F1
- Precision : 정밀도(Precision)는 검색된 결과들 중 관련 있는 것으로 분류된 결과물의 비율(예측한 것 중에 맞춘 비율) → TP/(TP+FP)
- Recall : 재현율(Recall)은 관련 있는 것으로 분류된 항목들 중 실제 검색된 항목들의 비율(전체 갯수 대비 맞춘 갯수 비율) → TP/(TP+FN)
- ex) 이미지에 10개의 사과가 있고 모델이 6개의 사과를 검출, 이중 5개는 TP, 1개는 FP 일때,
precision = 5/6 , Recall = 5/10
<br>

- F1 : Precision과 Recall의 조화 평균, Precision과 Recall을 한번에 비교 → 2*(pre*rec)/(pre+rec)

**결론**
- Precision과 Recall을 같이 비교하는 `F1` 스코어가 높아야 좋은 모델
- 위의 예시에서 precision만 봤을 때는 좋은 성능이지만, Recall은 그렇지 않음. 때문에 두 값을 종합해서
알고리즘을 평가 하기 위한 AP(Aveage Precision) 필요

### Average Precision(AP)
- Positive 판단 기준 : 일정한 임계치의 IoU(Pascal VOC 데이터셋의 경우, 0.5)를 넘기면 맞춘 것으로 간주
- Average Precision(AP) : Recall 별 Precision의 평균
- AP는 Precision-Recall 그래프의 아래 면적

![image](https://user-images.githubusercontent.com/74512114/197536639-0c329f96-2d8a-4ff8-bdbb-0f3b8be7256a.png)
- recall이 서서히 증가하다가 rank 10에서 5번째 True 일때 1.0
