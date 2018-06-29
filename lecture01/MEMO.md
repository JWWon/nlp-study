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



### 데이터 정제 Data Cleaning and Text Preprocessing

* 기계가 텍스트를 이애할 수 있도록 텍스트를 정제
* 신호와 소음을 구분한다. 아웃라이어 데이터로 인한 오버피팅을 방지한다.

```
1. BeautifulSoup을 통해 HTML 태그를 제거
2. 정규표현식으로 알파벳 이외의 문제를 공백으로 치환
3. NLTK 데이터를 사용해 불용어(Stopword)를 제거
4. 어간추출(스테밍 stemming)과 음소표기법(Lemmatizing)의 개념을 이해하고 SnowballStemmer를 통해 어간을 추출

* 불용어: 자주 등장하지만 문장의 의미와 맞지 않는 단어
```



### 텍스트 데이터 전처리 이해하기

한국어 : KoNLPy, 트위터 형태소 분석기 사용

* 정규화 normalization
  * 입니닼ㅋㅋ => 입니다 ㅋㅋ, 샤릉해 => 사랑해
* 토큰화 tokenization
  * 한국어를 처리하는 예시입니다 ㅋㅋ
    => 한국어(Noun), 를(Postposition), 처리(Noun), 하다(Verb), 예시(Noun), 이다(Adjective), ㅋㅋ(KoreanParticle)
* 어근화 stemming
  * 입니다 => 이다
* 어구 추출 phrase extraction
  * 한국어를 처리하는 예시입니다 ㅋㅋ
    => 한국어, 처리, 예시, 처리하는 예시



### 불용어 제거(Stopword Removal)

조사, 접미사, i, me, it, this 등과 같은 단어는 문장에 빈번하게 등장하지만 실제 의미를 찾는데 큰 기여를 하지 않는다. Stopwords는 'to', 'the'와 같은 용어를 포함하므로, 사전 처리 단계에서 제거하는 것이 좋다. NLTK에는 153개의 영어 불용어가 미리 정의되어 있다. 17개의 언어에 대해 정의되어 있으며, 한국어는 없다.



### 스태밍(어간추출, 형태소 분석)

* 어간추출 - 어형이 변형된 단어로부터 접사 등을 제거하고 그 단어의 어간을 분리해 내는 것
* 'message', 'messages', 'messaging'과 같이 복수형, 진행형 등의 문자를 같은 의미의 단어로 다룰 수 있도록 도와줌
* stemming(형태소 분석) - NLTK에서 제공하는 형태소 분석기를 사용. 포터 형태소 분석기는 보수적, 랭커스터 형태소 분석기는 더 적극적.



### Lemmatization 음소표기법

음소 표기법(lemmatization)은 단어의 보조 정리 또는 사전 형식에 의해 식별되는 단일 항목으로 분석 될 수 있도록 굴절된 형태의 단어를 그룹화하는 과정.

​	1) 배가 맛있다.

​	2) 배를 타는 것이 재미있다.

​	3) 평소보다 두 배로 많이 먹어서 배가 아프다.

위의 문장들에서 "배"는 모두 다른 의미를 갖고있다. 음소 표기법은 앞 뒤 문맥을 보고 단어의 의미를 식별하는 것이다.