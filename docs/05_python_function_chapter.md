# 5장. 함수(Function)

## 🧭 학습 목표

* **함수가 왜 필요한지**, 어떤 상황에서 사용하는지 이해한다.
* 함수를 **정의하고 호출**하는 방법을 익힌다.
* 함수의 다양한 활용법(기본값, 가변 인자, 반환 등)을 **직접 실습**한다.
* 작은 문제를 함수로 나누어 **구조화된 프로그램**을 만드는 기초를 다진다.

## 📚 5장 전체 구성

| 단원   | 제목                         | 주요 내용          | 설명 방식       |
| ---- | -------------------------- | -------------- | ----------- |
| 5-1  | 함수란 무엇인가?                  | 함수 개념, 필요성     | 실생활 비유 중심   |
| 5-2  | 함수 정의와 호출                  | `def`, 호출법     | 이름 짓기부터     |
| 5-3  | 매개변수와 인자                   | 전달값 사용법        | 다양한 전달 방식   |
| 5-4  | 기본값 인자 / 키워드 인자            | 선택적 입력, 순서 바꾸기 | 친숙한 예시 활용   |
| 5-5  | return과 반환값                | 계산 결과 돌려주기     | 출력 vs 반환 비교 |
| 5-6  | 여러 개 값 반환                  | 튜플 언패킹 활용      | 사칙연산, 좌표 예시 |
| 5-7  | 변수의 범위                     | 지역변수, 전역변수     | `global` 포함 |
| 5-8  | 가변 인자 (\*args, \*\*kwargs) | 유동적 인자 받기      | 리스트처럼 다루기   |
| 5-9  | lambda 함수                  | 한 줄 함수 표현      | 정렬, map 예시  |
| 5-10 | 실습: BMI 계산기                | 함수 쪼개서 설계      | 입력-계산-출력 분리 |
| 5-11 | 실습: 메뉴 기반 프로그램             | 은행, 계산기 등      | 함수 분리 종합 응용 |

## 🧾 5-1. 함수란 무엇인가?

### 📌 실생활에서 생각해보기

**"라면 끓이기"를 예로 들어볼게요.**

1. 물을 끓인다
2. 스프와 면을 넣는다
3. 3분 기다린다
4. 완성!

이처럼 **정해진 순서대로 실행되는 '작업 묶음'**이 바로 **함수(Function)**입니다.

> ✅ **함수란:**
> **여러 줄의 코드를 하나의 이름으로 묶어 놓은 것**

### ✅ 함수가 필요한 이유

| 상황                    | 코드 사용 방식           |
| --------------------- | ------------------ |
| 1. 같은 코드를 여러 번 써야 할 때 | 코드 복붙 ❌ → 함수로 묶기 ✅ |
| 2. 코드가 너무 길어서 복잡할 때   | 기능별로 함수로 나누기 ✅     |
| 3. 다른 사람이 보기 쉽게 하려면   | 의미 있는 이름의 함수로 정리 ✅ |

### 📌 함수의 기본 구조

```python
def 함수이름():
    실행할 코드들
```

```python
def say_hello():
    print("안녕하세요!")
    print("반갑습니다.")
```

> `def`는 define(정의하다)의 줄임말입니다.

### ✅ 함수 호출하기

```python
say_hello()
say_hello()
```

결과:
```
안녕하세요!
반갑습니다.
안녕하세요!
반갑습니다.
```

함수를 **정의만 해놓고 부르지 않으면 실행되지 않습니다.**

### 🧪 실습 1: 자기소개 함수 만들기

```python
def introduce():
    print("이름: 홍길동")
    print("사는 곳: 서울")
    print("직업: 개발자")

introduce()
```

## 🧾 5-2. 함수 정의와 호출

### 📌 함수 정의 (기본형)

```python
def 함수이름():
    실행할 코드
```

예시:
```python
def greet():
    print("안녕하세요!")
```

### 📌 함수 호출 (사용하기)

