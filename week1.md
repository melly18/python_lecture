# Python 기초 1회차

## AI 기반 바이브 코딩 동아리

---

# ✨ 오늘의 목표

오늘 수업에서는:

* Python 코드의 기본 구조를 이해하고
* AI가 만든 코드를 읽을 수 있으며
* 간단한 오류를 해석할 수 있는 수준

까지 가는 것을 목표로 한다.

우리는 앞으로 AI와 함께 프로젝트를 진행할 예정이다.
따라서 중요한 것은:

```text
✔ 코드를 읽는 능력
✔ 오류를 이해하는 능력
✔ AI에게 질문하는 능력
```

이다.

---

# 🌐 Google Colab 사용하기

우리는 Google Colab 환경에서 Python을 실습한다.

## Colab의 장점

| 장점     | 설명                  |
| ------ | ------------------- |
| 설치 불필요 | 인터넷만 있으면 사용 가능      |
| 자동 저장  | 작업 내용 자동 저장         |
| 협업 가능  | 링크 공유 가능            |

---

# 🖥️ Colab 시작하기

## ① Colab 접속

```text
https://colab.research.google.com
```

---

## ② 새 노트북 만들기

* “새 노트” 클릭
* 코드 입력
* Shift + Enter 실행

---

# 🧪 첫 코드 실행

```python
print("Hello Python")
```

실행 결과:

```text
Hello Python
```

---

# 🖨️ print() 함수

`print()`는 화면에 결과를 출력하는 함수이다.

예시:

```python
print("안녕하세요")
```

결과:

```text
안녕하세요
```

---

# 📦 변수(Variable)

변수는 데이터를 저장하는 공간이다.

예시:

```python
name = "민수"
age = 17
height = 172.5
```

각 변수에는 서로 다른 데이터가 저장된다.

| 변수     | 저장된 값 |
| ------ | ----- |
| name   | 문자열   |
| age    | 정수    |
| height | 실수    |

---

# 🏷️ 변수 이름 규칙

가능한 예시:

```python
student_name = "민수"
score1 = 100
```

불가능한 예시:

```python
1score = 100
```

❌ 숫자로 시작할 수 없다.

---

# 🔤 자료형(Data Type)

Python에는 여러 종류의 데이터가 존재한다.

| 자료형   | 의미   | 예시        |
| ----- | ---- | --------- |
| str   | 문자열  | `"hello"` |
| int   | 정수   | `3`       |
| float | 실수   | `3.14`    |
| bool  | 참/거짓 | `True`    |

---

# 🧵 문자열(str)

문자열은 글자를 저장하는 자료형이다.

```python
name = "민수"
```

문자열은:

```python
"큰따옴표"
'작은따옴표'
```

둘 다 사용할 수 있다.

예시:

```python
text1 = "Python"
text2 = 'Python'
```

---

# ⚠️ 문자열에서 자주 하는 실수

```python
name = 민수
```

오류 발생:

```text
NameError
```

문자열인데 따옴표를 사용하지 않았기 때문이다.

---

# 🔗 문자열 연결하기

```python
first = "AI"
second = "Project"

print(first + second)
```

결과:

```text
AIProject
```

---

# ✨ 띄어쓰기 추가하기

```python
print(first + " " + second)
```

결과:

```text
AI Project
```

---

# 🔢 숫자 자료형

## 정수(int)

```python
x = 10
```

## 실수(float)

```python
pi = 3.14
```

---

# ➕ 연산자

```python
x = 10
y = 3
```

| 연산  | 코드       | 결과       |
| --- | -------- | -------- |
| 덧셈  | `x + y`  | 13       |
| 뺄셈  | `x - y`  | 7        |
| 곱셈  | `x * y`  | 30       |
| 나눗셈 | `x / y`  | 3.333... |
| 몫   | `x // y` | 3        |
| 나머지 | `x % y`  | 1        |
| 제곱  | `x ** y` | 1000     |

