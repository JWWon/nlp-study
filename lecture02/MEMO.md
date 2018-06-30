## 캐글 영화 리뷰 분석 튜토리얼 2

튜토리얼1 과의 가장 큰 차이점 : CountVecotrization 대신 Word2Vec을 사용해 벡터화

#### Word2Vec

컴퓨터는 숫자만 인식할 수 있고, 한글 & 이미지는 바이너리 코드로 저장된다.

* one_hot_encoding 혹은 Bag of Words에서 vector size가 크고 sparce 하므로, neural net 성능이 잘 나오지 않는다.
* `주위 단어가 비슷하면 해당 단어의 의미는 유사하다`라는 아이디어
* 단어를 트레이닝 시킬 때, 주위 단어를 label로 매치하여 최적화
* 단어를 `의미를 내포한 dense vector`로 매칭시키는 것
* Word2Vec은 분산된 텍스트 표현을 사용하여 개념간 유사성을 본다. 예를 들어, 파리와 프랑스가 베를린과 독일이 수도-나라와 같은 방식으로 관련되어 있음을 이해

> gensim: Word2Vec을 python으로 개발한 라이브러리



