# 4장. 흐름 제어(Control Flow)

## 학습 목표
* 프로그램의 **흐름을 분기하거나 반복**할 수 있는 조건문/반복문 사용법을 익힌다.
* 실생활의 조건과 반복을 코드로 구현하는 법을 이해한다.
* 리스트 컴프리헨션 등 고급 흐름 제어 표현도 도입한다.

## 세부 목차

| 단원 | 제목 | 주요 내용 |
|---|---|---|
| 4-1 | 흐름 제어란? | 흐름 제어의 개념, 조건문과 반복문의 차이 |
| 4-2 | `if` 조건문 | if, elif, else / 비교 연산자 / 논리 연산자 |
| 4-3 | 중첩 조건문과 들여쓰기 | 중첩된 조건문 / 파이썬 들여쓰기 문법 강조 |
| 4-4 | `input()`과 조건문 실습 | 사용자 입력 기반 조건 처리 실습 |
| 4-5 | `for` 반복문 | 기본 구조, 리스트/문자열 순회, `range()` |
| 4-6 | `while` 반복문 | 조건 기반 반복 / 무한 루프 등 |
| 4-7 | 흐름 제어 키워드 | `break`, `continue`, `pass` |
| 4-8 | 리스트 컴프리헨션 심화 | 조건부 표현, 중첩 컴프리헨션 |
| 4-9 | 종합 실습: 메뉴형 프로그램 만들기 | 조건 + 반복 통합 실습 프로젝트 |

## 4-1. 흐름 제어란?

### 프로그램의 흐름이란?
> 코드가 **위에서 아래로 차례대로 실행되는 기본 흐름**을 **조건이나 반복에 따라 제어**하는 것

### 흐름 제어의 2가지 축
* **조건문 (if)**: 조건에 따라 다른 코드를 실행
* **반복문 (for, while)**: 같은 작업을 여러 번 반복

### 예시

**흐름이 제어되지 않은 프로그램**
```python
print("1단계 완료")
print("2단계 완료")
print("3단계 완료")
```

**흐름이 제어되는 프로그램 (조건)**
```python
temperature = 30
if temperature >= 30:
    print("에어컨을 켭니다.")
```

**흐름이 제어되는 프로그램 (반복)**
```python
for i in range(3):
    print(f"{i+1}단계 완료")
```

### 실습 1: 흐름 제어 맛보기
```python
name = input("당신의 이름은? ")

if name == "홍길동":
    print("반가워요, 의적 홍길동!")
else:
    print(f"{name}님, 안녕하세요!")

print("프로그램 종료")
```

## 4-2. 조건문: `if`, `elif`, `else`

### 조건문이란?
> 조건에 따라 **코드 실행 흐름을 분기**시키는 문법입니다.

### 기본 구조
```python
if 조건:
    실행문1
elif 다른조건:
    실행문2
else:
    실행문3
```

### 들여쓰기 주의
* 파이썬은 `{}` 대신 **들여쓰기**로 코드 블록을 구분합니다.
* 일반적으로 **스페이스 4칸**이 권장됩니다.

```python
score = 85

if score >= 90:
    print("A학점")
elif score >= 80:
    print("B학점")  # ← 여기까지만 실행
else:
    print("C학점")
```

### 비교 연산자
| 연산자 | 의미 | 예시 |
|---|---|---|
| `==` | 같다 | `a == b` |
| `!=` | 같지 않다 | `a != b` |
| `>` | 크다 | `a > b` |
| `<` | 작다 | `a < b` |
| `>=` | 크거나 같다 | `a >= b` |
| `<=` | 작거나 같다 | `a <= b` |

### 논리 연산자
| 연산자 | 의미 | 예시 |
|---|---|---|
| `and` | 둘 다 참이면 참 | `a > 0 and a < 10` |
| `or` | 하나라도 참이면 참 | `a == 0 or a == 1` |
| `not` | 참/거짓 반전 | `not True` → `False` |

### 실습 2: 나이 판별기
```python
age = int(input("나이를 입력하세요: "))

if age >= 65:
    print("노년층입니다.")
elif age >= 20:
    print("성인입니다.")
elif age >= 14:
    print("청소년입니다.")
else:
    print("어린이입니다.")
```

### 실습 3: 로그인 판별기
```python
user_id = input("아이디를 입력하세요: ")
user_pw = input("비밀번호를 입력하세요: ")

if user_id == "admin" and user_pw == "1234":
    print("로그인 성공!")
else:
    print("로그인 실패!")
```

