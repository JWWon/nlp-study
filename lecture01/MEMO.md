## 캐글 영화 리뷰 분석 튜토리얼

캐글 경진대회 중에 괜찮은 것들이 많다

* [Sentiment Analysis on Movie Reviews | Kaggle](https://www.kaggle.com/c/sentiment-analysis-on-movie-reviews)
* [Toxic Commnet Classification Challenge | Kaggle](https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge)
* [Spooky Author Identification | Kaggle](https://www.kaggle.com/c/spooky-author-identification)



#### 평가 - ROC 커브(Recover-Operating Characteristic curve)

- TPR(True Positive Rate)과 FPR(False Positive Rate)을 각각 x, y 축으로 놓은 그래프
- 민감도 TPR
  - 1인 케이스에 대해 1로 예측한 비율
  - ex. 암환자를 진찰해 암이라고 진단
- 특이도 FPR
  - 0인 케이스에 대해 1로 잘못 예측한 비율
  - ex. 암환자가 아닌데 암이라고 진단함
- x, y가 둘 다 [0, 1] 범위이고, (0, 0)에서 (1, 1)을 잇는 곡선
- ROC 커브의 밑 면적이 1에 가까울수록(왼쪽 꼭지점에 다가갈수록) 좋은 성능



#### Use Google's Word2Vec for movie reviews

* 자연어 텍스트를 분석해 특정 단어를 얼마나 사용했는지, 얼마나 자주 사용했는지, 어떤 종류의 텍스트인지 분류. 긍정인지 부정인지에 대한 감정분석, 내용을 요약하는 정보를 얻을 수 있다.
* Word2Vec을 통한 감정분석을 해보는 튜토리얼
* 단어의 의미와 관계를 이해하는데 도움
* 상당수의 NLP 기능은 NLTK모듈에 구현되어 있는데, 이 모듈은 코퍼스, 함수와 알고리즘으로 구성되어 있다.



#### BOW(bag of words)

* 가장 간단하지만 효과적이어서 널리 사용됨
* 장, 문단, 문장, 서식과 같은 입력 텍스트의 구조를 제외하고 각 단어가 말뭉치에 얼마나 많은지를 헤아림
* 구조와 상관없이 단어의 출현횟수만 카운팅, 텍스트를 담는 가방(bag)으로 생각할 수 있다.
* BOW는 단어의 순서과 완전히 무시된다는 단점이 있음.
  ex. 아래의 두 문장은 동일하게 반환된다.
  * `it's bad, not goot at all.`
  * `it's good, not bad at all.`
* 이를 보완하기 위해 n-gram을 사용하는 데, BOW는 하나의 토큰을 사용하지만 n-gram은 n개의 토큰을 사용할 수 있도록 한다.



