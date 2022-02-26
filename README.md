# Deeplearning-fianl-exam
Final-exam for submission in DeepLearning class

**실험 결과**

Network Architecture

![](https://blog.kakaocdn.net/dn/bX1uJt/btruyMYIa76/tBhsUvUbxf9HaGSl99RbPK/img.png)


Evaluation model

![](https://blog.kakaocdn.net/dn/cNUJ07/btrunPci0sl/WJ9bBqE65SLPyiKXAaO460/img.png)

Train, Test Accuracy and Loss graph

![](https://blog.kakaocdn.net/dn/5X5Vz/btruxjbpPXe/yHqvvDZYqk9Dd0xHIHOJXK/img.png)

Model.fit() 결과

![](https://blog.kakaocdn.net/dn/buRaTV/btruqEODd29/dCu1xjrzHgzhro7keaEwW0/img.png)

훈련된 모델을 바탕으로 테스트용 데이터로 시험할 때 54.22%의 정확성을 보여주었다.

Prediction

![](https://blog.kakaocdn.net/dn/mwfNQ/btruolvkMgc/A3UilovnVYTmhW0LKNCkg1/img.png)

훈련된 모델을 바탕으로 단일 이미지에 대한 테스트 10회 prediction 하였다.

첫번째 결과: 경로에 있는 파일 number(index), 두번째 결과: unique class number,  
세 번째 결과: 훈련된 라벨 name, 네 번째 결과: 테스트용 라벨 name  
다섯 번째 결과: 테스트 이미지

![](https://blog.kakaocdn.net/dn/Kk2A6/btruuiRCXTM/iG9K2drGr6MmuPiGDAWmBK/img.png)


10번의 예측결과 훈련된 train\_x를 test\_x에 일치하는지 결과를 출력하였고,

6번 일치 4번 일치하지 않은 결과를 도출하였다.

**고찰**

이번 프로젝트는 수업시간에 배운 내용을 바탕으로 로컬에 저장되어 있는 이미지 파일을 불러온 후 train\_x, test\_x에 파일들을 float32 type으로 array형 4차원으로 대입하였다. train\_y, test\_y는 파일 경로에서 split을 하여 클래스를 추출하였다. 처음에 언더바( \_ ) 로 구분해서 추출하였는데 100개의 클래스가 나오지 않았다. 클래스 명 중간에 willow\_tree, maple\_tree 와 같이 언더바가 있는 클래스명이 있어 이를 수정하여 추출하였고, 정상적으로 50000개의 이미지 파일에서 클래스를 추출하고 unique 메서드를 이용하여 100개의 클래스를 추출하였다. 이후 수업시간에 사용한 Model을 사용하여 complie을 수행하였다. epochs를 처음 20회 수행하였고 Val\_accuracy가 37%가 나와서 모델 수정을 하였다. 효율적인 모델 작성을 위해 Tensorflow, Keras 공식문서를 찾아보았고 Pretrained되지 않는 이상 70%이상 Val\_accuracy가 나오는 model 예제를 찾기 어려웠다. 때문에, 기존에 사용하던 kernel\_size를 수정하였고, Dropout값을 0.2à0.25, 0.3à0.5로 수정하였다. 그리고 레이어 중간에 배치 정규화를 수행하였다. 각 레이어마다 정규화 하는 레이어를 두어, 변형된 분포가 나오지 않도록 하였다. Val\_accuracy가 37% à 51% à 54% 수정할수록 더 높은 결과를 도출하였다. Prediction을 통해 1개의 이미지를 뽑아서 테스트를 10번 수행하였고 10번 중 5~6번 맞는 결과를 얻었다.
