# 차원 축소 Dimensionality Reduction

* 고차원 데이터는 당연하게도 다음과 같은 단점을 갖고 있다.
    - 특징 변수 과다 -> 불필요한 변수 존재
    - 계산 복잡도 증가 -> 모델링 비효율성
    - 시각적 표현의 어려움

* **변수 선택과 추출** 두 가지 방법으로, 고차원 데이터에서 중요한 정보는 유지하면서 데이터의 차원을 줄여 단점을 보완할 수 있다.

||변수 선택 Selection|변수 추출 Extraction|
|-|-|-|
||분석 목적에 부합하는 소수의 예측 변수 선택|예측 변수를 변환하여 새로운 변수 추출|
|장점|선택한 변수 해석이 쉬움|변수 간 상관관계 고려, 변수 개수 대폭 감소|
|단점|변수 간 상관관계 고려 어려움|추출된 변수의 해석 어려움.|
||**Example**||
|*Supervised*|전진선택법, 후진제거법, Ingormation Gain, LASSO|**PLS**, LDA|
|*Unsupervised*|PCA Loading|**PCA**, Autoencoder|

(*Supervised* : 모델이나 통계적 유의성을 기준으로 결정)

* <u>여기서는 PLS만을 중점적으로 다룬다.</u>


# PLS Partial Least Squares
## 부분 최소 제곱법

## 목차

1. [PLS 알고리즘](#pls-알고리즘)

2. [PCA와 비교](#pca와-비교)

3. [부분 최소 제곱-판별 분석 PLS-DA](#부분-최소-제곱-판별-분석-partial-least-squares-discriminant-analysis)

4. [부분 최소 제곱-변수 중요도 투영 PLS-VIP](#부분-최소-제곱-변수-중요도-투영-partial-least-squares-variable-importance-in-projection)


## PLS 알고리즘

* 다차원 입력 변수 X에서 예측 변수 Y와 가장 큰 공분산을 갖는 k개의 선형 조합(선형 결합)을 생성

* ex) n_components=2  
x1, x2, x3, x4, x5 에 가중치(0.5, 0.2, 0.1, 0.1, 0.1)를 부여하여 새로운 component1, component2 생성  
-> compoent1, 2는 y와 공분산 최대값을 가짐.

PLS 알고리즘
<div style="text-align: left;">

$t = Xw$
</div>

$$
Cov(t, Y) = {Cov(t, Y) \over \sqrt{var(t)}\sqrt{var(Y)}} \sqrt{var(t)}\sqrt{var(Y)} = Corr(t, Y)\sqrt{var(t)}\sqrt{var(Y)}
$$

<div style="text-align: left;">

$\therefore Maximize \; Cov(t, Y) \propto Maximize \; Corr(t, Y) \; var(t)$
</div>

* X : 입력 변수
* Y : 예측 변수
* t : X의 선형조합
* w : 선형조합의 가중치

<details>
<summary>가중치 w를 정하는 방법</summary>
<div></div>
<div style="text-align: left;">

$Maximize \; Cov(t, Y) \\
= Cov(Xw, Y) \\
= E[(Xw - E[Xw]) \cdot (Y-E[Y])] \\
= E[(Xw) \cdot (Y)] \\
= {1 \over n} \sum^n_{i=1}(Xw)_i \cdot Y_i \\
= {1 \over n} (Xw)^T Y \\
= {1 \over n} w^T(X^TY) \\
\\
\rightarrow w = X^TY \; 일때 \; w와 \; X^TY 같은 \; 방향으로 \; 값 \; 최대화$
</div>
</details>


## PCA와 비교

* X만 고려하는 PCA와 달리 X와 Y 모두를 동시에 고려하므로 예측력이 높은 성분 추출
* PCA보다 클러스터링된 데이터에 효과적
* 선형/비선형 관계에 대해서는 PCA보다 통찰력 부족


## 부분 최소 제곱-판별 분석 Partial Least Squares-Discriminant Analysis

* 회귀 기반인 PLS 알고리즘을 확장하여 차원 축소와 분류를 동시에 수행 가능
* 클래스의 수에 따라 PLS1-DA, PLS2-DA로 분류되나, 두 모델의 분류 성능을 비교한 경험적 연구는 적음. (PLS1, PLS2도 마찬가지)
    - PLS1-DA 범주가 둘인 경우, Y1 = 1, Y2 = -1
    - PLS2-DA 범주가 셋 이상인 경우, One-Hot Encoding
* 과적합(overfitting)되기 쉬우므로 교차 검증(cross-validation)이 중요



## 부분 최소 제곱-변수 중요도 투영 Partial Least Squares-Variable Importance in Projection




## References

Loong Chuen Lee, Choong-Yeun Liong, Abdul Aziz Jemain, 「Partial least squares-discriminant analysis (PLS-DA) for classification of high-dimensional (HD) data: a review of contemporary practice strategies and knowledge gaps」

Daniel Ruiz-Perez, Haibin Guan, Purnima Madhivanan, Kalai Mathee, Giri Narasimhan,「So you think you can PLS-DA?」

고슴군, 「Dive into Data Science」, https://dive-into-ds.tistory.com/33

Sopora, 「하루일지」, https://blog.naver.com/aromi913/223255936957