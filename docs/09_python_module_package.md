# 9장. 모듈과 패키지

## 학습 목표

* 코드가 많아지면 기능별로 **파일을 나누는 구조화**가 필요함을 이해
* 모듈과 패키지를 이용해 **코드를 나누고 불러오는 법**을 익힌다
* `import`, `from ... import`, `as`, `__name__ == "__main__"` 문법을 이해한다
* **내장 모듈**, **외부 모듈(pip)**, **사용자 정의 모듈** 모두 사용할 수 있게 한다
* 실습을 통해 실제로 **나만의 유틸 모듈**을 만들어 활용해본다

## 9-1. 모듈이란?

### 모듈의 정의와 필요성

모듈(Module)은 파이썬 코드가 담긴 `.py` 파일입니다. 코드가 많아지면 기능별로 파일을 나누는 구조화가 필요합니다.

## 9-2. 모듈 불러오기

### 모듈을 불러오는 기본 문법

| 방법                  | 예시                      | 설명            |
| ------------------- | ----------------------- | ------------- |
| `import 모듈명`        | `import math`           | 전체 불러오기       |
| `import 모듈명 as 별칭`  | `import math as m`      | 별명으로 간편하게     |
| `from 모듈 import 함수` | `from math import sqrt` | 특정 함수만 불러오기   |
| `from 모듈 import *`  | `from math import *`    | 전부 불러오기 (권장❌) |

### 예제 1: `import` 기본

```python
import math

print(math.sqrt(25))     # 5.0
print(math.pi)           # 3.1415...
```

### 예제 2: `import ... as` (별명)

```python
import math as m

print(m.sqrt(16))        # 4.0
```

### 예제 3: `from ... import ...`

```python
from math import sqrt, pi

print(sqrt(9))           # 3.0
print(pi)                # 3.1415...
```

### 예제 4: `from ... import *`

```python
from math import *

print(sin(pi / 2))       # 1.0
```

> 모든 함수가 import되지만, **이름 충돌 위험이 있어 권장되지 않음**

### 💬 ChatGPT에게 물어볼 질문

> **"`import`와 `from import` 중 어떤 걸 더 자주 쓰나요? 실무에서는?"**

## 9-3. 사용자 정의 모듈 만들기

### 사용자 정의 모듈이란?

내가 만든 `.py` 파일을 모듈처럼 불러와 사용하는 것입니다.

✅ 조건: **같은 폴더 안에 있어야 한다** (또는 `sys.path`에 등록)

### 1단계: `calc.py` 만들기

```python
# calc.py

def add(a, b):
    return a + b

def sub(a, b):
    return a - b

def mul(a, b):
    return a * b

def div(a, b):
    return a / b
```

### 2단계: `main.py`에서 사용하기

```python
# main.py

import calc

print(calc.add(2, 3))   # 5
print(calc.mul(4, 5))   # 20
```

### 3단계: `from` 방식도 사용 가능

```python
from calc import add, div

print(add(10, 5))  # 15
print(div(10, 2))  # 5.0
```

### 4단계: 별칭으로 간결하게

```python
import calc as c

print(c.sub(9, 3))  # 6
```

### 실습: `greeting.py` 만들기

```python
# greeting.py

def hello(name):
    print(f"안녕하세요, {name}님!")

def bye(name):
    print(f"{name}님, 안녕히 가세요.")
```

```python
# main.py
import greeting

greeting.hello("홍길동")
greeting.bye("홍길동")
```

출력:
```
안녕하세요, 홍길동님!
홍길동님, 안녕히 가세요.
```

### 💬 ChatGPT에게 물어볼 질문

> **"모듈을 여러 개로 나누면 import 순서나 충돌 문제가 생기지 않나요?"**

## 9-4. 모듈의 실행 확인: `__name__ == "__main__"`

### 목적

어떤 `.py` 파일이 **직접 실행되는 경우**와 **다른 파일에서 import된 경우**를 **구분**하는 조건문입니다.

```python
if __name__ == "__main__":
    # 직접 실행될 때만 이 코드를 실행
```

