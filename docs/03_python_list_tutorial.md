# 3장 자료구조 - 리스트(List)

## 🧾 3-1. 리스트란?

### 📌 리스트(List)란?

> 여러 개의 값을 하나의 변수에 저장할 수 있는 자료형입니다.

- 파이썬의 가장 기본적인 자료구조
- `[]` (대괄호)를 사용해 만듭니다.
- 여러 데이터 타입이 하나의 리스트에 함께 들어갈 수 있습니다.

### 🔹 리스트 생성 예제

```python
# 숫자 리스트
numbers = [10, 20, 30]

# 문자열 리스트
fruits = ["apple", "banana", "cherry"]

# 혼합 타입 리스트
mixed = [1, "hi", True, 3.14]

# 빈 리스트
empty = []
```

### 🧪 실습 1: 좋아하는 음식 3개 리스트로 만들기

```python
# 아래 코드를 수정해보세요
my_foods = ["떡볶이", "김밥", "라면"]

print("내가 좋아하는 음식 목록:", my_foods)
```

✅ **목표:** 리스트 문법 익히기, `[]` 사용

## 🧾 3-2. 인덱싱과 슬라이싱

### 📌 인덱싱(Indexing)

> 리스트의 각 요소는 **번호(인덱스)**로 접근합니다.

- 인덱스는 0부터 시작합니다.
- 음수 인덱스도 사용 가능합니다. (`-1`은 마지막 요소)

```python
fruits = ["apple", "banana", "cherry"]
print(fruits[0])   # apple
print(fruits[-1])  # cherry
```

### 📌 슬라이싱(Slicing)

> 리스트의 일부분을 추출할 수 있습니다.

```python
numbers = [1, 2, 3, 4, 5, 6]

print(numbers[1:4])   # [2, 3, 4]
print(numbers[:3])    # [1, 2, 3]
print(numbers[3:])    # [4, 5, 6]
print(numbers[::-1])  # [6, 5, 4, 3, 2, 1]
```

### 🧪 실습 2: 인덱싱과 슬라이싱 연습

```python
colors = ["red", "orange", "yellow", "green", "blue", "indigo", "violet"]

# 색깔 중 초록색 출력
print(colors[3])

# 빨강~노랑 출력
print(colors[0:3])

# 거꾸로 출력
print(colors[::-1])
```

✅ **목표:** 인덱싱/슬라이싱을 활용한 리스트 접근

## 🧾 3-3. 리스트 요소 수정, 추가, 삭제

### 📌 리스트 요소 수정 (값 변경)

리스트는 **mutable(변경 가능)** 합니다.
인덱스를 이용하여 값을 수정할 수 있습니다.

```python
fruits = ["apple", "banana", "cherry"]
fruits[1] = "grape"
print(fruits)  # ['apple', 'grape', 'cherry']
```

### 📌 요소 추가하기

#### 🔹 `append()` : 맨 뒤에 추가

```python
nums = [1, 2]
nums.append(3)
print(nums)  # [1, 2, 3]
```

#### 🔹 `insert(index, value)` : 원하는 위치에 삽입

```python
nums = [1, 2, 4]
nums.insert(2, 3)  # 2번 인덱스에 3 삽입
print(nums)  # [1, 2, 3, 4]
```

#### 🔹 `extend()` : 여러 개 한번에 추가

```python
nums = [1, 2]
nums.extend([3, 4])
print(nums)  # [1, 2, 3, 4]
```

### 📌 요소 삭제하기

#### 🔹 `remove(value)` : 해당 값을 찾아 삭제 (하나만)

```python
fruits = ["apple", "banana", "apple"]
fruits.remove("apple")
print(fruits)  # ['banana', 'apple']
```

> ⚠️ 없는 값 삭제 시 `ValueError` 발생

#### 🔹 `pop()` : 마지막 요소 꺼내서 삭제

```python
nums = [1, 2, 3]
n = nums.pop()
print(n)      # 3
print(nums)   # [1, 2]
```

#### 🔹 `del` : 인덱스로 삭제

