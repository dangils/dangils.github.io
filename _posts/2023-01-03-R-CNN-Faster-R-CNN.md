---
title: "[AI] R-CNN/Fast R-CNN/Faster R-CNN 정리"
date: "2023-01-03 23:24:12"
categories: [AI,Vision]
tags: [AI,vision,object detection]


---


> Object Detection 참고

**1-stage detector** :

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fds1hoJ%2FbtqCX8tXMTh%2FJlGldm3aTsGzwiratKhbqK%2Fimg.png)

- 1-stage는 2-stage와 다르게 RoI영역을 먼저 추출하지 않고 전체 image에 대해서 convolution network로 classification, box regression(localization)을 수행

**2-stage detector** :

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4Fi2X%2FbtqCWbZjit2%2FsN9Ba7jKxiVI0h4S5InzMk%2Fimg.png)

- Selective search, Region proposal network와 같은 알고리즘을 및 네트워크를 통해 object가 있을만한 영역을 우선 뽑아낸다.
- 이 영역을 RoI(Region of Interest)라고 한다. 이런 영역들을 우선 뽑아내고 나면 각 영역들을 convolution network를 통해 classification, box regression(localization)을 수행한다.

<br>

> 대표적인 2-Stage Detector
> - R-CNN, Fast R-CNN, Faster R-CNN

---------

## R-CNN

### R-CNN Process
1. R-CNN은 selective search를 통해 region proposal을 먼저 뽑아낸 후 CNN 모델에 들어간다.

2. CNN모델에 들어가 feature vector를 뽑고 각각의 class마다 SVM로 classification을 수행한다.
`SVM` : 서포트 벡터 머신(SVM: Support Vector Machine)은 분류 과제에 사용할 수 있는 강력한 머신러닝 지도학습 모델, 최적의 Decision Boundary(결정 경계)를 산출

3. localization error를 줄이기 위해 CNN feature를 이용하여 bounding box regression model을 수정한다.

### R-CNN 한계점
1) RoI (Region of Interest, Object 가 있을 만한 영역) 마다 CNN연산을 함으로써 속도저하
2) multi-stage pipelines으로써 모델을 한번에 학습시키지 못함

--------------

## Fast R-CNN
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcC15WF%2FbtqA57Lvbgm%2FZX3VwTFw89kc2Gbx2SKuD0%2Fimg.png)

### Fast R-CNN Process

1. R-CNN에서와 마찬가지로 Selective Search를 통해 RoI를 찾는다.

2. 전체 이미지를 CNN에 통과시켜 feature map을 추출한다.

3. Selective Search로 찾았었던 RoI를 feature map크기에 맞춰서 projection시킨다.

4. projection시킨 RoI에 대해 `RoI Pooling`을 진행하여 고정된 크기의 feature vector를 얻는다.

5. feature vector는 FC layer를 통과한 뒤, 구 브랜치로 나뉘게 된다.
- 하나는 softmax를 통과하여 RoI에 대해 object classification을 한다.

- bounding box regression을 통해 selective search로 찾은 box의 위치를 조정한다.

`ROI Pooling`
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb6vdLi%2FbtrscNzKsuW%2Fgm0k8RObuX1ty5AUVJFLL0%2Fimg.png)

- feature map의 proposal region에서 미리 정해놓은 크기(FC layer의 인풋 사이즈)의 격자(grid)에 맞추어 bin마다 maxpooling 하여 고정된 크기의 vector를 만들어낸다.

✔️ why? 사이즈가 제각각인 proposal region을 FC layer의 인풋으로 넣기위해 고정된 크기의 feature로 만들어 주기 위해.



------------

## Faster R-CNN

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdhq4iV%2FbtqBaAFDl4d%2FIZdxlDX5mkPMdnoKy2f2k0%2Fimg.png)

**RPN(Region Proposal Network)**
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbmPXTk%2FbtqQKuiOcdM%2FzzdpQeoS1TgzfvrnfD0xKK%2Fimg.png)

- 원본 이미지에서 region proposals를 추출하는 네트워크
- region proposals에 대하여 class score를 매기고, bounding box coefficient를 출력

(https://herbwood.tistory.com/10)