### 예제: `mytool.py`

```python
# mytool.py

def hello():
    print("안녕하세요!")

if __name__ == "__main__":
    print("✅ 직접 실행 중입니다.")
    hello()
```

#### 경우 ①: 직접 실행

```bash
$ python mytool.py
✅ 직접 실행 중입니다.
안녕하세요!
```

#### 경우 ②: 다른 파일에서 import

```python
# main.py
import mytool
```

출력 결과:
```
(아무것도 출력되지 않음)
```

### 응용 예: `calculator.py`

```python
def add(a, b):
    return a + b

def sub(a, b):
    return a - b

if __name__ == "__main__":
    print("테스트:", add(2, 3))  # 5
```

→ `import calculator` 하면 테스트 코드는 실행되지 않음

### 💬 ChatGPT에게 물어볼 질문

> **"`__name__`이라는 건 누가 정해주는 건가요? 직접 바꿀 수 있나요?"**

## 9-5. 패키지란?

### 패키지(Package)란?

관련 있는 모듈들을 **폴더 단위로 묶은 것**입니다.

✅ 폴더 안에 `.py` 모듈 파일들이 들어 있고  
✅ 반드시 `__init__.py` 파일이 존재해야 **"이 폴더는 패키지입니다"** 라고 인식됨

### 패키지 기본 구조 예시

```
mypackage/               ← 패키지 (폴더)
├── __init__.py          ← 패키지 초기화용 파일 (비워도 됨)
├── calc.py              ← 덧셈, 뺄셈
├── greeting.py          ← 인사 기능
```

### 사용 예시

#### 1단계: 폴더 구성

```text
project/
├── main.py
└── mypackage/
    ├── __init__.py
    ├── calc.py
    └── greeting.py
```

#### 2단계: 모듈 작성

```python
# mypackage/calc.py
def add(a, b):
    return a + b
```

```python
# mypackage/greeting.py
def hello(name):
    print(f"안녕하세요, {name}님!")
```

#### 3단계: `main.py`에서 import

```python
# main.py

from mypackage import calc, greeting

print(calc.add(2, 3))        # 5
greeting.hello("홍길동")      # 안녕하세요, 홍길동님!
```

또는 모듈별로 직접 불러올 수도 있습니다:

```python
from mypackage.calc import add
print(add(10, 5))  # 15
```

### `__init__.py`는 뭐하는 파일인가요?

해당 폴더가 "파이썬 패키지입니다"라는 표시입니다. 파일 내부는 비워도 되고, 초기 설정을 할 수도 있습니다.

```python
# mypackage/__init__.py
print("mypackage가 불러와졌습니다.")
```

→ import 시 한 번 출력됨

### 💬 ChatGPT에게 물어볼 질문

> **"패키지 안에 또 패키지를 넣을 수 있나요? (중첩 패키지)"**

## 9-6. 패키지 사용법

### 예제 폴더 구조

```
project/
├── main.py
└── mypkg/
    ├── __init__.py
    ├── calc.py
    └── greeting.py
```

### import 방법 ①: 모듈 전체 import

```python
from mypkg import calc, greeting

calc.add(3, 5)
greeting.hello("홍길동")
```

### import 방법 ②: 모듈 내 함수만 import

```python
from mypkg.calc import add
from mypkg.greeting import hello

print(add(2, 3))        # 5
hello("이몽룡")          # 안녕하세요, 이몽룡님!
```

### import 방법 ③: as로 별명 붙이기

```python
import mypkg.calc as c

print(c.add(10, 20))
```

또는 함수 단위 별명:

```python
from mypkg.calc import add as plus

print(plus(5, 6))
```

### 패키지 내부에서 다른 모듈 사용하기

```python
# mypkg/greeting.py
from . import calc

def greet_with_sum(a, b, name):
    result = calc.add(a, b)
    print(f"{name}님, 계산 결과는 {result}입니다.")
```

* `from . import 모듈명` → 같은 패키지 안에서 import
* `.`은 현재 패키지 위치를 의미 (상대 경로 import)

### 💬 ChatGPT에게 물어볼 질문