```python
greet()  # 실행됨
```

> 함수는 **정의만 해서는 실행되지 않으며**,
> 반드시 **호출(call)** 해야 동작합니다.

### 📌 인자(Argument) 전달하기

함수에 **외부에서 값을 넘겨줄 수 있습니다.**

```python
def greet(name):
    print(f"{name}님, 안녕하세요!")
```

```python
greet("홍길동")
greet("성춘향")
```

결과:
```
홍길동님, 안녕하세요!
성춘향님, 안녕하세요!
```

### ✅ 함수 구성 요소 다시 정리

| 요소              | 설명               | 예시             |
| --------------- | ---------------- | -------------- |
| `def`           | 함수 정의 키워드        | `def greet():` |
| 함수 이름           | 호출 시 사용할 이름      | `greet`        |
| 매개변수(Parameter) | 함수 안에서 사용할 변수 이름 | `name`         |
| 인자(Argument)    | 호출할 때 전달하는 실제 값  | `"홍길동"`        |
| `()`            | 전달값과 실행 구분       | `greet("홍길동")` |

### 🧪 실습 2: 이름과 나이를 받아 인사하기

```python
def introduce(name, age):
    print(f"안녕하세요! 저는 {name}이고, {age}살입니다.")

introduce("이몽룡", 20)
introduce("임꺽정", 35)
```

### ✅ 인자의 수와 순서 주의

```python
def calc(a, b):
    print(a + b)

calc(10, 20)       # 30
calc(20)           # ❌ TypeError (인자 부족)
```

## 🧾 5-3. 매개변수와 인자의 다양한 사용법

### 📌 1. 위치 인자 (Positional Argument)

> 인자를 **순서대로** 매개변수에 대응

```python
def calc_total(price, count):
    print("총 가격:", price * count)

calc_total(3000, 2)   # 순서 중요
```

✅ `price = 3000`, `count = 2`로 전달됨

### 📌 2. 기본값 인자 (Default Argument)

> **기본값이 지정된 인자**는 생략 가능

```python
def greet(name, message="반가워요"):
    print(f"{name}님, {message}")

greet("홍길동")                 # 기본값 사용
greet("성춘향", "오랜만이네요")   # 직접 전달
```

✅ **기본값이 있는 인자는 뒤에** 배치해야 합니다.

```python
# ❌ 오류 발생
# def greet(message="반가워요", name): ...
```

### 📌 3. 키워드 인자 (Keyword Argument)

> 인자의 **이름을 명시해서** 전달

```python
def order(menu, size):
    print(f"{size} 사이즈 {menu} 주문 완료")

order(size="Large", menu="아메리카노")  # 순서 무관
```

✅ 가독성이 높아지고, 실수 방지

### ✅ 3가지 사용 비교 예시

```python
def introduce(name, age=20, job="학생"):
    print(f"이름: {name}, 나이: {age}, 직업: {job}")

introduce("이몽룡")                               # 기본값 사용
introduce("성춘향", 17)                           # 일부만 지정
introduce(name="임꺽정", job="도적", age=35)       # 키워드 인자
```

### 🧪 실습 3: 메뉴 주문 함수 만들기

```python
def order_menu(food, count=1):
    print(f"{food} {count}개 주문 완료")

order_menu("김밥")              # 기본값 적용
order_menu("떡볶이", 3)         # 위치 인자
order_menu(count=2, food="라면") # 키워드 인자
```

## 🧾 5-4. `return`과 반환값

### 📌 `return`이란?

> 함수가 **계산한 결과를 밖으로 보내주는 문법**

```python
def add(a, b):
    return a + b
```

* `add(3, 5)`는 결과 `8`을 반환함
* 반환값은 **함수 바깥에서 변수에 저장하거나 다른 연산에 사용** 가능

### ✅ `print()` vs `return` 차이

