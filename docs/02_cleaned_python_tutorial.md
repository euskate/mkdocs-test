# Python 기초 - 2장 정리

[TOC]

## 🧾 2-1. 주석(Comment)과 코드 흐름

### 📌 주석이란?

> 주석은 **프로그램에 대한 설명을 적는 문장**으로,
> **실행되지 않는 코드**입니다.

- **사람은 읽지만, 컴퓨터는 무시**합니다.
- **abc**def
- 협업, 복습, 유지보수에 필수적인 요소입니다.

### ✅ 한 줄 주석: `#` 사용

```python
# 이것은 한 줄 주석입니다
print("Hello!")  # 출력 문장
```

### ✅ 여러 줄 주석: `''' '''` 또는 `""" """`

```python title="test1.py"
'''
이 부분은 여러 줄 주석입니다.
프로그램 설명이나 예시 등에 사용합니다.
'''
print("Hello, Python!") # (1)!
print(1) # (2)!
```

1. 테스트테스트
2. 테테

> 여러 줄 주석은 사실은 **문자열 리터럴**이지만,
> 변수에 저장되지 않으면 주석처럼 동작합니다.

### ✅ 주석 사용 시점 예시

1. 함수/코드 블록 설명
2. 디버깅 시 코드 잠깐 꺼두기
3. TODO, 수정할 부분 표시

```python
# TODO: 에러 처리 로직 추가 예정
```

### 🧪 실습 1: 자기소개 주석 작성

```python
# 이름, 나이, 관심사 출력 프로그램

print("이름: 홍길동")
print("나이: 25")
print("관심사: 인공지능")
```

✅ **목표:** 주석 작성과 코드 설명 구분하기

---

## 🧾 2-2. 변수란 무엇인가?

### 📌 변수(Variable)란?

> 데이터를 저장할 수 있는 **이름이 붙은 상자**

- 메모리 공간에 값을 저장하고,
  그 공간에 이름을 붙여 **나중에 재사용**할 수 있도록 하는 것

```python
name = "홍길동"
age = 25
```

- `"홍길동"`이라는 값을 `name`이라는 **이름에 담는다**
- `25`라는 값을 `age`라는 변수에 저장

### ✅ 변수 사용의 장점

- 값을 **한 번 저장하고 여러 번 재사용**
- **코드 의미가 명확해짐**
- 유지보수가 쉬움

예:

```python
width = 10
height = 5
area = width * height
print("넓이:", area)
```

### 📌 변수 이름 규칙

| 허용                             | 예시                           |
| -------------------------------- | ------------------------------ |
| 영문자, 숫자, 밑줄(\_) 사용 가능 | `score`, `user_name`, `value1` |
| 숫자로 시작 ❌                   | `1st_user` → ❌                |
| 공백 ❌                          | `user name` → ❌               |
| 대소문자 구분                    | `name` ≠ `Name`                |
| 예약어 사용 금지                 | `if`, `class`, `def` 등은 ❌   |

### ✅ 관례: 변수 이름 스타일

- **snake_case** 사용 권장 (소문자 + 밑줄)
  - 예: `user_name`, `max_score`
- **한글 변수**도 가능하지만, 교육 목적 외에는 권장하지 않음

### 🧪 실습 2: 변수 선언과 출력

```python
name = "이몽룡"
city = "남원"
year = 2025

print("이름:", name)
print("사는 곳:", city)
print("올해:", year)
```

### 🧪 실습 3: 잘못된 변수명 고쳐보기

```python
# 다음 변수명 중 잘못된 것은 무엇일까요?

1st_player = "홍길동"   # ❌ 숫자로 시작
user-name = "이몽룡"    # ❌ 하이픈 사용
def = "함수"            # ❌ 예약어 사용

# 올바르게 고쳐보세요:
first_player = "홍길동"
user_name = "이몽룡"
definition = "함수"
```

✅ **목표:** 변수명 규칙 숙지 + 실습

---