---

# 🔍 같은 숫자처럼 보여도 다르다

```python
x = 10
y = "10"
```

| 변수 | 자료형 |
|---|---|
| x | int |
| y | str |

```python
print(x + 1)
```

결과:

```text
11
```

하지만:

```python
print(y + 1)
```

오류 발생:

```text
TypeError
```

---

# 🖨️ print()와 문자열 + 숫자

잘못된 예시:

```python
print("나이: " + 17)
```

오류 발생:

```text
TypeError
```

이유:

* 문자열(str)
* 숫자(int)

는 바로 더할 수 없다.

---

# ✅ 해결 방법 1: 콤마 사용

```python
print("나이:", 17)
```

결과:

```text
나이: 17
```

---

# ✅ 해결 방법 2: 문자열 변환

```python
print("나이: " + str(17))
```

---

# ⌨️ input() 함수

`input()`은 사용자 입력을 받는 함수이다.

```python
name = input("이름 입력: ")
print(name)
```

---

# ⚠️ input()에서 중요한 점

입력받은 값은 기본적으로 문자열(str)이다.

```python
age = input("나이 입력: ")
print(age + 1)
```

오류 발생:

```text
TypeError
```

---

# ✅ 해결 방법

```python
age = int(input("나이 입력: "))
print(age + 1)
```

---

# ⚖️ 비교 연산자

비교 연산자는 결과가:

```python
True
False
```

로 나온다.

즉, 결과 자료형은 bool이다.

---

# 📊 비교 연산자 종류

| 연산자 | 의미     |
| --- | ------ |
| >   | 크다     |
| <   | 작다     |
| >=  | 크거나 같다 |
| <=  | 작거나 같다 |
| ==  | 같다     |
| !=  | 다르다    |

---

# 🧪 비교 연산 예시

```python
print(10 > 3)
print(5 == 5)
print(7 != 2)
```

결과:

```text
True
True
True
```

---

# 🔀 논리 연산자

논리 연산자는 여러 조건을 함께 비교한다.

| 연산자 | 의미     |
| --- | ------ |
| and | 둘 다 참  |
| or  | 하나라도 참 |
| not | 반대로 바꿈 |

---

# 🧠 논리 연산 예시

```python
age = 17
score = 85

print(age >= 15 and score >= 80)
```

결과:

```text
True
```

---

# 🌳 논리 연산 진리표

## AND 연산

|  A  |  B  |  결과 |
| :-: | :-: | :-: |
|  T  |  T  |  T  |
|  T  |  F  |  F  |
|  F  |  T  |  F  |
|  F  |  F  |  F  |

---

## OR 연산

|  A  |  B  |  결과 |
| :-: | :-: | :-: |
|  T  |  T  |  T  |
|  T  |  F  |  T  |
|  F  |  T  |  T  |
|  F  |  F  |  F  |

---

# 🚦 조건문 if

조건에 따라 다른 코드를 실행한다.

```python
score = 85

if score >= 80:
    print("합격")
```

---

# 📌 if 구조

```python
if 조건:
    실행 코드
```

중요한 것:

```text
✔ 콜론(:)
✔ 들여쓰기
```

---

# ❌ 자주 하는 실수

```python
if score >= 80
    print("합격")
```

오류 이유:

```text
콜론(:)이 없음
```

---

# 🔀 if - else 그리고 elif

```python
age = 17

if age >= 20:
    print("성인")
else:
    print("미성년자")
```

여러 가지 조건을 한 번에 처리할 수도 있다.

```python
score = 75

if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
else:
    print("F")
```

---
# if문 예제1

사용자로부터 점수를 입력받고, 다음과 같은 조건에 맞춰 학점을 출력한다.

100점이라면 "만점을 축하합니다!"출력. 90점 이상이면 A, 90점 미만 80점 이상이면 B, 80점 미만 70점 이상이면 C, 70점 미만의 점수의 경우 F를 출력한다.

