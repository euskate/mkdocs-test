# 8장. 예외 처리 (Exception Handling)

## 학습 목표

* 프로그램 실행 중 예상치 못한 오류(예외)를 **우아하게 처리**하는 방법을 익힌다.
* `try`, `except`, `finally`, `raise`의 정확한 의미를 이해하고 사용할 수 있다.
* 예외 처리로 **프로그램이 멈추지 않도록** 만들고, **오류 메시지를 사용자 친화적으로 출력**할 수 있다.

## 8-1. 예외란 무엇인가?

### 예외(Exception)란?

> 프로그램 실행 도중 **의도치 않게 발생하는 문제 상황**
> → 이를 파이썬에서는 **"예외(Exception)"** 라고 부릅니다.

* 프로그램을 멈추게 만들 수 있는 **특별한 상황**
* 예외는 **잡아서 처리할 수 있습니다** (에러는 시스템 수준에서 해결이 필요함)

### 예외 vs 에러

| 구분                | 설명                      | 예시                         |
| ----------------- | ----------------------- | -------------------------- |
| **에러(Error)**     | 치명적인 오류. 프로그램을 종료시킴     | 문법 오류, 메모리 오류 등            |
| **예외(Exception)** | 실행 중 발생하는 오류. **처리 가능** | 나누기 0, 잘못된 인덱스, 없는 파일 읽기 등 |

### 예외 발생 예시

#### 1. 0으로 나누기 (`ZeroDivisionError`)

```python
print(10 / 0)  # 예외 발생
```

#### 2. 숫자가 아닌 값 입력 (`ValueError`)

```python
num = int(input("숫자를 입력하세요: "))  # 문자열 입력 시 예외 발생
```

#### 3. 존재하지 않는 인덱스 (`IndexError`)

```python
lst = [1, 2, 3]
print(lst[5])  # 범위를 벗어남
```

### 예외 처리가 필요한 이유

* 사용자의 실수로 **입력이 잘못될 수 있음**
* 외부 환경(파일, 네트워크 등)은 **항상 예측 불가능**
* 예외가 발생해도 **프로그램을 계속 실행할 수 있도록** 하기 위함

### 현실 비유

> **ATM 기기**: 카드가 잘못 꽂혀도 "다시 넣어주세요" 라고 안내하죠?
> → 프로그램도 이런 **"안전 장치"**가 필요합니다.

### 💬 ChatGPT에게 물어볼 질문

> **"숫자 검사에 if도 쓰는데, 왜 try-except가 더 필요한가요?"**

## 8-2. try-except 기본 구조

### 예외 처리란?

> 예외가 발생할 수 있는 코드를 `try` 블록에 넣고,
> 문제가 생겼을 때 `except` 블록에서 **대비하는 방식**입니다.

### 기본 구조

```python
try:
    # 문제가 생길 수 있는 코드
except 예외종류:
    # 예외 발생 시 처리할 코드
```

### 예제: 0으로 나누기 방지

```python
try:
    num = int(input("숫자를 입력하세요: "))
    result = 10 / num
    print("결과:", result)

except ZeroDivisionError:
    print("❗ 0으로 나눌 수 없습니다.")
```

### 흐름도

```text
[try 시작]
 ├─ 정상 실행 → except 생략
 └─ 예외 발생 → 해당 except 블록 실행
```

> 예외가 발생하지 않으면 `except`는 무시됩니다.

### 예외 종류에 따라 분기 가능

```python
try:
    num = int(input("숫자 입력: "))
    print(10 / num)

except ValueError:
    print("❗ 숫자가 아닌 값을 입력했습니다.")

except ZeroDivisionError:
    print("❗ 0으로 나눌 수 없습니다.")
```

### 모든 예외를 한꺼번에 처리하려면?

```python
try:
    ...
except Exception:
    print("❗ 문제가 발생했습니다.")
```

> 여러 종류의 예외가 예상될 때 **일괄 처리용**으로 사용 가능
> (단점: 어떤 예외인지 구체적으로 알 수 없음)

### `else`: 예외가 없을 때만 실행되는 코드

```python
try:
    num = int(input("정수 입력: "))
except ValueError:
    print("숫자가 아닙니다.")
else:
    print(f"{num}은 정수입니다.")
```

### 실습: 사용자 입력 처리 예제

```python
try:
    age = int(input("나이를 입력하세요: "))
    print(f"당신은 {age}살입니다.")
except ValueError:
    print("❗ 숫자로 입력해주세요.")
```

