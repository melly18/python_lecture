:::writing
# Python 기초 2회차

## 목표

이번 시간에는 단순 문법을 넘어서  
여러 기능을 조합하여 “하나의 프로그램”을 만드는 방법을 익힌다.

- 반복문을 더 정확하게 이해하고 제어할 수 있다  
- 함수를 사용하여 코드를 구조적으로 작성할 수 있다  
- 리스트와 딕셔너리를 함께 활용할 수 있다  
- 문자열을 가공할 수 있다  
- 파일을 읽고 데이터를 처리할 수 있다  

---

# 1. 반복문 심화

## for문과 range() 정확히 이해하기

```python
for i in range(5):
    print(i)
```

이 코드는 0부터 4까지 출력된다.  
헷갈릴 수 있는 부분: 왜 5까지가 아닌 4까지인가?

range(5)는 “0부터 시작해서 5 바로 전까지”를 의미한다.  
즉, range(n)은 항상 n-1까지.

---

## range의 다양한 형태

```python
range(시작, 끝)
```

```python
for i in range(1, 5):
    print(i)
```

이 코드는 1, 2, 3, 4를 출력한다.  
끝 숫자는 포함되지 않는다.

---

```python
range(시작, 끝, 간격)
```

```python
for i in range(0, 10, 2):
    print(i)
```

이 코드는 0, 2, 4, 6, 8을 출력한다.  
간격(증가량)을 직접 설정할 수 있다.

---

## 리스트와 함께 사용하는 for문

```python
scores = [80, 90, 100]

for s in scores:
    print(s)
```

이 방식은 range 없이 리스트의 값을 하나씩 꺼내는 방법이다.  

---

## while문 복습

```python
x = 0

while x < 5:
    print(x)
    x += 1
```

while문은 조건이 참인 동안 계속 반복된다.  
조건이 거짓이 되는 순간 반복이 종료된다.

---

## break (반복 중단)

```python
for i in range(10):
    if i == 5:
        break
    print(i)
```

반복 도중 break를 만나면 즉시 반복문이 종료된다.  
즉, 5 이후의 값은 아예 실행되지 않는다.

---

## continue (건너뛰기)

```python
for i in range(5):
    if i == 2:
        continue
    print(i)
```

continue는 반복을 멈추는 것이 아니라,  
“현재 한 번만 건너뛰고 다음 반복으로 넘어가는 것”이다.

---

## while문에서 break 활용

```python
while True:
    text = input("종료하려면 exit 입력: ")

    if text == "exit":
        break

    print("입력:", text)
```

while True는 무한 반복을 의미한다.  
이 경우 break가 없으면 프로그램이 끝나지 않는다.

---

## 실전 예제: 합계 구하기

```python
total = 0

for i in range(1, 6):
    total += i

print(total)
```

이 코드는 1부터 5까지의 합을 구한다.  
total이라는 변수를 이용해 값을 계속 누적하는 방식이다.


---

# 2. 함수 (Function)

## 함수가 필요한 이유

지금까지는 코드를 위에서부터 순서대로 작성했다.  
하지만 코드가 길어지면 다음과 같은 문제가 생긴다.

- 같은 코드를 여러 번 반복하게 된다  
- 읽기가 어려워진다  
- 수정이 힘들어진다  

함수는 이런 문제를 해결하기 위해  
“코드를 하나의 기능 단위로 묶는 방법”이다.

---

## 기본 구조

```python
def 함수이름(매개변수):
    실행 코드
    return 결과
```

매개변수는 함수에 전달되는 값이고,  
return은 함수가 결과를 돌려주는 역할을 한다.

---

## 예제 1

```python
def greet(name):
    print(name + "님 안녕하세요")

greet("민수")
```

이 함수는 이름을 받아서 인사 문장을 출력한다.  
같은 기능을 여러 번 사용할 수 있다는 점이 중요하다.

---

## 예제 2 (return)

```python
def add(a, b):
    return a + b

result = add(10, 20)
print(result)
```

return이 있으면 결과를 변수에 저장할 수 있다.  
이렇게 하면 계산 결과를 다른 곳에서도 사용할 수 있다.