```python
nums = [10, 20, 30]
del nums[1]
print(nums)  # [10, 30]
```

#### 🔹 `clear()` : 모든 요소 제거

```python
nums = [1, 2, 3]
nums.clear()
print(nums)  # []
```

### 🧪 실습 3: 영화 리스트 관리하기

```python
# 영화 리스트 만들기
movies = ["Interstellar", "Inception", "Tenet"]

# 'Dunkirk' 추가
movies.append("Dunkirk")

# 'Tenet' 앞에 'Oppenheimer' 삽입
movies.insert(2, "Oppenheimer")

# 'Inception' 삭제
movies.remove("Inception")

print("최종 영화 리스트:", movies)
```

✅ **목표:** 리스트에 요소를 자유롭게 삽입, 삭제, 수정할 수 있다.

### 🧪 실습 4: 사용자 입력으로 값 추가/삭제

```python
# 초기 리스트
my_list = []

# 값 추가
item = input("리스트에 추가할 값을 입력하세요: ")
my_list.append(item)
print("리스트:", my_list)

# 삭제 시도
delete_item = input("삭제할 값을 입력하세요: ")
if delete_item in my_list:
    my_list.remove(delete_item)
else:
    print("리스트에 존재하지 않습니다.")

print("최종 리스트:", my_list)
```

✅ **목표:** `append()`, `remove()`에 사용자 입력을 연결

## 🧾 3-4. 리스트 정렬과 반전

### 📌 리스트 정렬하기

#### 🔹 `sort()` : 리스트 자체를 정렬 (기본 오름차순)

```python
numbers = [5, 3, 1, 4, 2]
numbers.sort()
print(numbers)  # [1, 2, 3, 4, 5]
```

#### 🔹 `sort(reverse=True)` : 내림차순 정렬

```python
numbers = [5, 3, 1, 4, 2]
numbers.sort(reverse=True)
print(numbers)  # [5, 4, 3, 2, 1]
```

### 📌 정렬 결과를 새로운 리스트로 : `sorted()`

```python
numbers = [4, 2, 3, 1]
sorted_numbers = sorted(numbers)
print(sorted_numbers)  # [1, 2, 3, 4]
print(numbers)         # [4, 2, 3, 1] (원본 유지)
```

### 📌 리스트 뒤집기

#### 🔹 `reverse()` : 리스트 자체 순서 뒤집기

```python
nums = [1, 2, 3]
nums.reverse()
print(nums)  # [3, 2, 1]
```

### 📌 정렬 대상이 문자열일 때

```python
words = ["banana", "apple", "cherry"]
words.sort()
print(words)  # ['apple', 'banana', 'cherry']
```

> 기본적으로 **알파벳 순서** 또는 **유니코드 순서**로 정렬됩니다.

### 🧪 실습 5: 숫자 정렬기 만들기

```python
nums = [int(n) for n in input("숫자 여러 개를 입력하세요 (공백으로 구분): ").split()]

print("오름차순 정렬:", sorted(nums))
print("내림차순 정렬:", sorted(nums, reverse=True))
```

✅ **목표:** `sorted()`와 `sort()`의 차이를 이해하고 사용해보기

### 🧪 실습 6: 좋아하는 단어 정렬하기

```python
words = []

for _ in range(3):
    w = input("좋아하는 단어를 하나 입력하세요: ")
    words.append(w)

print("입력된 단어들:", words)
print("정렬된 단어들:", sorted(words))
```

✅ **목표:** 리스트를 문자열로 정렬하는 법 연습

## 🧾 3-5. 리스트 컴프리헨션 (List Comprehension)

### 📌 리스트 컴프리헨션이란?

> 반복문을 한 줄로 간결하게 작성하여 리스트를 생성하는 문법입니다.

```python
# 일반 방식
squares = []
for i in range(1, 6):
    squares.append(i * i)

# 리스트 컴프리헨션 방식
squares = [i * i for i in range(1, 6)]
```

### 📌 기본 구조

```python
[표현식 for 변수 in 반복가능한객체]
```

#### 예시:

