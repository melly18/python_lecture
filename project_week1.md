## 언론사별 사회복지 기사 본문 감정분석

이번 시간에는 사회복지 이슈를 다룬 기사 본문을 컴퓨터로 분석하는 방법을 알아본다.

이번 프로젝트의 질문은 다음과 같다.

> 같은 사회복지 이슈를 다룬 기사라도 언론사에 따라 감정 표현과 보도 방식에 차이가 나타날까?

프로그램은 분석 결과를 계산해 주지만, 그 결과가 언론사의 성향을 완벽하게 판정해 주는 것은 아니다. 분석한 기사, 기간, 기준, 인공지능 모델에 따라 결과가 달라질 수 있다.

---

## 1. 오늘 정할 것

다음 항목을 정한다.

- 사회복지 이슈 1개
- 분석할 언론사
- 기사 수와 기간
- 기사 본문을 어떤 방식으로 분석할지
- 네 명이 맡을 기능

처음부터 많은 기사를 분석하지 않는다. 먼저 기사 3~6개로 프로그램이 작동하는지 확인한다.

---

## 2. 본문 분석이 어려운 이유

기사 본문에는 기자의 설명, 인용문, 수치, 정책 발표, 비판과 반론이 함께 들어 있다.

예를 들어 다음 문장을 보자.

> 지원 확대를 발표했지만, 현장에서는 여전히 복지 사각지대가 해소되지 않았다는 지적이 나온다.

이 문장에는 긍정적으로 보이는 표현과 부정적으로 보이는 표현이 함께 있다. 따라서 감정분석 결과는 기사의 진짜 감정을 완벽하게 나타내는 것이 아니라, 정해진 방법으로 계산한 분석 결과다.

---

## 3. 기사 데이터

기사 하나를 표의 한 행으로 저장한다.

| 언론사 | 제목 | 본문 | 날짜 | 주제 |
|---|---|---|---|---|
| 언론사A | 노인 지원 확대 | 정부가 지원을 확대했다. | 2026-05-01 | 노인 빈곤 |

이런 표 데이터를 저장하는 대표적인 파일 형식이 CSV이다. CSV는 행과 열의 데이터를 단순한 텍스트로 저장한다.

```text
media,title,body,date,topic,url
```

파이썬에서 읽을 때는 다음처럼 사용할 수 있다.

```python
import pandas as pd

df = pd.read_csv("articles.csv", encoding="utf-8-sig")

print(df)
print(df["body"])
```

`df["body"]`는 기사 본문 열을 가져오는 코드다.

---

## 4. 분석 방법 1: 감정어휘 사전

긍정 단어와 부정 단어를 정하고, 기사 본문에 몇 번 등장하는지 세어 점수를 계산할 수 있다.

```python
positive_words = [
    "확대", "개선", "지원", "보장", "회복", "기대"
]

negative_words = [
    "위기", "차별", "빈곤", "사각지대", "논란", "피해"
]
```

```python

def calculate_dictionary_score(text):
    score = 0

    for word in positive_words:
        score += text.count(word)

    for word in negative_words:
        score -= text.count(word)

    return score
```

긍정 단어가 많이 나오면 점수가 커지고, 부정 단어가 많이 나오면 점수가 작아진다. 하지만 이 방법은 문맥을 충분히 이해하지 못한다.

예를 들어 `피해가 줄었다`라는 문장에서 `피해`만 발견하면 부정 점수가 될 수 있다.

---

## 5. 분석 방법 2: AI 감정분석 모델

이미 다른 데이터로 학습된 인공지능 모델에 문장을 입력하여 긍정 또는 부정으로 분류할 수 있다.

이번 시간에는 사전학습 모델을 사용한다. 사전학습 모델은 우리가 직접 학습시키는 것이 아니라, 다른 사람이 미리 학습시켜 둔 모델이다.

### 5.1 라이브러리 설치

Google Colab의 코드 셀에 다음을 실행한다.

```python
!pip install transformers torch
```