## 🧾 2-3. 파이썬의 기본 자료형 소개

### 📌 자료형(Data Type)이란?

> **값이 어떤 종류인지 나타내는 정보**
> 예: 정수, 실수, 글자, 참/거짓 등

```python
type(123)         # <class 'int'>
type("hello")     # <class 'str'>
type(True)        # <class 'bool'>
```

### ✅ 숫자형 (정수, 실수)

```python
a = 10          # int (정수)
b = 3.14        # float (실수)
c = -100
```

연산 가능:

```python
print(a + b)    # 13.14
print(a * 2)    # 20
print(b // 1)   # 3.0 (정수 나눗셈)
```

### ✅ 문자열 (str)

```python
text1 = "Hello"
text2 = 'Python'
```

- 문자열은 `""` 또는 `''`로 묶음
- 여러 줄 문자열: `""" """` 또는 `''' '''`

```python
multiline = """안녕하세요
여러 줄입니다"""
```

### ✅ 불형 (bool)

```python
is_adult = True
is_student = False
```

- 대문자 `True`, `False`
- 조건 비교, 논리 연산 등에서 사용

### ✅ None

```python
result = None
```

- **"아직 값이 없음"**, "비어 있음"의 의미
- 변수 초기화 시 자주 사용됨

### 🧪 실습 4: 자료형 확인하기

```python
a = 10
b = 3.14
c = "안녕"
d = True
e = None

print(type(a))  # <class 'int'>
print(type(b))  # <class 'float'>
print(type(c))  # <class 'str'>
print(type(d))  # <class 'bool'>
print(type(e))  # <class 'NoneType'>
```

✅ **목표:** `type()`으로 자료형 확인하는 법 익히기

---

## 🧾 2-4. 자료형 확인 및 형 변환

### 📌 `type()` 함수

> 변수나 값의 **자료형을 확인**하는 함수

```python
print(type(10))          # <class 'int'>
print(type("Hello"))     # <class 'str'>
print(type(3.14))        # <class 'float'>
```

### 📌 형 변환 (Type Casting)

파이썬에서는 `int()`, `float()`, `str()`, `bool()` 등의 함수를 이용해 **자료형을 변환**할 수 있습니다.

### ✅ 숫자형 변환

```python
print(int(3.9))     # 3
print(float(10))    # 10.0
```

- 소수 → 정수: **소수점 이하 버림**
- 정수 → 소수: `.0` 붙여 실수로 변환

### ✅ 문자열 ↔ 숫자 변환

```python
num = int("100")        # 문자열 → 정수
text = str(3.14)        # 숫자 → 문자열

print(num + 50)         # 150
print(text + "원")      # '3.14원'
```

> 문자열을 숫자로 바꿀 때는 반드시 **숫자 형식의 문자열**이어야 함

```python
int("hello")  # ❌ ValueError
```

### ✅ 불형 변환

```python
print(bool(1))        # True
print(bool(0))        # False
print(bool("안녕"))   # True
print(bool(""))       # False
```

- 숫자 `0`, 빈 문자열 `""`, `None`, 빈 리스트 `[]` → `False`
- 나머지 값들은 `True`

### 🧪 실습 5: 사용자의 나이 입력받고 계산

```python
birth_year = input("태어난 연도는? ")    # str
age = 2025 - int(birth_year)
print(f"당신의 나이는 {age}세입니다.")
```

✅ **목표:** `input()`으로 받은 문자열을 `int()`로 변환

### 🧪 실습 6: 형 변환 오류 잡기

```python
text = "10원"
# price = int(text)  # 오류 발생!

# 수정
text = "10"
price = int(text)
print(price + 5)  # 15
```

✅ **목표:** 형식이 잘못된 문자열 변환 시 오류 잡기

---

## 🧾 2-5. 문자열 인덱싱과 슬라이싱

### 📌 인덱싱(Indexing)

> 문자열의 **각 문자는 번호(인덱스)**로 접근할 수 있습니다.