### 💬 ChatGPT에게 물어볼 질문

> **"except에 아무 예외도 안 쓰면 모든 예외를 잡나요? 그게 좋은가요?"**

## 8-3. 다양한 예외 유형 처리하기

### 파이썬의 자주 발생하는 예외들

| 예외 종류               | 설명         | 예시 상황            |
| ------------------- | ---------- | ---------------- |
| `ValueError`        | 잘못된 값 입력   | `int("abc")`     |
| `ZeroDivisionError` | 0으로 나눔     | `10 / 0`         |
| `IndexError`        | 리스트 범위 초과  | `lst[10]`        |
| `KeyError`          | 딕셔너리에 없는 키 | `dic['없는키']`     |
| `FileNotFoundError` | 없는 파일 열기   | `open("없음.txt")` |
| `TypeError`         | 타입 불일치 연산  | `"문자열" + 5`      |

### 예제 1: 리스트 인덱스 오류

```python
lst = [10, 20, 30]

try:
    print(lst[5])
except IndexError:
    print("❗ 존재하지 않는 인덱스입니다.")
```

### 예제 2: 딕셔너리 키 오류

```python
student = {"name": "홍길동", "age": 20}

try:
    print(student["grade"])
except KeyError:
    print("❗ 없는 키입니다.")
```

### 예제 3: 없는 파일 열기

```python
try:
    f = open("not_exist.txt", "r")
except FileNotFoundError:
    print("❗ 파일을 찾을 수 없습니다.")
```

### 예제 4: 타입 오류

```python
try:
    print("나이: " + 30)
except TypeError:
    print("❗ 문자열과 숫자는 더할 수 없습니다.")
```

> 이럴 땐 `str(30)`으로 형변환을 해줘야 합니다.

### 여러 예외를 함께 처리

```python
try:
    num = int(input("숫자 입력: "))
    print(10 / num)

except (ValueError, ZeroDivisionError) as e:
    print("❗ 예외 발생:", e)
```

* 괄호로 묶어서 **여러 예외를 동시에 처리**할 수 있음
* `as e`를 사용하면 **에러 메시지 확인도 가능**

### 실습: 계산기 입력 오류 처리

```python
try:
    n1 = int(input("첫 번째 숫자: "))
    n2 = int(input("두 번째 숫자: "))
    print("나눗셈 결과:", n1 / n2)

except ValueError:
    print("❗ 숫자만 입력하세요.")
except ZeroDivisionError:
    print("❗ 0으로 나눌 수 없습니다.")
```

### 💬 ChatGPT에게 물어볼 질문

> **"예외의 종류가 너무 많은데, 전부 외워야 하나요? 자주 쓰는 건 따로 있나요?"**

## 8-4. 예외 메시지 확인 (`as e`)

### `except 예외 as e`란?

> 예외가 발생했을 때, 그 **예외 메시지를 변수(e 등)에 저장**해서 출력할 수 있습니다.

```python
try:
    ...
except 예외타입 as e:
    print(e)
```

### 예제: 나눗셈과 예외 메시지 출력

```python
try:
    num = int(input("숫자를 입력하세요: "))
    print(10 / num)

except Exception as e:
    print("문제가 발생했습니다.")
    print("예외 메시지:", e)
```

예시 출력:

```
숫자를 입력하세요: 0
문제가 발생했습니다.
예외 메시지: division by zero
```

### 예제: 없는 파일 열기

```python
try:
    with open("없는파일.txt", "r") as f:
        content = f.read()

except FileNotFoundError as e:
    print("파일을 열 수 없습니다.")
    print("에러 내용:", e)
```

출력 예:

```
파일을 열 수 없습니다.
에러 내용: [Errno 2] No such file or directory: '없는파일.txt'
```

### 예외 메시지를 로그로 저장하기

```python
try:
    ...
except Exception as e:
    with open("error_log.txt", "a") as log:
        log.write(str(e) + "\n")
```

* 실무에서는 **에러 로그를 파일에 남겨두는 습관**이 중요합니다.

### 실습: 예외 메시지 저장기

```python
try:
    num = int(input("정수 입력: "))
    print(100 / num)

except Exception as e:
    print("예외가 발생했습니다:", e)

    with open("error.txt", "a", encoding="utf-8") as f:
        f.write(f"예외 내용: {e}\n")
```

### 💬 ChatGPT에게 물어볼 질문

> **"에러 메시지를 그대로 사용자에게 보여줘도 괜찮은가요? 보안상 문제는 없나요?"**

## 8-5. finally 절

