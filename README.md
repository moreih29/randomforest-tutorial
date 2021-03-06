# Random Forest tutorial

## 개요
![결정 트리의 앙상블](https://upload.wikimedia.org/wikipedia/commons/thumb/3/36/%EB%9E%9C%EB%8D%A4%ED%8F%AC%EB%A0%88%EC%8A%A4%ED%8A%B8_%ED%95%99%EC%8A%B5%EA%B3%BC%EC%A0%95_%EB%B0%B0%EA%B9%85.png/1280px-%EB%9E%9C%EB%8D%A4%ED%8F%AC%EB%A0%88%EC%8A%A4%ED%8A%B8_%ED%95%99%EC%8A%B5%EA%B3%BC%EC%A0%95_%EB%B0%B0%EA%B9%85.png)
- 결정 트리의 단점은 훈련 데이터에 과적합 되는 경향이 있다는 것
- 랜덤 포레스트는 전체 데이터 중 일부 데이터에 과적합된 결정 트리를 많이 만듦
- 데이터 선택 또는 특성 결정에서 전체 중 일부 선택을 랜덤으로 함
- 생성된 모든 결정 트리의 결과를 평균냄으로써 성능을 향상시킴

## 동작 과정
### Step 1
- 각 결정 트리는 다른 일부 데이터에 대해 과적합이 되어야 함
- 이를 위해 부트스트랩 샘플(bootstrap sample)을 생성함
- n개의 데이터 속에서 n번의 중복 추출을 수행함
- 따라서, 원래 데이터 셋과 크기는 같지만 어떤 데이터는 누락될 수 있고, 어떤 데이터는 중복되어 여러번 포함되어 있을 수 있음
- 예를 들어, 리스트 `['a', 'b', 'c', 'd']`에서 부트스트랩 샘플을 만들면, `['b', 'd', 'd', 'c']` 또는 `['d', 'a', 'd', 'a']`와 같은 형태가 될 수 있음

### Step 2
- 부트스트랩 샘플링을 통해 데이터 셋을 만들고 결정 트리를 생성
- 이 때, 각 노드는 모든 특성을 대상으로 최선의 분기를 찾는 것이 아님
- 각 노드는 특성들 중 랜덤으로 선택된 m개의 특성에 대해서만 최선의 분기를 찾음
- 매 노드마다 다른 특성에 대해 최선의 분기를 찾음

### Step 3
- 랜덤하게 선택된 데이터, 랜덤하게 선택된 각 노드의 특성을 사용해 결정 트리가 다수 생성됨
- 분류의 경우, 생성된 결정 트리들이 예측한 확률의 평균을 통해 최종 결정을 함
- 회귀의 경우, 예측 값의 평균을 통해 최종 값을 예측

## 앙상블(Ensemble)
- 랜덤 포레스트와 같이 여러 개의 모델을 연결하여 더 강력한 모델을 생성하는 방법을 앙상블(ensemble)이라고 함
- 배깅(Bagging)과 부스팅(Boosting)이 있음

### 배깅(Bagging)
- Bootstrap aggregation을 뜻하며, 복원 추출(bootstrap)하여 통합(aggregation)하는 것임
- 즉, 복원 추출을 통해 전체 데이터 셋의 일부 특징만을 가진 여러 훈련 데이터를 생성함
- 그리고, 각 훈련 데이터 셋에 대한 모델들의 평균 예측 값을 최종 예측으로 사용
- 랜덤 포레스트는 배깅의 일종이며, 다른 점은 특성 선택 또한 임의로 선택함

### 부스팅(Boosting)
- 부트스트랩을 사용해 데이터를 추출함
- 모델을 학습시키고, 모델이 잘못 예측한 데이터에 대해 가중치를 부여
- 가중치가 적용된 데이터에 대해 다시 부트스트랩을 사용
- 이를 반복하여, 잘못된 예측에 대해 깊은 학습을 진행

---
출처
- https://tensorflow.blog/%ed%8c%8c%ec%9d%b4%ec%8d%ac-%eb%a8%b8%ec%8b%a0%eb%9f%ac%eb%8b%9d/2-3-6-%ea%b2%b0%ec%a0%95-%ed%8a%b8%eb%a6%ac%ec%9d%98-%ec%95%99%ec%83%81%eb%b8%94/
- https://ko.wikipedia.org/wiki/%EB%9E%9C%EB%8D%A4_%ED%8F%AC%EB%A0%88%EC%8A%A4%ED%8A%B8
- https://datapedia.tistory.com/21