```python
nums = [1, 2, 3, 4, 5]
even_nums = [n for n in nums if n % 2 == 0]
print(even_nums)  # [2, 4]
```

### 🧪 실습 7: 문자열 길이 리스트 만들기

```python
words = ["apple", "banana", "cherry"]
lengths = [len(w) for w in words]
print(lengths)  # [5, 6, 6]
```

### 🧪 실습 8: 1부터 10까지의 제곱수 리스트 만들기

```python
squares = [x ** 2 for x in range(1, 11)]
print(squares)
```

✅ **목표:** 컴프리헨션 문법으로 리스트 생성

## 🧾 3-6. 종합 실습: TODO 리스트 만들기

> 리스트를 활용하여 간단한 할 일 목록 관리 프로그램을 만들어봅니다.

### 📌 기능 요구사항

- 할 일 추가
- 할 일 삭제
- 할 일 목록 출력
- 종료

### 🧪 실습 9: 메뉴 기반 TODO 리스트

```python
todo_list = []

while True:
    print("\n[ TODO LIST ]")
    print("1. 추가")
    print("2. 삭제")
    print("3. 전체 보기")
    print("4. 종료")

    choice = input("메뉴를 선택하세요: ")

    if choice == "1":
        item = input("추가할 일을 입력하세요: ")
        todo_list.append(item)
        print("추가 완료!")

    elif choice == "2":
        item = input("삭제할 일을 입력하세요: ")
        if item in todo_list:
            todo_list.remove(item)
            print("삭제 완료!")
        else:
            print("해당 항목이 리스트에 없습니다.")

    elif choice == "3":
        print("\n[ 현재 할 일 목록 ]")
        for i, task in enumerate(todo_list, 1):
            print(f"{i}. {task}")

    elif choice == "4":
        print("프로그램을 종료합니다.")
        break

    else:
        print("올바른 메뉴 번호를 입력하세요.")
```

✅ **목표:** 리스트 + 조건문 + 반복문 통합 실습

## 🧾 3-7. 튜플 (Tuple)

### 📌 튜플이란?

- **여러 값을 순서 있게 저장**할 수 있는 자료형
- 리스트와 비슷하지만, **수정할 수 없음(불변, immutable)**

```python
point = (3, 5)
colors = ("red", "green", "blue")
```

### 📌 특징 정리

| 항목            | 내용                               |
| --------------- | ---------------------------------- |
| 생성 문법       | `()` 또는 `tuple()` 사용           |
| 변경 가능 여부  | ❌ 불가능                          |
| 인덱싱/슬라이싱 | ✅ 가능                            |
| 사용 예시       | 좌표, RGB 값 등 고정된 데이터 저장 |

### 🧪 실습 10: 튜플 사용해보기

```python
info = ("홍길동", 25, "서울")
print("이름:", info[0])
print("나이:", info[1])
print("지역:", info[2])

# info[1] = 30  # TypeError: 튜플은 수정 불가
```

✅ **목표:** 튜플이 리스트와 비슷하되 변경 불가함을 이해

## 🧾 3-8. 딕셔너리 (Dictionary)

### 📌 딕셔너리란?

> `키(key):값(value)` 형태로 데이터를 저장하는 구조

```python
scores = {
    "홍길동": 90,
    "이몽룡": 85,
    "성춘향": 100
}
```

### 📌 주요 메서드

```python
scores["임꺽정"] = 70     # 값 추가
scores["홍길동"] = 95     # 값 수정
del scores["이몽룡"]      # 삭제

print(scores.get("성춘향"))  # 100
print(scores.keys())         # dict_keys(['홍길동', '성춘향', '임꺽정'])
```

### 🧪 실습 11: 연락처 관리

```python
contacts = {
    "엄마": "010-1234-5678",
    "아빠": "010-9876-5432"
}

# 연락처 조회
print("엄마 번호:", contacts.get("엄마"))

# 새 번호 추가
contacts["친구"] = "010-1111-2222"

# 삭제
del contacts["아빠"]

print("전체 연락처:", contacts)
```