### `finally`란?

> `try` 블록에서 예외가 발생하든 말든 **무조건 실행되는 블록**

```python
try:
    # 실행할 코드
except 예외:
    # 예외 처리
finally:
    # 항상 실행됨 (성공/실패 관계없이)
```

### 왜 필요한가요?

* 예외가 발생해도 꼭 해야 하는 **마무리 작업**이 있을 수 있음
* 예: **파일 닫기**, **네트워크 종료**, **DB 연결 끊기** 등

### 예제: 파일을 안전하게 닫기

```python
try:
    f = open("data.txt", "r", encoding="utf-8")
    data = f.read()
    print(data)

except FileNotFoundError:
    print("파일이 없습니다.")

finally:
    print("파일을 닫습니다.")
    try:
        f.close()
    except:
        pass  # f가 정의되지 않았을 경우 대비
```

### 예제: 나눗셈 프로그램

```python
try:
    x = int(input("숫자1: "))
    y = int(input("숫자2: "))
    print(f"{x} / {y} = {x/y}")

except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")

finally:
    print("프로그램을 종료합니다.")
```

> `finally` 블록은 항상 실행되므로, **정리 메시지, 종료 처리** 등에 적합합니다.

### `with`와 함께 쓰면 더 깔끔한 방법도 있음

```python
# 자동으로 파일 닫히므로 finally 없이도 안전함
with open("data.txt", "r", encoding="utf-8") as f:
    print(f.read())
```

### 실습: 로그 기록 + 마무리

```python
try:
    num = int(input("숫자를 입력하세요: "))
    print(10 / num)

except Exception as e:
    print("에러:", e)

finally:
    print("작업 종료 로그 기록")
    with open("log.txt", "a") as f:
        f.write("작업이 끝났습니다.\n")
```

### 💬 ChatGPT에게 물어볼 질문

> **"`finally` 블록은 return이나 exit보다 먼저 실행되나요?"**

## 8-6. 사용자 정의 예외와 raise 문

### `raise` 문이란?

> **특정 조건에서 강제로 예외를 발생시키는 명령**

```python
raise 예외이름("메시지")
```

* 상황이 문제가 되거나 부적절할 때 직접 **예외를 던질 수 있음**
* 내장 예외 (`ValueError`, `TypeError`, ...) 또는 **직접 만든 예외 클래스** 사용 가능

### 예제 1: 나이 제한 검사

```python
age = int(input("나이를 입력하세요: "))

if age < 0:
    raise ValueError("❗ 나이는 음수가 될 수 없습니다.")
else:
    print("나이:", age)
```

### 사용자 정의 예외 만들기

> `Exception` 클래스를 상속받아 내가 원하는 이름으로 예외를 만들 수 있습니다.

```python
class SoldOutError(Exception):
    pass
```

```python
chicken = 0
waiting = 1

if chicken == 0:
    raise SoldOutError("❗ 재고가 모두 소진되었습니다.")
```

### 예외 처리와 연결

```python
try:
    raise SoldOutError("❗ 치킨이 다 떨어졌어요.")
except SoldOutError as e:
    print(e)
```

### 예제 2: 주문 시스템 예외 처리

```python
class SoldOutError(Exception):
    pass

chicken = 3
waiting = 1

while True:
    try:
        print(f"[남은 치킨: {chicken}]")
        order = int(input("치킨 몇 마리 주문하시겠습니까? "))

        if order > chicken:
            print("❗ 재고가 부족합니다.")
        elif order <= 0:
            raise ValueError("❗ 1마리 이상 주문해주세요.")
        else:
            print(f"[대기번호 {waiting}] {order}마리 주문 완료")
            chicken -= order
            waiting += 1

        if chicken == 0:
            raise SoldOutError

    except ValueError as e:
        print(e)

    except SoldOutError:
        print("❗ 재고가 모두 소진되어 더 이상 주문할 수 없습니다.")
        break
```

### 사용자 정의 예외를 쓰는 이유?

* **기존 예외와 구분 가능**
* 특정 상황을 **정확하게 명시하고 처리**할 수 있음
* 협업/팀 개발 시 예외 종류별 대응이 쉬움

### 💬 ChatGPT에게 물어볼 질문

> **"직접 예외를 만들지 않고 그냥 raise ValueError만 써도 되지 않나요?"**

## 8-7. 실습: 나눗셈 계산기

### 목표