| 구분        | 목적        | 결과 사용 가능성      |
| --------- | --------- | -------------- |
| `print()` | 화면에 보여주기용 | ❌ 다른 연산에 사용 불가 |
| `return`  | 결과값을 돌려줌  | ✅ 다른 변수에 저장 가능 |

### ✅ 예시 비교

```python
def say_hello():
    print("안녕하세요!")   # 출력만 함

def get_hello():
    return "안녕하세요!"  # 결과를 돌려줌

say_hello()             # 그냥 인사만 나옴
msg = get_hello()
print(msg)              # 안녕하세요!
```

### ✅ return이 함수 실행을 멈추는 순간

```python
def check(x):
    if x > 0:
        return "양수"
    print("이건 절대 실행 안 됨")

print(check(3))  # 양수
```

### ✅ return이 없는 함수는?

* 자동으로 `None`을 반환합니다.

```python
def no_return():
    print("출력만 해요")

result = no_return()
print(result)  # None
```

### 🧪 실습 4: 계산 결과 반환

```python
def multiply(x, y):
    return x * y

result = multiply(3, 4)
print("결과:", result)
```

## 🧾 5-5. 여러 개 값 반환하기

### 📌 여러 값을 한 번에 반환

```python
def get_position():
    return 100, 200
```

이렇게 반환하면 실제로는 **튜플**로 반환됩니다:

```python
pos = get_position()
print(pos)         # (100, 200)
print(type(pos))   # <class 'tuple'>
```

### ✅ 튜플 언패킹(Unpacking)

```python
x, y = get_position()
print("x 좌표:", x)
print("y 좌표:", y)
```

> 반환된 튜플의 값을 변수 여러 개로 **한 번에 분리**할 수 있습니다.

### ✅ 실용 예: 사칙연산 함수

```python
def calc(a, b):
    return a + b, a - b, a * b, a / b

plus, minus, mul, div = calc(10, 2)
print("합:", plus)
print("차:", minus)
print("곱:", mul)
print("나눗셈:", div)
```

### ✅ 조건에 따라 다른 값 반환

```python
def min_max(a, b):
    if a < b:
        return a, b
    else:
        return b, a

small, big = min_max(7, 3)
print("작은 값:", small)
print("큰 값:", big)
```

### 🧪 실습 5: 입력값에 따라 통계값 반환

```python
def summary(numbers):
    return sum(numbers), max(numbers), min(numbers)

nums = [5, 8, 3, 9, 1]
total, maximum, minimum = summary(nums)
print(f"총합: {total}, 최댓값: {maximum}, 최솟값: {minimum}")
```

## 🧾 5-6. 변수의 범위 (Scope)

### 📌 지역변수(Local Variable)

> 함수 **안에서 선언된 변수**
> 함수가 끝나면 **사라짐**

```python
def greet():
    message = "안녕!"   # 지역변수
    print(message)

greet()
# print(message)  # ❌ 오류: 함수 밖에서는 message를 모름
```

### 📌 전역변수(Global Variable)

> 함수 **밖에서 선언된 변수**
> 프로그램 전체에서 사용 가능

```python
nickname = "길동이"

def say_hi():
    print("안녕하세요,", nickname)

say_hi()  # 안녕하세요, 길동이
```

✅ 함수 안에서는 전역변수를 **읽는 건 가능**

### 📌 전역변수 수정은 `global` 키워드 필요

```python
counter = 0

def increase():
    global counter
    counter += 1

increase()
print("카운터:", counter)  # 1
```

> `global` 없이 수정하면 에러 또는 **지역변수로 덮어씀**

### ✅ 전형적인 실수 예

```python
total = 0

def add(num):
    total = total + num  # ❌ 에러: 참조 전에 total을 수정함

add(5)
```

🔧 해결:
```python
def add(num):
    global total
    total += num
```

### 🧪 실습 6: 지역변수 vs 전역변수 차이 확인

```python
msg = "Hello"  # 전역변수

def change_msg():
    msg = "Hi"  # 지역변수 (전역 msg와 다름)
    print("함수 안:", msg)

change_msg()
print("함수 밖:", msg)
```