처음 실행할 때 필요한 라이브러리를 설치한다.

- `transformers`: 인공지능 언어 모델을 사용하는 라이브러리
- `torch`: 모델의 계산을 돕는 라이브러리

### 5.2 모델 불러오기

```python
from transformers import pipeline

classifier = pipeline(
    "sentiment-analysis",
    model="WhitePeak/bert-base-cased-Korean-sentiment"
)
```

Hugging Face 웹사이트에서 파일을 직접 다운로드할 필요는 없다. 모델 이름을 지정하면 처음 실행할 때 필요한 파일을 자동으로 내려받는다.

다만 Colab 런타임이 초기화되면 다시 다운로드할 수 있다.

### 5.3 짧은 문장 분석

```python
text = "복지 지원이 확대되어 생활 개선이 기대된다."

result = classifier(text)

print(result)
```

결과는 다음과 비슷한 구조로 나온다.

```python
[
    {
        "label": "LABEL_1",
        "score": 0.98
    }
]
```

결과의 가장 바깥쪽은 리스트이고, 리스트 안에 딕셔너리가 하나 들어 있다.

- `label`: 모델이 판단한 라벨
- `score`: 모델의 확신도처럼 해석할 수 있는 값

모델 카드에서 라벨의 의미를 확인해야 한다. 이 예시 모델에서는 `LABEL_0`을 부정, `LABEL_1`을 긍정으로 설명한다.

### 5.4 결과 꺼내기

```python
label = result[0]["label"]
score = result[0]["score"]

print("라벨:", label)
print("확신도:", score)
```

`result[0]`은 리스트의 첫 번째 딕셔너리다. 그 뒤에 `"label"` 또는 `"score"`를 적어 원하는 값을 가져온다.

### 5.5 사람이 읽는 표현으로 바꾸기

```python
def convert_label(label):
    if label == "LABEL_0":
        return "부정"
    elif label == "LABEL_1":
        return "긍정"
    else:
        return "알 수 없음"
```

```python
sentiment = convert_label(label)
print("감정:", sentiment)
```

### 5.6 함수로 만들기

```python
def analyze_sentiment(text, classifier):
    result = classifier(text)

    label = result[0]["label"]
    score = result[0]["score"]

    if label == "LABEL_0":
        sentiment = "부정"
    elif label == "LABEL_1":
        sentiment = "긍정"
    else:
        sentiment = "알 수 없음"

    return {
        "label": sentiment,
        "confidence": score
    }
```

```python
result = analyze_sentiment(text, classifier)
print(result)
```

이 함수는 다음과 같은 딕셔너리를 반환한다.

```python
{
    "label": "긍정",
    "confidence": 0.98
}
```

### 5.7 기사 본문에 적용하기

CSV에서 읽은 기사들이 `articles` 리스트에 들어 있다고 가정한다.

```python
for article in articles:
    result = analyze_sentiment(
        article["body"],
        classifier
    )

    article["ai_result"] = result
```

이제 각 기사 딕셔너리에 AI 분석 결과가 추가된다.

---

## 6. 긴 본문 처리

기사 본문 전체가 너무 길면 모델이 처리하지 못할 수 있다. 처음에는 본문 일부만 사용하여 테스트할 수 있다.

```python
text = article_body[:2000]
```

하지만 앞부분만 사용하면 기사 후반의 결론이나 반론이 빠질 수 있다. 본문을 여러 조각으로 나누는 방법도 있다.

```python
def split_text(text, size=500):
    chunks = []

    for i in range(0, len(text), size):
        chunks.append(text[i:i + size])

    return chunks
```

본문을 나누면 각 조각을 따로 분석할 수 있지만, 조각 사이의 문맥이 끊길 수 있다는 한계가 있다.

---

## 7. 네 명의 기능 분담

| 담당 | 기능 |
|---|---|
| 1 | CSV 파일 읽기와 기사 데이터 확인 |
| 2 | 감정어휘 사전과 점수 계산 |
| 3 | AI 모델 호출과 결과 정리 |
| 4 | 언론사별 평균·비율 계산과 그래프 |