## 4-3. 중첩 조건문과 들여쓰기

### 중첩 조건문이란?
> `if`문 안에 또 다른 `if`문이 들어 있는 형태로, 조건이 **여러 단계로 분기**되는 상황에 사용합니다.

### 기본 구조
```python
if 조건1:
    if 조건2:
        실행문1
    else:
        실행문2
else:
    실행문3
```

### 예제 1: 영화 관람 가능 여부
```python
age = int(input("나이를 입력하세요: "))
has_ticket = input("티켓이 있나요? (yes/no): ")

if age >= 18:
    if has_ticket == "yes":
        print("입장 가능합니다.")
    else:
        print("티켓이 필요합니다.")
else:
    print("나이가 부족합니다.")
```

### 실습 4: 회원 등급 확인기
```python
grade = input("회원 등급을 입력하세요 (gold/silver): ")
purchase = int(input("이번 달 구매 금액을 입력하세요: "))

if grade == "gold":
    if purchase >= 100000:
        print("VIP 혜택 제공")
    else:
        print("기본 골드 혜택 제공")
else:
    print("실버 또는 일반 회원입니다.")
```

## 4-4. `input()`과 조건문 실습

### `input()` 함수 복습
```python
name = input("당신의 이름은? ")
age = int(input("나이를 입력하세요: "))  # 숫자 변환
```

### 실습 5: 숫자 맞히기 게임
```python
secret = 7
guess = int(input("1~10 사이의 숫자를 맞혀보세요: "))

if guess == secret:
    print("정답입니다!")
elif guess < secret:
    print("너무 작아요!")
else:
    print("너무 커요!")
```

### 실습 6: BMI 판별기
```python
height = float(input("키(cm): "))
weight = float(input("몸무게(kg): "))

bmi = weight / ((height / 100) ** 2)

print(f"BMI: {bmi:.2f}")

if bmi >= 25:
    print("과체중입니다.")
elif bmi >= 18.5:
    print("정상 체중입니다.")
else:
    print("저체중입니다.")
```

## 4-5. `for` 반복문

### `for` 반복문이란?
> 시퀀스(리스트, 문자열 등)의 **요소를 하나씩 꺼내며 반복**하는 문법입니다.

### 기본 구조
```python
for 변수 in 반복가능한객체:
    실행문
```

### 예시
```python
fruits = ["apple", "banana", "cherry"]

for fruit in fruits:
    print(fruit)
```

### 문자열도 반복 가능
```python
for ch in "Hello":
    print(ch)
```

### `range()` 함수
```python
for i in range(5):
    print(i)  # 0, 1, 2, 3, 4
```

```python
for i in range(1, 10, 2):
    print(i)  # 1, 3, 5, 7, 9
```

### 실습 7: 구구단 출력기
```python
dan = int(input("출력할 단 입력 (2~9): "))

for i in range(1, 10):
    print(f"{dan} x {i} = {dan * i}")
```

### 실습 8: 리스트 요소와 인덱스 함께 출력
```python
menu = ["떡볶이", "김밥", "순대"]

for i in range(len(menu)):
    print(f"{i+1}. {menu[i]}")
```

또는:
```python
for idx, item in enumerate(menu, 1):
    print(f"{idx}. {item}")
```

## 4-6. `while` 반복문

### `while`문이란?
> 주어진 **조건이 참(`True`)인 동안 계속해서 반복** 실행하는 문법입니다.

### 기본 구조
```python
while 조건:
    실행문
```

### 예시
```python
count = 1
while count <= 5:
    print(f"{count}번째 출력")
    count += 1
```

### `while` vs `for`
| 특징 | `for` 문 | `while` 문 |
|---|---|---|
| 반복 조건 | 반복 횟수가 명확할 때 | 조건이 만족하는 동안 |
| 제어 방식 | 반복 가능한 객체에 대해 반복 | 조건을 직접 검사 |
| 종료 조건 | 범위가 끝나면 자동 종료 | 조건이 `False`가 되어야 종료 |

### 실습 9: 비밀번호 입력 반복
```python
correct_pw = "1234"

while True:
    pw = input("비밀번호를 입력하세요: ")
    if pw == correct_pw:
        print("접속 성공!")
        break
    else:
        print("틀렸습니다. 다시 시도하세요.")
```