- **0부터 시작**
- **음수 인덱스**로 뒤에서부터 접근 가능

```python
text = "Python"

print(text[0])    # P
print(text[1])    # y
print(text[-1])   # n (끝 문자)
print(text[-2])   # o
```

### 📌 슬라이싱(Slicing)

> 문자열에서 **일부만 잘라서 추출**

```python
text = "Hello, Python!"

print(text[0:5])   # 'Hello' (0 이상, 5 미만)
print(text[:5])    # 'Hello' (처음부터 5 이전까지)
print(text[7:])    # 'Python!' (7부터 끝까지)
print(text[-7:-1]) # 'Python' (뒤에서부터 슬라이스)
```

### 📌 [start:stop:step] 구조

```python
word = "abcdefg"
print(word[::2])     # a c e g
print(word[::-1])    # 문자열 뒤집기
```

### 🧪 실습 7: 문자열에서 원하는 글자 추출하기

```python
id_number = "990101-1234567"

print("생년월일:", id_number[:6])
print("성별 코드:", id_number[7])
```

✅ **목표:** 문자열에서 슬라이싱으로 의미 있는 정보 추출

### 🧪 실습 8: 문자열 거꾸로 출력하기

```python
text = "Python"
print(text[::-1])  # nohtyP
```

### ✅ 주의: 인덱스 범위 벗어나면 오류!

```python
text = "Hi"
print(text[10])  # IndexError
```

---

## 🧾 2-6. 문자열 연산과 포매팅

### 📌 문자열 연산

#### 🔹 덧셈 `+`

```python
greeting = "Hello, " + "Python"
print(greeting)  # Hello, Python
```

#### 🔹 곱셈 `*`

```python
print("Hi~ " * 3)  # Hi~ Hi~ Hi~
```

> 문자열을 반복하는 간단한 방법입니다.

### 📌 문자열 포매팅이란?

> **값을 문자열에 삽입**하는 방법입니다.

### ✅ ① `%` 방식 (C 스타일)

```python
name = "홍길동"
age = 25

print("이름: %s, 나이: %d" % (name, age))
```

- `%s`: 문자열
- `%d`: 정수
- `%f`: 실수

#### 🔸 소수점 자리수 지정

```python
pi = 3.141592
print("원주율은 %.2f입니다." % pi)  # 3.14
```

### ✅ ② `format()` 함수

```python
print("이름: {}, 나이: {}".format("이몽룡", 20))
print("이름: {0}, 나이: {1}".format("성춘향", 18))
```

- `{}` 안에 위치 인덱스도 지정 가능

### ✅ ③ f-string (파이썬 3.6+)

> 가장 현대적인 방식. **추천!**

```python
name = "임꺽정"
age = 30
print(f"이름: {name}, 나이: {age}")
```

### 🧪 실습 9: 자기소개 문자열 만들기

```python
name = "홍길동"
age = 25
job = "백엔드 개발자"

intro = f"안녕하세요. 저는 {name}이고, {age}살 {job}입니다."
print(intro)
```

✅ **목표:** 변수와 문자열 포매팅을 함께 사용하기

### 🧪 실습 10: 가격 정보 출력 포맷

```python
product = "노트북"
price = 1290000
print(f"{product}의 가격은 {price:,}원입니다.")  # 천 단위 콤마
```

---

## 🧾 2-7. 문자열 관련 함수들

### 📌 문자열 함수란?

> 문자열에서 사용할 수 있는 **내장 함수(메서드)** > `"문자열".함수명()` 형식으로 사용합니다.

### ✅ 대소문자 관련

```python
text = "Python Programming"

print(text.upper())   # 대문자 전체
print(text.lower())   # 소문자 전체
print(text.capitalize())  # 첫 글자만 대문자
```

### ✅ 공백 및 문자 제거

```python
text = "  hello python  "

print(text.strip())     # 양쪽 공백 제거
print(text.lstrip())    # 왼쪽 공백 제거
print(text.rstrip())    # 오른쪽 공백 제거
```