✅ **목표:** 딕셔너리 기본 구조와 `get()`, 수정/삭제 이해

## 🧾 3-9. 세트 (Set)

### 📌 세트란?

> **중복을 허용하지 않고**, **순서가 없는** 자료형

```python
s = {1, 2, 3, 3, 2}
print(s)  # {1, 2, 3}
```

### 📌 주요 연산

```python
a = {1, 2, 3}
b = {3, 4, 5}

print(a | b)  # 합집합: {1, 2, 3, 4, 5}
print(a & b)  # 교집합: {3}
print(a - b)  # 차집합: {1, 2}
```

### 🧪 실습 12: 중복 제거와 집합 연산

```python
nums = [1, 2, 2, 3, 3, 4]
unique = set(nums)
print("중복 제거:", unique)

a = {"사과", "바나나", "딸기"}
b = {"딸기", "수박", "참외"}

print("공통 과일:", a & b)
```

✅ **목표:** 중복 제거 및 집합 연산 연습

## 📌 3장 전체 요약: 자료구조 비교표

| 항목      | 리스트 (List)             | 튜플 (Tuple) | 딕셔너리 (Dict)          | 세트 (Set)                |
| --------- | ------------------------- | ------------ | ------------------------ | ------------------------- |
| 문법      | `[]`                      | `()`         | `{key: value}`           | `{}`                      |
| 순서      | O                         | O            | X (단, 3.7+는 순서 유지) | X                         |
| 중복      | O                         | O            | 키 중복 불가             | X                         |
| 변경 가능 | ✅                        | ❌           | ✅                       | ✅                        |
| 특징      | 가장 많이 사용, 순서 있음 | 변경 불가    | 키로 빠르게 접근         | 중복 자동 제거, 집합 연산 |

## 🧪 실습 13: 나만의 즐겨찾기 폴더 만들기

> 내가 자주 방문하는 사이트들을 리스트로 관리하는 프로그램을 만들어보세요.

### ✨ 기능 요구사항

1. 처음에 기본 사이트 3개가 등록되어 있음
2. 메뉴를 통해 다음 기능을 선택할 수 있음
   - **1. 추가**: 새로운 사이트를 리스트에 추가
   - **2. 삭제**: 사이트 이름으로 삭제
   - **3. 정렬**: 사이트 리스트를 알파벳순으로 정렬
   - **4. 검색**: 특정 사이트가 리스트에 있는지 확인
   - **5. 전체 보기**: 현재 즐겨찾기 리스트를 모두 출력
   - **6. 종료**: 프로그램 종료

### 💻 예시 코드

```python
bookmarks = ["google.com", "naver.com", "github.com"]

while True:
    print("\n[ 즐겨찾기 관리 ]")
    print("1. 추가 | 2. 삭제 | 3. 정렬 | 4. 검색 | 5. 전체 보기 | 6. 종료")
    choice = input("메뉴 선택: ")

    if choice == "1":
        site = input("추가할 사이트 주소 입력: ")
        bookmarks.append(site)

    elif choice == "2":
        site = input("삭제할 사이트 주소 입력: ")
        if site in bookmarks:
            bookmarks.remove(site)
        else:
            print("해당 사이트는 즐겨찾기에 없습니다.")

    elif choice == "3":
        bookmarks.sort()
        print("정렬 완료!")

    elif choice == "4":
        keyword = input("검색할 사이트 이름 입력: ")
        if keyword in bookmarks:
            print(f"{keyword}는 즐겨찾기에 있습니다.")
        else:
            print(f"{keyword}는 등록되어 있지 않습니다.")

    elif choice == "5":
        print("[ 전체 즐겨찾기 목록 ]")
        for i, site in enumerate(bookmarks, 1):
            print(f"{i}. {site}")

    elif choice == "6":
        print("프로그램 종료!")
        break

    else:
        print("잘못된 메뉴입니다.")
```

✅ **학습 포인트**
- 리스트 기본 조작 능력 종합
- 사용자 입력 처리 (`input`)
- 조건문과 반복문 적용