---

## 예제 3 (조건 포함)

```python
def check_even(num):
    if num % 2 == 0:
        return "짝수"
    else:
        return "홀수"

print(check_even(5))
```

함수 안에서도 if문을 사용할 수 있다.  
즉, 함수는 “작은 프로그램”이라고 생각하면 된다.


---

# 3. 리스트 복습

## 리스트 기본 개념

```python
numbers = [1, 2, 3, 4, 5]
```

리스트는 여러 개의 데이터를 하나로 묶어서 저장하는 자료형이다.

---

## 인덱스

```python
print(numbers[0])
```

리스트는 0번부터 시작한다.  
즉, numbers[0]은 첫 번째 값이다.

---

## 값 추가

### -append

```python
numbers = [1, 2, 3]
numbers.append(4)
print(numbers)
```

결과:

```text
[1, 2, 3, 4]
```

append를 사용하면 리스트의 맨 뒤에 한 개의 값을 추가할 수 있다.

### -extend

```python
numbers = [1, 2, 3]
numbers.extend([4, 5])
print(numbers)
```

결과:

```text
[1, 2, 3, 4, 5]
```

extend는 리스트를 이어붙인다.
즉, 여러 개의 값을 한 번에 추가할 수 있다.

### -append vs extend

```python
numbers = [1, 2, 3]
numbers.append([4, 5])
print(numbers)
```

결과:

```text
[1, 2, 3, [4, 5]]
```

```python
numbers = [1, 2, 3]
numbers.extend([4, 5])
print(numbers)
```

결과:

```text
[1, 2, 3, 4, 5]
```

append는 하나의 값을 넣고,
extend는 리스트를 풀어서 넣는다.


### -insert

```python
numbers = [1, 2, 3]
numbers.insert(1, 10)
print(numbers)
```

결과:

```text
[1, 10, 2, 3]
```

insert는 원하는 위치에 값을 넣을 때 사용한다.

### - + 연산자

```python
numbers = [1, 2, 3]
numbers = numbers + [4]
print(numbers)
```

결과:

```text
[1, 2, 3, 4]
```

이 방법은 기존 리스트를 수정하는 것이 아니라,
새로운 리스트를 만들어서 다시 저장하는 방식이다.


---

## 반복문 활용

```python
for n in numbers:
    print(n)
```

리스트에 있는 값들을 하나씩 꺼내서 사용할 수 있다.

---

## 리스트 합계

```python
total = 0

for n in numbers:
    total += n

print(total)
```

이 방식은 이후 데이터 분석에서도 계속 사용된다.

---

# 4. 딕셔너리 (Dictionary)

## 개념

딕셔너리는 데이터에 이름(키)을 붙여 저장하는 방식이다.

```python
student = {
    "name": "민수",
    "score": 90
}
```

리스트가 “순서 기반”이라면  
딕셔너리는 “이름 기반”이라고 보면 된다.

---

## 값 사용

```python
print(student["name"])
```

key를 통해 원하는 값을 가져온다.

---

## 값 추가 / 수정

```python
student["age"] = 17
student["score"] = 95
```

없는 key를 넣으면 추가,  
이미 있으면 수정된다.

---

## 반복문

```python
for key in student:
    print(key, student[key])
```

딕셔너리의 모든 데이터를 확인할 때 사용한다.

```pyhon
for key, value in student.items():
	print(key, value)
```

items()를 사용하면 key와 value를 동시에 얻을 수 있다.

---

# 5. 리스트 + 딕셔너리 함께 사용

## 왜 중요한가

실제 프로그램에서는  
“여러 개의 구조화된 데이터”를 다루게 된다.

이때 가장 많이 쓰는 형태가 리스트 안에 딕셔너리를 넣는 구조이다.

---

## 예제

```python
students = [
    {"name": "민수", "score": 90},
    {"name": "영희", "score": 80},
    {"name": "철수", "score": 70}
]
```

이 구조는 “학생 여러 명”을 표현한다.

---

## 데이터 접근

```python
for s in students:
    print(s["name"], s["score"])
```

