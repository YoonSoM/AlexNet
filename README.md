* * *
AlexNet의 기본구조는 LeNet-5와 크게 다르지 않다. 2개의 GPU로 병렬 연산을 수행하기 위해서 병렬적인 구조롤 설계되었다는 점이 가장 큰 변화이다

![Alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99FEB93C5C80B5192E)

AlexNet은 8개의 레이어로 구성되어 있다. 5개의 컨볼루션 레이어와 3개의 full-connected 레이어로 구성되어 있다. 

두번째, 네번째, 다섯번째 컨볼루션 레이어들은 전 단계의 같은 채널의 특성맵들과만 연결되어 있는 반면, 세번째 컨볼루션 레이어는 전 단계의 두 채널의 특성맵들과 모두 연결되어 있다

 우선 AlexNet에 입력 되는 것은 227 x 227 x 3 이미지다. (227 x 227 사이즈의 RGB 컬러 이미지를 뜻한다.) 그림에는 224로 되어 있는데 잘못된 겁니다. 
 
 * * *
 1) ReLU 함수: 활성화 함수로는 LeNet-5에서 사용되었던 Tanh 함수 대신에 ReLU 함수가 사용되었다. ReLU는 rectified linear unit의 약자이다. 같은 정확도를 유지하면서 Tanh을 사용하는 것보다 6배나 빠르다고 한다. AlexNet 이후에는 활성화함수로 ReLU 함수를 사용하는 것이 선호되고 있다. 
 
 ![Alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcexrVz%2FbtqBFwoUz96%2F6E1W6ALGpm3EfkJykHPFak%2Fimg.jpg)
 
 2) dropout: 과적합(over-fitting)을 막기 위해서 규제 기술의 일종인 dropout을 사용했다. dropout이란 fully-connected layer의 뉴런 중 일부를 생략하면서 학습을 진행하는 것이다[5]. 몇몇 뉴런의 값을 0으로 바꿔버린다. 따라서 그 뉴런들은 forward pass와 back propagation에 아무런 영향을 미치지 않는다. dropout은 훈련시에 적용되는 것이고, 테스트시에는 모든 뉴런을 사용한다. 
 
 ![Alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcMcWkE%2FbtqBFNcRhiv%2FjJyZWvbf9uQLmKJG3pQAK1%2Fimg.jpg)
 
 3) overlapping pooling: CNN에서 pooling의 역할은 컨볼루션을 통해 얻은 특성맵의 크기를 줄이기 위함이다. LeNet-5의 경우 평균 풀링(average pooling)이 사용된 반면, AlexNet에서는 최대 풀링(max pooling)이 사용되었다. 또한 LeNet-5의 경우 풀링 커널이 움직이는 보폭인 stride를 커널 사이즈보다 작게 하는 overlapping pooling을 적용했다. 따라서 정확히 말하면 LeNet-5는 non-overlapping 평균 풀링을 사용한 것이고, AlexNet은 overlapping 최대 풀링을 사용한 것이다. 
 
 ![Alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fb5hfOx%2FbtqBCUY3kpE%2FCKcK19bmDgtkSkWS5GPkBk%2Fimg.png)
 
 4) local response normalization (LRN): 신경생물학에는 lateral inhibition이라고 불리는 개념이 있다. 활성화된 뉴런이 주변 이웃 뉴런들을 억누르는 현상을 의미한다. lateral inhibition 현상을 모델링한 것이 바로 local response normalization이다. 강하게 활성화된 뉴런의 주변 이웃들에 대해서 normalization을 실행한다. 주변에 비해 어떤 뉴런이 비교적 강하게 활성화되어 있다면, 그 뉴런의 반응은 더욱더 돋보이게 될 것이다. 반면 강하게 활성화된 뉴런 주변도 모두 강하게 활성화되어 있다면, local response normalization 이후에는 모두 값이 작아질 것이다. 

5) data augmentation: 과적합을 막기 위해 dropout 말고도 또다른 방법이 사용되었다. 과적합을 막는 가장 좋은 방법 중 하나는 데이터의 양을 늘리는 것이다. 훈련시킬 때 적은 양의 데이터를 가지고 훈련시킬 경우 과적합될 가능성이 크기 때문이다. 따라서 AlexNet의 개발자들은 data augmentation이란 방법을 통해 데이터의 양을 늘렸다. 

 ![Alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FviqCJ%2FbtqBD1C97Ax%2FVRY44kp7K8Y1VpqNdu7fJk%2Fimg.png)
* * *