* 사용자로부터 숫자 2개를 입력받고, **나눗셈 결과 출력**
* 숫자가 아닌 값 → `ValueError`
* 0으로 나누기 → `ZeroDivisionError`
* 모든 예외 → 에러 메시지 저장 및 종료 안내

### 예제 코드

```python
try:
    print("📘 나눗셈 계산기")
    num1 = int(input("첫 번째 숫자 입력: "))
    num2 = int(input("두 번째 숫자 입력: "))
    result = num1 / num2

except ValueError:
    print("❗ 숫자만 입력해주세요.")

except ZeroDivisionError:
    print("❗ 0으로 나눌 수 없습니다.")

except Exception as e:
    print("❗ 예기치 못한 오류가 발생했습니다.")
    print("에러 내용:", e)

else:
    print(f"✅ 결과: {result}")

finally:
    print("🔚 프로그램 종료")
```

### 실행 예시

**예시 1:**
```
📘 나눗셈 계산기  
첫 번째 숫자 입력: 10  
두 번째 숫자 입력: 0  
❗ 0으로 나눌 수 없습니다.  
🔚 프로그램 종료
```

**예시 2:**
```
📘 나눗셈 계산기  
첫 번째 숫자 입력: 열  
❗ 숫자만 입력해주세요.  
🔚 프로그램 종료
```

**예시 3:**
```
📘 나눗셈 계산기  
첫 번째 숫자 입력: 10  
두 번째 숫자 입력: 2  
✅ 결과: 5.0  
🔚 프로그램 종료
```

### 💬 ChatGPT에게 물어볼 질문

> **"try-except-else-finally 구조는 모두 같이 써야 하나요? 필요한 것만 써도 되나요?"**

## 8-8. 실습: 치킨 주문 시스템

### 목표

* 치킨 재고를 관리하며 주문받기
* 사용자가 숫자가 아닌 값을 입력하거나, 0 이하를 입력하면 예외 처리
* 재고가 다 떨어지면 **사용자 정의 예외 `SoldOutError`** 발생
* 프로그램은 주문 후 자동 종료되거나 계속 반복됨

### 예외 정의

```python
class SoldOutError(Exception):
    """재고가 없을 때 발생시키는 사용자 정의 예외"""
    pass
```

### 전체 코드

```python
class SoldOutError(Exception):
    pass

chicken = 5
waiting = 1

while True:
    try:
        print(f"\n[남은 치킨: {chicken}]")
        order = int(input("치킨 몇 마리 주문하시겠습니까? "))

        if order <= 0:
            raise ValueError("❗ 1마리 이상 주문해주세요.")
        if order > chicken:
            print("❗ 주문 수량이 재고보다 많습니다.")
        else:
            print(f"[대기번호 {waiting}] {order}마리 주문 완료")
            chicken -= order
            waiting += 1

        if chicken == 0:
            raise SoldOutError("❗ 재고가 모두 소진되었습니다.")

    except ValueError as e:
        print("입력 오류:", e)

    except SoldOutError as e:
        print(e)
        print("더 이상 주문을 받지 않습니다.")
        break
```

### 실행 예시

```
[남은 치킨: 5]
치킨 몇 마리 주문하시겠습니까? abc
입력 오류: invalid literal for int() with base 10: 'abc'

[남은 치킨: 5]
치킨 몇 마리 주문하시겠습니까? 0
입력 오류: ❗ 1마리 이상 주문해주세요.

[남은 치킨: 5]
치킨 몇 마리 주문하시겠습니까? 6
❗ 주문 수량이 재고보다 많습니다.

[남은 치킨: 5]
치킨 몇 마리 주문하시겠습니까? 3
[대기번호 1] 3마리 주문 완료

[남은 치킨: 2]
치킨 몇 마리 주문하시겠습니까? 2
[대기번호 2] 2마리 주문 완료
❗ 재고가 모두 소진되었습니다.
더 이상 주문을 받지 않습니다.
```

### 💬 ChatGPT에게 물어볼 질문

> **"사용자 정의 예외를 쓰는 게 if 문으로 처리하는 것보다 나은 이유는 뭔가요?"**

## 마무리 요약

| 개념        | 핵심 문법                                                    |
| --------- | -------------------------------------------------------- |
| 예외 처리     | `try`, `except`, `else`, `finally`                       |
| 예외 종류     | `ValueError`, `ZeroDivisionError`, `FileNotFoundError` 등 |
| 예외 메시지 출력 | `except Exception as e:`                                 |
| 예외 발생     | `raise 예외("메시지")`                                        |
| 사용자 정의 예외 | `class MyError(Exception): pass`                         |