출력:
```
함수 안: Hi
함수 밖: Hello
```

### 🧪 실습 7: 전역 변수 누적기

```python
total = 0

def add(n):
    global total
    total += n

add(5)
add(3)
print("총합:", total)  # 8
```

## 🧾 5-7. 가변 인자와 키워드 인자

### 📌 `*args` : 개수가 정해지지 않은 **위치 인자**

```python
def show_names(*args):
    print("이름 목록:")
    for name in args:
        print("-", name)

show_names("홍길동", "이몽룡", "성춘향")
```

✅ `args`는 **튜플(tuple)**처럼 동작합니다.

### 📌 응용: 합계 계산기

```python
def total(*numbers):
    print("총합:", sum(numbers))

total(10, 20, 30)  # 총합: 60
```

### 📌 `**kwargs` : 개수가 정해지지 않은 **키워드 인자**

```python
def show_profile(**kwargs):
    print("회원 정보:")
    for key, value in kwargs.items():
        print(f"{key}: {value}")

show_profile(name="홍길동", age=30, job="도적")
```

✅ `kwargs`는 **딕셔너리(dict)**처럼 동작합니다.

### 📌 함께 쓰는 순서

함수 정의 시 순서는 꼭 다음과 같이!

```python
def 함수명(고정인자, 기본값인자, *args, **kwargs):
    ...
```

✅ 고정 → 기본값 → 위치 가변 → 키워드 가변 순서

### 🧪 실습 8: 쇼핑 장바구니

```python
def shopping_cart(*items):
    print("장바구니 목록:")
    for i, item in enumerate(items, 1):
        print(f"{i}. {item}")

shopping_cart("우유", "빵", "딸기")
```

### 🧪 실습 9: 회원 가입 정보

```python
def register_user(**info):
    print("가입한 정보:")
    for key in info:
        print(f"{key}: {info[key]}")

register_user(name="이몽룡", email="lee@test.com", age=21)
```

## 🧾 5-8. `lambda` 함수 (익명 함수)

### 📌 lambda 함수란?

> **간단한 함수**를 **한 줄**로 표현할 수 있는 방식
> 이름을 따로 정의하지 않고 **즉석에서 만드는 함수**

### ✅ 기본 구조

```python
lambda 매개변수: 표현식
```

> `return`은 사용하지 않음 — **표현식의 결과가 자동 반환됩니다**

### ✅ 일반 함수와 비교

```python
def add(a, b):
    return a + b

# 동일한 기능을 하는 lambda 함수
add_lambda = lambda a, b: a + b

print(add(3, 5))         # 8
print(add_lambda(3, 5))  # 8
```

### ✅ 실용 예: 정렬 기준

```python
students = [("홍길동", 90), ("이몽룡", 80), ("성춘향", 95)]

# 점수 기준으로 정렬
students.sort(key=lambda x: x[1])
print(students)
```

### ✅ 실용 예: map, filter, sorted

```python
numbers = [1, 2, 3, 4, 5]

# 제곱값으로 변환
squares = list(map(lambda x: x * x, numbers))
print(squares)  # [1, 4, 9, 16, 25]
```

### 🧪 실습 10: 홀짝 판별 함수 (lambda)

```python
is_even = lambda x: x % 2 == 0

print(is_even(4))  # True
print(is_even(5))  # False
```

### 🧪 실습 11: 문자열 길이로 정렬

```python
words = ["hi", "apple", "go", "banana"]

words.sort(key=lambda x: len(x))
print(words)  # ['hi', 'go', 'apple', 'banana']
```

## 🧾 5-9. 실습 예제 – BMI 계산기

### 🎯 목표

* `입력 → 계산 → 결과 해석`을 **함수로 나누어 구현**
* 함수 간 **협업**(호출 관계) 경험

### ✅ ① BMI 공식

> **BMI = 체중(kg) ÷ (키(m)²)**