리스트에서 하나 꺼내고 → 딕셔너리에서 값 꺼내기  
이 2단 구조를 이해하는 것이 중요하다.

---

## 평균 구하기

```python
total = 0

for s in students:
    total += s["score"]

print(total / len(students))
```

len은 list나 dictionary의 원소 개수를 알려주는 함수다.

len(students)는 리스트의 개수를 알려준다.

---

# 6. 문자열 다루기

## 문자열 기본

```python
text = "Hello Python"
```

문자열은 텍스트 데이터를 의미한다.

---

## 자주 사용하는 함수

```python
print(len(text))
```

문자열의 길이를 구한다.

```python
print(text.upper())
print(text.lower())
```

대문자 / 소문자로 변환한다.

```python
print(text.replace("Python", "AI"))
```

특정 단어를 다른 단어로 바꾼다.

---

## 나누기 (split)

```python
data = "apple banana orange"
words = data.split()
```

문자열을 공백 기준으로 나누어 리스트로 만든다.


```python
data = "apple,banana,orange"
words = data.split(",")
print(words)
```

괄호 안에 문자를 넣으면 그 문자를 기준으로 나눌 수 있다.

---

## 포함 여부 확인

```python
text = "I like Python"

print("Python" in text)
```

특정 단어가 포함되어 있는지 확인한다.
결과는 bool 값으로 나온다.

---

# 7. 파일 입출력

## 왜 필요한가

프로젝트에서는 데이터를 직접 입력하는 것이 아니라  
파일에서 읽어오는 경우가 많다.

예: 설문 결과, CSV 데이터 등

---

## 파일 열기와 읽기

```python
f = open("data.txt", "r")
data = f.read()
print(data)
f.close()
```

파일을 열고 → 읽고 → 닫는 구조이다.

---

## 더 안전한 방법 (with)

```python
with open("data.txt", "r") as f:
    data = f.read()
    print(data)
```

with를 사용하면 파일을 자동으로 닫아준다.

---

## 한 줄씩 읽기

```python
with open("data.txt", "r") as f:
    for line in f:
        print(line)
```

파일을 한 줄씩 처리할 때 사용한다.

---

## 파일 쓰기

```python
with open("output.txt", "w") as f:
    f.write("Hello Python")
```

새로운 파일을 만들거나 내용을 덮어쓴다.

---

## 예제: 숫자 합 구하기

파일 내용이 다음과 같다고 가정하자:

```
10
20
30
```

```python
total = 0

with open("data.txt", "r") as f:
    for line in f:
        total += int(line)

print(total)
```

각 줄을 숫자로 변환해서 더한다.

---

# 8. 종합 미니 프로젝트

## 주제: 학생 데이터 분석 프로그램

이번 프로젝트에서는 지금까지 배운 내용을 모두 활용하여  
간단한 “데이터 처리 프로그램”을 만든다.

---

## 해야 할 기능

1. 사용자로부터 학생 이름과 점수를 입력받는다  
2. 입력받은 데이터를 리스트 + 딕셔너리 형태로 저장한다  
3. 전체 학생의 평균 점수를 계산한다  
4. 가장 점수가 높은 학생을 찾는다  

---

## 데이터 구조 예시

```python
students = [
    {"name": "민수", "score": 90},
    {"name": "영희", "score": 80}
]
```

이 구조를 직접 만들어야 한다.

---

## 구현 힌트

- 반복문을 사용하여 여러 학생 입력받기  
- 딕셔너리를 만들어 리스트에 추가하기  
- 함수로 평균 계산 기능 만들기  

---

## 출력 예시 (참고)

```
평균 점수: 85
최고 점수 학생: 민수 (90점)
```

---

## 도전 과제

- 특정 점수 이상 학생만 출력하기  
- 이름으로 학생 검색하기  
- 등급(A/B/C) 추가하기  

---

# 정리

이번 시간 핵심:

- range와 반복문 정확히 이해하기  
- break / continue로 흐름 제어  
- 함수로 코드 구조화  
- 리스트 + 딕셔너리 결합  
- 문자열 처리  
- 파일 입출력  

이제 “데이터를 다루는 프로그램”을 만들 준비가 된 상태이다.
:::

---