> **"패키지 안에 있는 모듈끼리 서로 불러오려면 어떻게 해야 하나요?"**

## 9-7. 내장 모듈 소개

### 내장 모듈이란?

파이썬이 기본적으로 제공하는 모듈들입니다.

* 설치 불필요
* import만 하면 바로 사용 가능

### 주요 내장 모듈

| 모듈         | 설명      | 대표 기능                   |
| ---------- | ------- | ----------------------- |
| `math`     | 수학 계산   | `sqrt()`, `pi`, `sin()` |
| `random`   | 난수 생성   | `randint()`, `choice()` |
| `datetime` | 날짜/시간   | `now()`, `strftime()`   |
| `os`       | 운영체제 접근 | 파일 경로, 디렉터리             |
| `sys`      | 시스템 정보  | 경로, 종료, argv            |
| `time`     | 시간 관련   | `sleep()`, 시간 측정        |

### 예제 1: `datetime`

```python
import datetime

now = datetime.datetime.now()
print("현재 시각:", now)
print("연도:", now.year)
print("포맷:", now.strftime("%Y-%m-%d %H:%M"))
```

### 예제 2: `random`

```python
import random

print("1~10 무작위 정수:", random.randint(1, 10))
print("랜덤 선택:", random.choice(["홍길동", "이몽룡", "성춘향"]))
```

### 예제 3: `os` – 파일 시스템 다루기

```python
import os

print("현재 작업 폴더:", os.getcwd())
os.mkdir("연습폴더")     # 폴더 만들기
os.rename("연습폴더", "테스트")  # 이름 바꾸기
os.remove("파일이름.txt")       # 파일 삭제
```

### 예제 4: `sys` – 파이썬 실행 관련 정보

```python
import sys

print("실행 인자:", sys.argv)
print("파이썬 경로:", sys.executable)
# sys.exit()  # 강제 종료
```

### 예제 5: `time` – 시간 지연

```python
import time

print("3초 후 시작")
time.sleep(3)
print("시작!")
```

### 활용 예제: 프로그램 실행 시간 측정

```python
import time

start = time.time()

# 실행할 코드
for i in range(1000000):
    pass

end = time.time()

print("실행 시간:", end - start)
```

### 💬 ChatGPT에게 물어볼 질문

> **"내장 모듈 외에 외부 모듈은 어떻게 설치해서 쓰나요?"**

## 9-8. 외부 모듈 사용하기

### 외부 모듈이란?

파이썬 기본에 포함되어 있지 않지만, 다른 개발자들이 만들어서 **공개한 라이브러리**입니다.

* 예: `requests`, `openpyxl`, `pandas`, `pyperclip`, `beautifulsoup4`, `flask` 등
* 설치 도구: **`pip`** (Python Package Installer)

### pip 기본 명령어

| 명령어                  | 설명           |
| -------------------- | ------------ |
| `pip install 모듈명`    | 모듈 설치        |
| `pip uninstall 모듈명`  | 모듈 삭제        |
| `pip list`           | 설치된 모듈 목록 확인 |
| `pip show 모듈명`       | 설치된 모듈 정보 확인 |
| `pip install 모듈==버전` | 특정 버전 설치     |

### 예제 1: pyperclip (클립보드 복사/붙여넣기)

#### 설치

```bash
pip install pyperclip
```

#### 사용 예

```python
import pyperclip

pyperclip.copy("안녕하세요!")        # 클립보드에 복사
text = pyperclip.paste()            # 클립보드에서 붙여넣기
print("복사된 내용:", text)
```

### 예제 2: requests (웹 요청)

```bash
pip install requests
```

```python
import requests

res = requests.get("https://httpbin.org/get")
print("응답 상태:", res.status_code)
print("본문:", res.text)
```

### 외부 모듈 `Faker` 사용하기

#### Faker란?

다양한 국가의 **가짜 이름, 주소, 이메일, 회사명, 전화번호 등**을 생성해주는 외부 라이브러리입니다.

#### 설치 방법

```bash
pip install Faker
```

#### 기본 사용 예시