### ✅ ② 함수 나누기

1. `calc_bmi(weight, height)` → BMI 계산
2. `interpret_bmi(bmi)` → 해석 문자열 반환
3. `run()` → 전체 흐름 제어

### ✅ 예제 코드

```python
def calc_bmi(weight, height_cm):
    height_m = height_cm / 100
    bmi = weight / (height_m ** 2)
    return round(bmi, 2)

def interpret_bmi(bmi):
    if bmi >= 25:
        return "과체중입니다."
    elif bmi >= 18.5:
        return "정상 체중입니다."
    else:
        return "저체중입니다."

def run():
    height = float(input("키(cm)를 입력하세요: "))
    weight = float(input("몸무게(kg)를 입력하세요: "))
    bmi = calc_bmi(weight, height)
    print(f"BMI 지수: {bmi}")
    print(interpret_bmi(bmi))

run()
```

### ✅ 실행 예시

```
키(cm)를 입력하세요: 170
몸무게(kg)를 입력하세요: 65
BMI 지수: 22.49
정상 체중입니다.
```

### 🧪 도전 과제

* BMI 수치에 따라 이모지 출력 추가하기
* 여러 사람 BMI를 반복해서 측정하는 기능 추가

## 🧾 5-10. 실습 예제 – 은행 계좌 시뮬레이터

### 🎯 기능 요구사항

* 입금
* 출금
* 잔액 조회
* 프로그램 종료

### ✅ ① 전역 변수 선언

```python
balance = 0  # 잔액 저장용 변수
```

### ✅ ② 각 기능별 함수 정의

```python
def deposit(amount):
    global balance
    balance += amount
    print(f"{amount}원이 입금되었습니다. 현재 잔액: {balance}원")

def withdraw(amount):
    global balance
    if amount > balance:
        print("잔액이 부족합니다.")
    else:
        balance -= amount
        print(f"{amount}원이 출금되었습니다. 현재 잔액: {balance}원")

def check_balance():
    print(f"현재 잔액은 {balance}원입니다.")
```

### ✅ ③ 실행 메뉴 함수

```python
def run_bank():
    while True:
        print("\n📋 은행 메뉴")
        print("1. 입금")
        print("2. 출금")
        print("3. 잔액 조회")
        print("4. 종료")
        choice = input("번호를 선택하세요: ")

        if choice == "1":
            amt = int(input("입금할 금액: "))
            deposit(amt)
        elif choice == "2":
            amt = int(input("출금할 금액: "))
            withdraw(amt)
        elif choice == "3":
            check_balance()
        elif choice == "4":
            print("프로그램을 종료합니다.")
            break
        else:
            print("잘못된 입력입니다.")
```

### ✅ 프로그램 실행

```python
run_bank()
```

### 💬 실행 예시

```
📋 은행 메뉴
1. 입금
2. 출금
3. 잔액 조회
4. 종료
번호를 선택하세요: 1
입금할 금액: 10000
10000원이 입금되었습니다. 현재 잔액: 10000원
```

### 🧪 도전 과제 (선택 실습)

* 출금 제한 (ex: 1회 10만원 이상 불가)
* 출금 이력 저장 리스트 만들기
* 사용자 이름을 입력받아 각 사용자별 잔액 관리 (`dict`로 확장)

## ✅ 5장 마무리 요약

| 핵심 개념               | 설명             |
| ------------------- | -------------- |
| 함수 정의               | `def 함수명():`   |
| 매개변수/인자             | 함수에 전달되는 값     |
| 기본값/키워드 인자          | 유연한 입력 방식      |
| return              | 함수 결과 반환       |
| 여러 값 반환             | 튜플로 묶어서 돌려주기   |
| 전역/지역 변수            | 변수의 유효 범위 구분   |
| `*args`, `**kwargs` | 유동적인 인자 받기     |
| lambda 함수           | 한 줄 표현 함수      |
| 실습                  | BMI, 은행 프로그램 등 |