input 예시:

```text
점수를 입력해 주세요: 15
```

output 예시:

```text
F
```


예시 정답 코드는 다음과 같다.

```python
score = int(input("점수를 입력해 주세요: "))

if score==100:
  print("만점을 축하합니다!")
elif score >= 90:
  print("A")
elif score >= 80:
  print("B")
elif score >= 70:
  print("C")
else:
  print("F")
```

---

# if문 예제2

상품의 등급에 따라 판매 가격이 달라지는 상품이 있다. 사용자로부터 등급을 입력 받고 상품의 가격을 출력하는 코드를 작성해 보자.

기본 가격은 1만원이다. 등급이 A라면 기본 가격의 1배를 판매 가격으로 책정한다. 등급이 B라면 기본 가격의 0.75배를 판매 가격으로 책정한다. 등급이 C라면 기본 가격의 0.5배를 판매 가격으로 책정한다. 그 외 입력은 모두 무시하며, "잘못된 입력입니다."라는 메시지를 출력한다.

input 예시:

```text
상품의 등급을 입력해 주세요: A
```

output 예시:

```text
판매 가격은 10000원입니다.
```


예시 정답 코드는 다음과 같다.

```python
origin_price = 10000

grade = input("상품의 등급을 입력해 주세요: ")

if grade == 'A':
  print("판매 가격은 "+str(int(origin_price*1))+"원입니다.")
elif grade == 'B':
  print("판매 가격은 "+str(int(origin_price*0.75))+"원입니다.")
elif grade == 'C':
  print("판매 가격은 "+str(int(origin_price*0.5))+"원입니다.")
else:
  print("잘못된 입력입니다.")
```

---

# 🔁 반복문 for

반복문은 같은 작업을 여러 번 수행한다.

```python
for i in range(5):
    print(i)
```

결과:

```text
0
1
2
3
4
```

---

# 📌 range() 이해하기

```python
range(5)
```

의미:

```text
0부터 4까지
```

---

# 🔄 반복문 활용

```python
for i in range(3):
    print("안녕하세요")
```

---

# ♾️ while 반복문

조건이 참인 동안 계속 반복한다.

```python
x = 0

while x < 5:
    print(x)
    x += 1
```

---

# ⚠️ 무한 반복 주의

```python
while True:
    print("무한 반복")
```

멈추지 않는다.

---

# 📚 리스트(List)

리스트는 여러 데이터를 저장한다.

```python
scores = [80, 90, 100]
```

---

# 📌 리스트 데이터 꺼내기

```python
print(scores[0])
```

결과:

```text
80
```

---

# 🔄 리스트와 반복문

```python
scores = [80, 90, 100]

for s in scores:
    print(s)
```


---

# for문 예제

주어진 점수 리스트의 총합을 구하는 코드를 작성하라. 점수 리스트 [10, 20, 30, 50, 100]

input 예시:

```text
없음
```

output 예시:

```text
210
```


예시 정답 코드는 다음과 같다.

```python
score = [10,20,30,50,100]
sum = 0

for i in score:
  sum += i

print(sum)
```


---

# 구구단 출력 예제

사용자로부터 몇 단을 출력하고 싶은지 숫자를 입력받는다. 그 후 해당 구구단을 출력한다.

input 예시:

```text
구구단 몇 단을 알고 싶나요? 2
```

output 예시:

```text
2x1 = 2
2x2 = 4
2x3 = 6
2x4 = 8
2x5 = 10
2x6 = 12
2x7 = 14
2x8 = 16
2x9 = 18
```


예시 정답 코드는 다음과 같다.

```python
num = int(input("구구단 몇 단을 알고 싶나요? "))

for i in range(9):
  print(str(num)+"x"+str(i+1)+" = "+str(num*(i+1)))
```

---

### 모두 수고하셨습니다!