### 실습 10: 1부터 n까지의 합 구하기
```python
n = int(input("숫자를 입력하세요: "))
total = 0
i = 1

while i <= n:
    total += i
    i += 1

print(f"1부터 {n}까지의 합은 {total}")
```

## 4-7. 흐름 제어 키워드

### ① `break`
> 반복문을 **강제로 종료**시킬 때 사용합니다.

```python
while True:
    word = input("단어 입력 (종료하려면 exit 입력): ")
    if word == "exit":
        break
    print(f"입력한 단어: {word}")
```

### ② `continue`
> 반복문 안에서 **다음 반복으로 건너뜁니다.**

```python
for i in range(1, 6):
    if i == 3:
        continue
    print(i)  # 1, 2, 4, 5
```

### ③ `pass`
> **아무것도 하지 않고 넘어감**. 문법적으로 코드 블록이 필요한 자리에 임시로 사용.

```python
score = 80

if score >= 90:
    print("A등급")
elif score >= 80:
    pass  # 아직 처리할 코드 없음
else:
    print("C등급")
```

### 실습 11: 짝수만 출력하기
```python
for i in range(1, 11):
    if i % 2 != 0:
        continue
    print(i)
```

### 실습 12: 첫 번째로 30 이상인 숫자 찾기
```python
nums = [10, 20, 25, 32, 40, 50]

for n in nums:
    if n >= 30:
        print(f"30 이상인 첫 수: {n}")
        break
```

## 4-8. 리스트 컴프리헨션 심화

### 복습: 기본 형태
```python
[표현식 for 변수 in 반복가능한객체]
```

```python
squares = [x * x for x in range(1, 6)]
print(squares)  # [1, 4, 9, 16, 25]
```

### 조건부 리스트 컴프리헨션
```python
even_nums = [x for x in range(1, 11) if x % 2 == 0]
print(even_nums)  # [2, 4, 6, 8, 10]
```

### 삼항 연산자 활용
```python
labels = ["짝수" if x % 2 == 0 else "홀수" for x in range(1, 6)]
print(labels)  # ['홀수', '짝수', '홀수', '짝수', '홀수']
```

### 중첩 반복 (2중 for문)
```python
pairs = [(x, y) for x in [1, 2] for y in ['a', 'b']]
print(pairs)  # [(1, 'a'), (1, 'b'), (2, 'a'), (2, 'b')]
```

### 실습 13: 문자열 길이 3 이상만 필터링
```python
words = ["hi", "hello", "안녕", "python", "go"]
long_words = [w for w in words if len(w) >= 3]
print(long_words)  # ['hello', '안녕', 'python']
```

### 실습 14: 구구단 (2~4단) 곱셈 쌍 만들기
```python
pairs = [(dan, i) for dan in range(2, 5) for i in range(1, 10)]
for dan, i in pairs:
    print(f"{dan} x {i} = {dan * i}")
```

## 4-9. 종합 실습: 메뉴 기반 프로그램

### 실습 15: 명언 저장소 만들기
```python
quotes = []

while True:
    print("\n==== 명언 저장소 ====")
    print("1. 추가")
    print("2. 목록 보기")
    print("3. 삭제")
    print("4. 종료")
    choice = input(">> ")

    if choice == "1":
        new_quote = input("추가할 명언: ")
        quotes.append(new_quote)

    elif choice == "2":
        if not quotes:
            print("아직 등록된 명언이 없습니다.")
        else:
            for i, q in enumerate(quotes, 1):
                print(f"[{i}] {q}")

    elif choice == "3":
        num = int(input("삭제할 번호: "))
        if 1 <= num <= len(quotes):
            removed = quotes.pop(num - 1)
            print(f"삭제됨: {removed}")
        else:
            print("유효하지 않은 번호입니다.")

    elif choice == "4":
        print("프로그램을 종료합니다.")
        break

    else:
        print("1~4 사이의 숫자를 입력하세요.")
```

## 4장 마무리 요약

| 주제 | 핵심 내용 요약 |
|---|---|
| 조건문 | if, elif, else / 비교 & 논리 연산자 |
| 반복문 (for) | 리스트, 문자열, range, enumerate |
| 반복문 (while) | 조건 반복, 무한 루프, break |
| 흐름 제어 키워드 | break, continue, pass |
| 리스트 컴프리헨션 | 표현식 + 조건 필터링 |
| 실습 종합 | 조건 + 반복 + 입력/출력 통합 사용 |