### ✅ 찾기, 포함 여부

```python
text = "banana"

print(text.find("a"))     # 1 (첫 번째 'a')
print(text.rfind("a"))    # 5 (마지막 'a')
print(text.count("a"))    # 3
print("na" in text)       # True
```

### ✅ 변경/분리/결합

```python
text = "one,two,three"

words = text.split(",")       # ['one', 'two', 'three']
joined = "-".join(words)      # 'one-two-three'

print(joined)
```

### ✅ 검사 함수

```python
"123".isdigit()     # True
"abc".isalpha()     # True
"   ".isspace()     # True
```

### 🧪 실습 11: 사용자 이름 처리

```python
name = input("이름을 입력하세요: ")  # 공백 포함 가능

# 공백 제거, 대문자 출력
cleaned = name.strip().upper()
print(f"이름 (정리됨): {cleaned}")
```

### 🧪 실습 12: 문자열 분석 도구 만들기

```python
sentence = input("문장을 입력하세요: ")

print("문장 길이:", len(sentence))
print("'a' 개수:", sentence.count("a"))
print("앞에서부터 'a' 위치:", sentence.find("a"))
print("문장 전체 대문자:", sentence.upper())
```

✅ **목표:** 여러 문자열 함수 조합 연습

---

## 🧾 2-8. 실습 예제: 자기소개 만들기

### 🎯 목표

- 변수 선언
- 문자열 포매팅(f-string)
- 문자열 함수(`upper`, `strip`, `len`) 활용

### ✅ 예시 코드

```python
name = input("이름을 입력하세요: ").strip()
age = int(input("나이를 입력하세요: "))
city = input("사는 도시를 입력하세요: ").strip()
job = input("직업을 입력하세요: ").strip()

intro = f"""
안녕하세요! 저는 {name.upper()}입니다.
나이는 {age}살이고, {city}에 살고 있습니다.
현재 직업은 {job}입니다. 반갑습니다!
"""

print(intro)
```

### 📌 응용 포인트

- `strip()`으로 입력 오류 방지
- `upper()`로 이름 강조
- `f-string`으로 가독성 좋은 출력

---

## 🧾 2-9. 실습 예제: 비밀번호 생성기

### 🎯 목표

- 문자열 처리(슬라이싱, 길이)
- 논리 연산(`in`)
- 문자열 + 숫자 조합 생성

### ✅ 문제 설명

`http://naver.com` 같은 웹사이트 주소가 주어졌을 때 다음 규칙으로 비밀번호를 만듭니다:

1. `http://` 제외 → `naver.com`
2. `.` 앞까지만 → `naver`
3. 비밀번호 = (앞 3글자) + (길이) + ('e' 포함 여부) + (길이 % 3)

### ✅ 코드 예시

```python
url = input("사이트 주소 입력 (예: http://naver.com): ")
url = url.replace("http://", "").replace("https://", "")

site_name = url.split(".")[0]
length = len(site_name)
has_e = 'e' in site_name
password = site_name[:3] + str(length) + str(has_e) + str(length % 3)

print(f"{url}의 비밀번호는 → {password}")
```

### 📌 예시 입력/출력

```
입력: http://google.com
출력: google.com의 비밀번호는 → goo6True0
```

---

## ✅ 2장 마무리 요약

| 개념        | 키워드                             | 예시               |
| ----------- | ---------------------------------- | ------------------ |
| 변수        | `=`, 이름 규칙                     | `name = "홍길동"`  |
| 자료형      | `int`, `str`, `bool`, `None`       | `type(x)`          |
| 형 변환     | `int()`, `str()`, `bool()`         | `int("10")`        |
| 문자열 처리 | 인덱싱, 슬라이싱, 포매팅           | `s[1:4]`, `f"{x}"` |
| 문자열 함수 | `strip()`, `upper()`, `count()` 등 | `s.find("a")`      |