```python
from faker import Faker

fake = Faker(locale="ko_KR")  # 한국어 설정

print(fake.name())         # 예: 이민준
print(fake.address())      # 예: 서울특별시 강남구 ...
print(fake.email())        # 예: soyoung22@example.net
print(fake.phone_number()) # 예: 010-1234-5678
```

#### 다양한 더미 데이터 생성

```python
print(fake.company())       # 회사명
print(fake.job())           # 직업
print(fake.date_of_birth()) # 생년월일
print(fake.text())          # 임의의 문장
print(fake.ssn())           # 주민등록번호 형식
```

#### 여러 개 생성하기

```python
for _ in range(5):
    print(fake.name(), "-", fake.phone_number())
```

#### 구조화된 테스트 데이터 만들기

```python
def create_user():
    return {
        "이름": fake.name(),
        "이메일": fake.email(),
        "주소": fake.address(),
        "전화번호": fake.phone_number()
    }

for _ in range(3):
    print(create_user())
```

### 💬 ChatGPT에게 물어볼 질문

> **"외부 모듈이 충돌날 수 있다던데, 그건 어떻게 관리하나요?"**

> **"Faker에서 사용자 지정 패턴으로 전화번호나 ID를 만들 수 있나요?"**

## 9-9. 실습: 나만의 유틸리티 모듈 만들기

### 목표

* 자주 사용하는 기능을 **모듈로 분리**
* 다른 파일에서 **재사용 가능**하도록 구성
* 함수, 상수, 메시지 등을 하나로 묶음

### Step 1. `util.py` 만들기

```python
# util.py

def print_header(title):
    print("=" * 40)
    print(f"📌 {title}")
    print("=" * 40)

def calc_area(width, height):
    return width * height

def format_price(price):
    return f"{price:,}원"  # 10000 → "10,000원"
```

### Step 2. `main.py`에서 사용

```python
import util

util.print_header("면적 계산기")

w = int(input("가로 길이: "))
h = int(input("세로 길이: "))

area = util.calc_area(w, h)
print(f"넓이: {area}㎡")
```

출력 예시:
```
========================================
📌 면적 계산기
========================================
가로 길이: 5
세로 길이: 3
넓이: 15㎡
```

### Step 3. 패키지로 구성해 보기

```
project/
├── main.py
└── myutil/
    ├── __init__.py
    ├── printutil.py
    ├── calcutil.py
```

```python
# printutil.py
def print_title(text):
    print(f"===== {text} =====")
```

```python
# calcutil.py
def add(a, b):
    return a + b
```

```python
# main.py
from myutil import printutil, calcutil

printutil.print_title("유틸 테스트")
print("덧셈:", calcutil.add(2, 3))
```

### 💬 ChatGPT에게 물어볼 질문

> **"모듈을 만들어두면 나중에 어떤 프로젝트에서도 쉽게 쓸 수 있나요?"**

## 9장 마무리 요약

| 구분        | 키워드                                 |
| --------- | ----------------------------------- |
| 모듈        | `.py` 파일 (import해서 사용)              |
| 패키지       | 모듈을 묶은 폴더 (`__init__.py`)           |
| import    | `import`, `from`, `as`, `*`         |
| 사용자 정의 모듈 | 직접 만든 함수 모음 파일                      |
| 내장 모듈     | math, random, os, sys, datetime 등   |
| 외부 모듈     | pip로 설치 (`requests`, `pyperclip` 등) |
| 실습        | 나만의 util 모듈/패키지 구성 및 활용             |

### 핵심 개념 키워드

* `import`, `from ... import`, `as`, `__name__`
* 모듈(module), 패키지(package), 내장 모듈, 외부 모듈
* 사용자 정의 모듈, `pip install`, `__init__.py`

### 예제 중심 주제 흐름

* `math` 모듈 → 제곱근, 삼각함수
* `random` 모듈 → 당첨자 뽑기
* 사용자 정의 모듈 → 계산기 유틸, 메시지 유틸
* 패키지 구조로 나누기
* `pip`로 설치한 `pyperclip` 사용 → 클립보드 복사