각 기능은 함수로 만든다. 모든 사람은 다음 내용을 기록한다.

- 내가 만든 함수의 입력과 출력
- AI에게 보낸 질문
- AI가 만든 코드에서 수정한 부분
- 테스트 입력과 결과
- 오류와 해결 방법
- 분석 결과의 한계

---

## 8. 함수 구조

```python
def load_articles(file_path):
    pass


def calculate_dictionary_score(
    text,
    positive_words,
    negative_words
):
    pass


def analyze_with_ai(text, classifier):
    pass


def calculate_media_average(articles, media_name):
    pass


def visualize_results(result):
    pass
```

`pass`는 아직 함수 내용을 작성하지 않았을 때 임시로 넣는 문법이다. 각 함수의 이름과 입력·출력 형식을 먼저 약속한 뒤, 담당 기능을 구현한다.

---

## 9. AI에게 코드 요청하기

완성된 프로그램 전체를 한 번에 요청하지 않는다. 담당 함수 하나를 구체적으로 요청한다.

```text
나는 고등학교 사회복지 데이터 분석 프로젝트에서 다음 함수를 담당하고 있다.

프로젝트 주제:
언론사별 사회복지 기사 본문 감정 분석

담당 기능:
기사 본문을 입력받아 감정어휘 사전 기반 점수를 계산하는 함수

함수 이름:
calculate_dictionary_score

입력:
text: 기사 본문 문자열
positive_words: 긍정 단어 리스트
negative_words: 부정 단어 리스트

출력:
정수형 감정 점수

조건:
긍정 단어가 등장할 때마다 1점을 더하고,
부정 단어가 등장할 때마다 1점을 뺀다.

요청:
파이썬 함수로 작성하고, 코드의 흐름과 테스트 결과를 설명해줘.
```

AI 모델을 사용하는 경우에는 다음을 요청할 수 있다.

```text
한국어 기사 본문을 transformers pipeline으로 분석하는 파이썬 코드를 작성해줘.

모델 결과의 자료형과 리스트·딕셔너리 구조를 설명하고,
긴 본문을 입력할 때 발생할 수 있는 문제와
사회복지 뉴스에 특화되지 않은 모델을 사용할 때의 한계도 설명해줘.
```

---

## 10. 분석할 때 주의할 점

감정지수가 높다고 좋은 언론사라는 뜻은 아니다. 감정지수가 낮다고 나쁜 언론사라는 뜻도 아니다.

다음과 같이 표현한다.

> 분석한 기간과 표본 안에서 해당 언론사의 기사 본문에 특정 감정 표현이 상대적으로 많이 나타났다.

다음과 같은 결론은 피한다.

- 이 언론사는 항상 부정적이다.
- 이 언론사는 편향되었다.
- AI가 언론사의 성향을 정확히 판정했다.

분석 결과와 함께 다음의 한계도 설명한다.

- 기사 표본이 충분하지 않을 수 있다.
- 모델의 학습 분야가 사회복지 뉴스가 아닐 수 있다.
- 문맥, 반어, 부정 표현을 정확히 처리하지 못할 수 있다.
- 감정지수만으로 기사 전체의 보도 관점을 설명할 수 없다.

---

## 오늘의 확인 활동

짧은 기사 본문 3~6개를 이용해 다음을 확인한다.

1. 감정어휘 사전 점수를 계산한다.
2. AI 모델 결과를 확인한다.
3. 사람이 읽고 판단한 결과를 적는다.
4. 세 결과가 일치하는지 비교한다.
5. 결과가 다른 문장을 하나 찾아 이유를 추측한다.

오늘의 핵심 질문은 다음과 같다.

> 사람이 정한 감정 단어 방식과 AI 모델의 결과는 왜 다를 수 있는가?

> AI 모델의 결과를 어느 범위까지 믿을 수 있는가?
