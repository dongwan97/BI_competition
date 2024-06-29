# 🪨 제 12회 산업통상자원부 공공데이터 활용 공모전
<br>

## MICO[Mineral Commentor] - AI 광물 리스크 탐지 레포트 서비스 
![시연영상](https://github.com/dongwan97/BI_competition/assets/122766043/b865aadd-3df2-45f5-a1c8-4816f2d320b6)

## 1. 🏃🏻‍♂️ 팀 소개
<p>팀명 : ...</p>
<p>프로젝트 기간 : 2024-06-01~2024-07-01</p>

|    소속    |          전공           |  이름  |
| :--------: | :---------------------: | :----: |
| 동국대학교 | 통계학과, 융합소프트웨어 | 김동완 |
| 동국대학교 | 통계학과, 데이터사이언스 | 이가린 |
| 동국대학교 | 통계학과, 데이터사이언스 | 조유솔 |
<br>

## 2. 💻 서비스 개요
본 서비스는 2차 전지 핵심 광물인 리튬, 니켈, 망간, 텅스텐에 대한 일일 레포트를 제공하는 것을 목적으로 한다. 레포트는 LSTM 모델을 활용하여 시장 전망지수와 희유 광물 지수를 기반으로 한 명일 가격 예측값을 제공하며, 자동으로 수집된 뉴스 데이터를 통해 최신 공급 동향을 요약하여 신속하게 파악할 수 있도록 돕는다. 또한, 뉴스 데이터를 분석하여 가격 예측값의 근거가 되는 공급 위기 요인을 리스트업하여 사용자에게 제공함으로써, 예측값의 신뢰성을 높이고 대응할 수 있도록 지원한다. 
<br>

## 3. 📈 가격예측 모델링
이번 프로젝트에서는 LSTM과 GRU모델을 사용하였습니다. 성능(RMSE)와 패턴을 얼마나 잘 따라가는 지를 비교한 결과 최종적으로 LSTM모델이 선정되었습니다. 또한 파생변수와 변수선택의 유의성과 모델성능을 비교검증 하기 위해서 3가지의 케이스(none,시장,all) 로 비교하였습니다. 각 케이스별로 선택된 변수는 아래와 같습니다.

| case | 변수명 |
| :----- | :----- |
| `NONE` | 광물가격변수, 종합광물지수, 메이저/희유금속 지수 | 
| `시장` | 광물가격변수, 종합광물지수, 메이저/희유금속 지수 | 
| `ALL` | 광물가격변수, 종합광물지수, 메이저/희유금속 지수, 환율(USD,RMD), 2차전지산업지수, 무역수지 | 


### 3.1. 예측 그래프
이번 프로젝트에서 최종 모델로 선정된 LSTM의 시계열 예측 그래프이다. 파란색은 실제 값을 의미하고 주황색은 예측된 값을 의미한다. 1년간의 시계열그래프를 그렸고 예측에 사용된 test 일자는 2024-04-23 ~ 2024-04-30 이다. 이번 프로젝트에서 사용된 파생변수 및 새로운 변수가 유의미함을 직관적으로 확인 할 수 있다. 

| 니켈 none | 니켈 all |
| :-----: | :-----: |
![LSTM 니켈none](https://github.com/dongwan97/BI_competition/assets/122766043/a65052ac-940b-4790-9c3e-ed99896a1fd7) | ![LSTM 니켈all](https://github.com/dongwan97/BI_competition/assets/122766043/c0e8fbb7-61cc-4a6a-89ef-eb11ba4b3ee5) 

| 리튬 none | 리튬 all |
| :-----: | :-----: |
![LSTM 리튬none](https://github.com/dongwan97/BI_competition/assets/122766043/07eed9a5-9b2f-4eed-91ae-0d08fa223f00) | ![LSTM 리튬all](https://github.com/dongwan97/BI_competition/assets/122766043/67e435cd-9a1d-4058-9ab5-b994b624806c) 

| 코발트 none | 코발트 all |
| :-----: | :-----: |
![LSTM 코발트none](https://github.com/dongwan97/BI_competition/assets/122766043/69e85f61-d8b5-477b-8dff-1378b5e40895) | ![LSTM 코발트all](https://github.com/dongwan97/BI_competition/assets/122766043/f23bc74a-4a89-43f3-90c9-6a54a0bfeb41)

| 망간 none | 망간 all |
| :-----: | :-----: |
![LSTM 망간none](https://github.com/dongwan97/BI_competition/assets/122766043/9ce7b8be-e1f5-43e8-946e-505c6fcf5b2c) | ![LSTM 망간](https://github.com/dongwan97/BI_competition/assets/122766043/86e42256-5ffc-4eef-b2dc-e7b37d3dd764)


### 3.2. 성능 평가
RMSE (Root Mean Square Error)는 원래 데이터와 예측 데이터 사이의 차이의 제곱을 측정한 후, 제곱근을 취한 값이므로 원래 데이터의 단위와 동일한 단위를 가지기 때문에 해석이 용이하다는 장점을 가지고 있습니다. 이러한 이유로 RMSE로 성능을 평가하였습니다.

성능 개선은 none케이스 대비 all 케이스의 RMSE의 하락 비율을 의미합니다.

### LSTM
|        |  니켈(USD/ton)  |  리튬(USD/ton)  | 코발트(RMD/kg) | 망간(USD/ton) |
| :----- | :-----: | :----: | :----: | :----: |
| `NONE` | **1216.14** | **22.5** | **4695.07** | **138.26** |
| `ALL` | **327.28** | **4.44** | **456.38** | **12.99** |
| `시장` | 714.79 | 7.71 | 862.3 | 28.53 |
| `성능개선` | **73%** | **81%** | **91%** | **91%** | 

### GRU
|        |  니켈(USD/ton)  |  리튬(USD/ton)  | 코발트(RMD/kg) | 망간(USD/ton) |
| :----- | :-----: | :----: | :----: | :----: |
| `NONE` | **1177.25** | **29.07** | **4961.32** | **133.09** |
| `ALL` | **337.64** | **5.04** | **472.46** | **15.81** |
| `시장` | 724.48 | 8.41 | 812.83 | 21.79 |
| `성능개선` | **72%** | **83%** | **91%** | **89%** | 

## 4. GPT 프롬프터

## 5. 서비스 개요 및 기대효과
### 5.1 서비스 개요
앞에서 언급한 딥러닝을 이용한 가격예측과 chatGPT 프롬프트를 활용하여 실사용 가능하도록 구체적인 프로토타입을 구현하였다. 구체적인 서비스를 고안하기 위하기 전에 기존에 서비스에서 느낀 pain point 는 두가지였다. 일자별 가격예측 모델은 존재하지 않고 광물 관련 정보들이 분산되어 있다는 점이다. 이 두가지를 고객관점에서 가장 해결할 수 있는 UI를 고안하였다. 서비스의 이름은 광물(Mineral)과 Commentor의 합성어로 MICO(미코)로 이름 지었다.

### 5.2 레포트 페이지
레포트 페이지에서는 한페이지에 특정 광물과 관련된 이슈와 정보를 한눈에 확인 할 수 있도록 구성하였다. 해당 페이지에서는 원하는 날짜를 선택하여 광물의 레포트를 받아 볼 수 있다. 앞서 언급한 바와같이 AI가 요약한 해당 일자 뉴스정보와 딥러닝을 통해서 예측된 가격 이 두가지 정보를 요약하여서 보여준다. 뿐만 아니라 기존 komis에서 제공하는 시장전망지표, 수급안정화, 환율 등의 정보를 요약하여 보여준다. 페이지의 하단에는 모델을 구성하는데 사용했거나 관련된 데이터를 시각화자료로 정리하여 보여준다.  

