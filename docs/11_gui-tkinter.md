# Chapter 11: GUI 프로그래밍 (Tkinter)

## 학습 목표

* GUI의 개념과 Tkinter의 구조를 이해한다.
* 버튼, 라벨, 텍스트박스 등 주요 위젯 사용법을 익힌다.
* 배치 방식(`pack`, `grid`, `place`)을 이해하고 적용한다.
* 이벤트 처리와 입력값 받아서 반응하는 방법을 익힌다.
* 실습 예제를 통해 직접 GUI 프로그램을 만든다.

## 전체 구성

| 절차    | 단원 제목                                           | 주요 내용                            |
| ----- | ----------------------------------------------- | -------------------------------- |
| 11-1  | GUI란? Tkinter란?                                 | GUI 개념, CLI와 비교, Tkinter 소개 및 장점 |
| 11-2  | Tkinter 설치와 기본 창 만들기                            | 기본 창, `Tk()`, `mainloop()` 구조 이해 |
| 11-3  | 기본 위젯: Label, Button, Entry                     | 기본 요소 위젯 사용법 실습                  |
| 11-4  | 입력값 처리: Entry → Label 반영                        | 사용자 입력을 받아 버튼 클릭 시 처리            |
| 11-5  | 배치 관리: pack, grid, place                        | 위젯의 위치 정렬 방식 설명 및 비교             |
| 11-6  | 다양한 위젯: Text, Checkbutton, Radiobutton, Listbox | 추가 위젯 활용                         |
| 11-7  | 이벤트 핸들링과 함수 연결                                  | 버튼 클릭, 입력 변화에 함수 연결하기            |
| 11-8  | 실습: 간단한 계산기 만들기                                 | Entry + Button으로 계산 결과 표시        |
| 11-9  | 실습: 간단한 회원가입 창 만들기                              | 이름/이메일/비밀번호 → 결과 확인              |
| 11-10 | 창 크기, 색상, 아이콘, 타이틀 변경                           | GUI 꾸미기 및 속성 설정                  |

## 주요 위젯 소개

| 위젯            | 설명           |
| ------------- | ------------ |
| `Label`       | 텍스트 출력       |
| `Button`      | 클릭 가능한 버튼    |
| `Entry`       | 한 줄 입력창      |
| `Text`        | 여러 줄 텍스트 입력창 |
| `Checkbutton` | 체크박스         |
| `Radiobutton` | 라디오 버튼       |
| `Listbox`     | 리스트 항목 표시    |
| `Frame`       | 여러 위젯 묶기용 박스 |

---

## 11-1. GUI란? Tkinter란?

### GUI란?

**Graphical User Interface (그래픽 사용자 인터페이스)**

사용자가 **마우스 클릭, 버튼, 창 등 시각적 요소**를 통해 프로그램과 소통하는 방식입니다.

### GUI vs CLI 비교

| 구분      | CLI (Command Line Interface) | GUI (Graphical User Interface) |
| ------- | ---------------------------- | ------------------------------ |
| 방식      | 텍스트 명령어 입력                   | 버튼/창 등 시각적 요소 조작               |
| 예       | `python hello.py`            | 마우스로 버튼 클릭                     |
| 사용자 친화성 | 낮음 (초보자 불편)                  | 높음 (직관적 사용 가능)                 |
| 예시      | 터미널, 콘솔                      | 윈도우 탐색기, 카카오톡                  |

### Tkinter 소개

**Tkinter**는 파이썬에서 기본으로 제공하는 GUI 라이브러리입니다.

* 설치 필요 없음 → **파이썬에 기본 포함**
* 쉽고 빠르게 GUI 앱 개발 가능
* 학습용/작은 툴 제작에 적합

### Tkinter의 장점

| 항목       | 설명                          |
| -------- | --------------------------- |
| 내장 라이브러리 | 설치 없이 import만으로 사용 가능       |
| 학습 곡선    | 초보자도 입문하기 쉬움                |
| 크로스 플랫폼  | Windows, macOS, Linux 모두 지원 |
| 커뮤니티     | 튜토리얼, 예시, 문서 풍부             |

### Tkinter 프로그램 기본 구조

```python
import tkinter as tk

root = tk.Tk()         # 윈도우 생성
root.title("나의 첫 GUI")  # 창 제목 설정
root.mainloop()        # GUI 실행 (무한 루프)
```

* `Tk()` : 기본 창(Window) 생성
* `mainloop()` : 사용자가 닫기 전까지 계속 실행

### 💬 ChatGPT에게 물어볼 질문

> **"Tkinter 말고 다른 GUI 라이브러리는 어떤 게 있나요?"**

👉 `PyQt`, `wxPython`, `Kivy` 등도 존재하지만, 학습용으로는 Tkinter가 가장 가볍고 쉽습니다.

---

## 11-2. Tkinter 기본 창 만들기

### 기본 코드 구조

```python
import tkinter as tk

root = tk.Tk()  # 윈도우 생성
root.title("나의 첫 GUI 프로그램")  # 창 제목
root.geometry("400x300")  # 창 크기 (너비 x 높이)

root.mainloop()  # GUI 실행 (무한 루프)
```

### 주요 메서드

| 메서드                   | 설명                     |
| --------------------- | ---------------------- |
| `Tk()`                | 새 창 생성                 |
| `title("제목")`         | 창 제목 설정                |
| `geometry("400x300")` | 창 크기 설정 (가로x세로)        |
| `mainloop()`          | GUI 유지, 사용자가 닫을 때까지 대기 |

### 창 크기 조절 설정

```python
root.resizable(False, False)  # 가로, 세로 창 크기 조절 금지
```

* `True/False` 값으로 가로/세로 조절 가능 여부 설정

### 💬 ChatGPT에게 물어볼 질문

> **"Tkinter 창이 실행되었는데 바로 닫히는 이유는 뭘까요?"**

👉 `mainloop()`를 호출하지 않으면 창이 바로 닫힙니다. 반드시 마지막 줄에 있어야 합니다.

---

## 11-3. 기본 위젯 – Label, Button, Entry

### 1. `Label` – 텍스트 출력

```python
import tkinter as tk

root = tk.Tk()
root.title("Label 예제")
root.geometry("300x100")

label = tk.Label(root, text="안녕하세요, Tkinter!")  # 텍스트
label.pack()

root.mainloop()
```

* `text`: 보여줄 문자열
* `pack()`: 위젯을 배치하는 가장 기본적인 방식 (아래로 쌓임)

### 2. `Button` – 버튼 만들기

```python
def on_click():
    print("버튼이 클릭되었습니다!")

btn = tk.Button(root, text="클릭", command=on_click)
btn.pack()
```

* `text`: 버튼에 표시할 내용
* `command`: 클릭 시 실행할 함수 (괄호 없이 함수명만)

### 3. `Entry` – 한 줄 입력창

```python
entry = tk.Entry(root, width=20)
entry.pack()
```

* 사용자의 입력을 받을 수 있는 위젯
* `entry.get()` 으로 입력값 읽기 가능

### 예제: 버튼 클릭 → Entry 내용 → Label로 출력

```python
import tkinter as tk

def say_hello():
    name = entry.get()
    label.config(text=f"안녕하세요, {name}님!")

root = tk.Tk()
root.title("입력 예제")
root.geometry("300x150")

entry = tk.Entry(root)
entry.pack()

btn = tk.Button(root, text="확인", command=say_hello)
btn.pack()

label = tk.Label(root, text="")
label.pack()

root.mainloop()
```

### 주요 메서드 정리

| 위젯     | 메서드                   | 설명            |
| ------ | --------------------- | ------------- |
| Entry  | `.get()`              | 입력값 가져오기      |
| Label  | `.config(text="...")` | 라벨 텍스트 변경     |
| Button | `command=함수`          | 버튼 클릭 시 함수 실행 |

---

## 11-4. 입력값 처리 – Entry → Label 반영 및 활용

### 기본 예제: 이름 입력 → 라벨 출력

```python
def show_name():
    name = entry.get()
    if name.strip() == "":
        label.config(text="⚠️ 이름을 입력하세요.")
    else:
        label.config(text=f"👋 안녕하세요, {name}님!")

entry = tk.Entry(root)
entry.pack()

btn = tk.Button(root, text="입력 확인", command=show_name)
btn.pack()

label = tk.Label(root, text="")
label.pack()
```

### 입력값 초기화 하기

```python
entry.delete(0, tk.END)  # 입력값 지우기 (0번 인덱스부터 끝까지)
```

예: 버튼 누르면 입력창 초기화

```python
def reset():
    entry.delete(0, tk.END)
    label.config(text="")

reset_btn = tk.Button(root, text="초기화", command=reset)
reset_btn.pack()
```

### Entry 입력창에 포커스 주기

```python
entry.focus()  # 실행 시 자동 커서 이동
```

### 숫자 입력 체크 예제

```python
def check_age():
    value = entry.get()
    if value.isdigit():
        label.config(text=f"당신의 나이는 {value}세입니다.")
    else:
        label.config(text="⚠️ 숫자를 입력해주세요.")
```

> `.isdigit()`은 문자열이 숫자로만 구성되어 있는지 확인

### 💬 ChatGPT에게 물어볼 질문

> **"Entry 위젯에 숫자만 입력되게 제한할 수는 없나요?"**

👉 가능합니다. `validate` 옵션 또는 `ttk.Spinbox` 등으로 제한 가능합니다.

---

## 11-5. 위젯 배치 – `pack`, `grid`, `place`

### GUI 배치란?

여러 개의 위젯을 창 안에 **어떻게 배치할지 정하는 방식**입니다.

Tkinter에서는 대표적으로 **3가지 방식**이 있습니다:

| 배치 방식     | 설명                    | 사용 예          |
| --------- | --------------------- | ------------- |
| `pack()`  | 위젯을 **위에서 아래로 자동 정렬** | 간단한 레이아웃      |
| `grid()`  | **표 형태의 행/열 위치 지정**   | 폼(Form), 로그인창 |
| `place()` | **픽셀 위치 지정 (절대 좌표)**  | 자유로운 위치 조절    |

### 1. `pack()` – 기본 배치 방식

```python
tk.Label(root, text="이름").pack()
tk.Entry(root).pack()
tk.Button(root, text="확인").pack()
```

* 위젯들이 **위에서 아래로 쌓임**
* `side="left"`, `side="right"` 등으로 방향 지정 가능

```python
tk.Button(root, text="왼쪽").pack(side="left")
tk.Button(root, text="오른쪽").pack(side="right")
```

### 2. `grid()` – 표 형태 배치

```python
tk.Label(root, text="이름").grid(row=0, column=0)
tk.Entry(root).grid(row=0, column=1)

tk.Label(root, text="나이").grid(row=1, column=0)
tk.Entry(root).grid(row=1, column=1)
```

* `row`, `column` 지정
* 한 줄에 여러 개 배치 가능
* 폼 입력 화면에 적합

> ❗주의: **pack과 grid는 같은 창(root) 내에서 함께 쓰면 안 됨**

### 3. `place()` – 절대 위치 배치

```python
tk.Button(root, text="확인").place(x=100, y=50)
```

* `x`, `y` 좌표 직접 지정
* 복잡한 위치 지정 가능
* 하지만 해상도나 창 크기 변화에 약함

### 실전 예제: grid로 회원가입 폼 만들기

```python
import tkinter as tk

root = tk.Tk()
root.title("회원가입 폼")

tk.Label(root, text="이름").grid(row=0, column=0, sticky="e")
entry_name = tk.Entry(root)
entry_name.grid(row=0, column=1)

tk.Label(root, text="이메일").grid(row=1, column=0, sticky="e")
entry_email = tk.Entry(root)
entry_email.grid(row=1, column=1)

tk.Button(root, text="제출").grid(row=2, column=0, columnspan=2)

root.mainloop()
```

### 레이아웃 디자인 팁

* 같은 방식(`pack` or `grid`)만 사용
* `grid()`는 **columnspan**, **padx/pady**, **sticky**로 세부 조정 가능
* `place()`는 추천하지 않음 (단순 앱 외에는 어려움 많음)

### 💬 ChatGPT에게 물어볼 질문

> **"위젯 간의 여백 조정은 어떻게 하나요?"**

👉 `padx`, `pady`, `ipadx`, `ipady` 옵션을 활용할 수 있습니다.

---

## 11-6. 다양한 위젯 – Checkbutton, Radiobutton, Listbox

### 1. Checkbutton (체크박스)

여러 개 항목 중 **복수 선택** 가능 (예: 관심사, 약관 동의 등)

```python
import tkinter as tk

root = tk.Tk()
root.title("체크박스 예제")

music = tk.IntVar()
movie = tk.IntVar()

tk.Checkbutton(root, text="음악", variable=music).pack()
tk.Checkbutton(root, text="영화", variable=movie).pack()

def show_checked():
    result = []
    if music.get() == 1:
        result.append("음악")
    if movie.get() == 1:
        result.append("영화")
    label.config(text="선택한 취미: " + ", ".join(result))

tk.Button(root, text="확인", command=show_checked).pack()
label = tk.Label(root, text="")
label.pack()

root.mainloop()
```

* `variable=IntVar()` → 체크 여부를 정수(0 또는 1)로 저장
* `get()`으로 체크 상태 확인

### 2. Radiobutton (라디오 버튼)

여러 개 중 **하나만 선택** 가능 (예: 성별, 연령대)

```python
gender = tk.StringVar(value="남성")  # 기본값 설정

tk.Radiobutton(root, text="남성", variable=gender, value="남성").pack()
tk.Radiobutton(root, text="여성", variable=gender, value="여성").pack()

def show_gender():
    label.config(text="선택된 성별: " + gender.get())

tk.Button(root, text="확인", command=show_gender).pack()
```

* `StringVar()`에 선택값이 자동으로 저장됨
* `value=...`에 지정된 값이 저장됨

### 3. Listbox (리스트 박스)

여러 항목을 **리스트 형태**로 보여주고, **선택 가능**

```python
listbox = tk.Listbox(root, height=4, selectmode="single")
listbox.insert(0, "Python")
listbox.insert(1, "Java")
listbox.insert(2, "C++")
listbox.insert(3, "JavaScript")
listbox.pack()

def show_language():
    selected = listbox.curselection()
    if selected:
        label.config(text="선택한 언어: " + listbox.get(selected[0]))

tk.Button(root, text="확인", command=show_language).pack()
```

* `.insert(index, "항목")`: 항목 추가
* `.curselection()`: 현재 선택된 항목의 인덱스를 반환
* `selectmode`는 `"single"` 또는 `"multiple"`

### 위젯 선택 비교 요약

| 위젯            | 용도     | 선택 수                    |
| ------------- | ------ | ----------------------- |
| `Checkbutton` | 체크박스   | 여러 개 선택 가능              |
| `Radiobutton` | 라디오 버튼 | 하나만 선택                  |
| `Listbox`     | 목록 리스트 | 1개 또는 다중 선택 가능 (설정에 따라) |

### 💬 ChatGPT에게 물어볼 질문

> **"Listbox에서 다중 선택은 어떻게 하나요?"**

👉 `selectmode="multiple"` 또는 `"extended"`로 설정하면 가능합니다.

---

## 11-7. 이벤트 핸들링과 사용자 함수 연결

### 이벤트(Event)란?

사용자의 **행동(클릭, 입력, 선택, 이동 등)**에 반응해 프로그램이 **미리 지정된 함수(콜백)를 실행**하는 구조

### 대표적인 이벤트 예시

| 이벤트       | 설명                                     |
| --------- | -------------------------------------- |
| 버튼 클릭     | `command=함수명` 사용                       |
| 입력창 값 변경  | `.bind("<KeyRelease>", 함수)`            |
| 마우스 클릭    | `.bind("<Button-1>", 함수)`              |
| 엔터 키 입력   | `.bind("<Return>", 함수)`                |
| 마우스 진입/이탈 | `.bind("<Enter>")`, `.bind("<Leave>")` |

### 1. 버튼 클릭 → command 방식 (가장 기본)

```python
def greet():
    print("안녕하세요!")

btn = tk.Button(root, text="인사하기", command=greet)
btn.pack()
```

* `command=함수명`은 **이벤트 객체(event)를 받지 않음**
* 파라미터 전달이 필요하다면 `lambda`로 래핑

### 2. bind()로 키보드/마우스 이벤트 연결

```python
def on_key(event):
    label.config(text="입력된 키: " + event.char)

entry = tk.Entry(root)
entry.pack()
entry.bind("<KeyRelease>", on_key)  # 키 입력 시 반응
```

* `event` 객체는 `.char`, `.keysym`, `.x`, `.y` 등 다양한 정보 포함

### 3. 마우스 클릭 이벤트 예시

```python
def on_click(event):
    label.config(text=f"클릭 위치: x={event.x}, y={event.y}")

root.bind("<Button-1>", on_click)  # 마우스 왼쪽 클릭
```

* `Button-1`: 왼쪽 클릭
* `Button-2`: 휠 클릭
* `Button-3`: 오른쪽 클릭

### 4. Entry에서 Enter 키 입력 처리

```python
def on_enter(event):
    name = entry.get()
    label.config(text=f"환영합니다, {name}님!")

entry.bind("<Return>", on_enter)  # Enter 키 감지
```

### 이벤트 이름 정리

| 이벤트                 | 설명        |
| ------------------- | --------- |
| `<Button-1>`        | 마우스 왼쪽 클릭 |
| `<Double-Button-1>` | 더블 클릭     |
| `<Enter>`           | 마우스 진입    |
| `<Leave>`           | 마우스 벗어남   |
| `<Key>`             | 키 누름      |
| `<KeyRelease>`      | 키 뗌       |
| `<Return>`          | Enter 키   |

### 💬 ChatGPT에게 물어볼 질문

> **"command와 bind는 어떤 차이가 있나요?"**

👉 `command`는 간단한 클릭 이벤트용, `bind`는 키보드/마우스 등 다양한 이벤트를 세밀하게 처리할 때 사용합니다.

---

## 11-8. 실습 – 간단한 계산기 만들기

### 전체 코드 예제

```python
import tkinter as tk

def calculate():
    try:
        num1 = int(entry1.get())
        num2 = int(entry2.get())
        result = num1 + num2
        label_result.config(text=f"결과: {result}")
    except ValueError:
        label_result.config(text="⚠️ 숫자만 입력하세요.")

root = tk.Tk()
root.title("간단한 계산기")
root.geometry("300x200")

tk.Label(root, text="첫 번째 숫자").pack()
entry1 = tk.Entry(root)
entry1.pack()

tk.Label(root, text="두 번째 숫자").pack()
entry2 = tk.Entry(root)
entry2.pack()

btn = tk.Button(root, text="더하기", command=calculate)
btn.pack(pady=10)

label_result = tk.Label(root, text="결과: ")
label_result.pack()

root.mainloop()
```

### 포인트 정리

| 포인트                 | 설명                 |
| ------------------- | ------------------ |
| `int(entry.get())`  | 입력값을 정수로 변환        |
| `ValueError` 처리     | 숫자 외 입력시 오류 메시지 출력 |
| `.config(text=...)` | Label 텍스트 동적 변경    |
| `pady`              | 버튼과 다음 위젯 사이 여백 설정 |

### 💬 ChatGPT에게 물어볼 질문

> **"입력창이 비어 있을 때도 오류가 나는 이유는 뭔가요?"**

👉 빈 문자열은 숫자로 변환할 수 없기 때문에 `ValueError`가 발생합니다. 예외 처리로 이를 막아야 합니다.

---

## 11-9. 실습 – 회원가입 GUI 만들기

### 전체 코드 예제

```python
import tkinter as tk
from tkinter import messagebox

def submit():
    name = entry_name.get().strip()
    email = entry_email.get().strip()
    pw = entry_pw.get().strip()

    if not name or not email or not pw:
        messagebox.showwarning("입력 오류", "모든 항목을 입력해주세요.")
        return

    info = f"이름: {name}\n이메일: {email}"
    messagebox.showinfo("가입 완료", info)

root = tk.Tk()
root.title("회원가입 폼")
root.geometry("300x200")

tk.Label(root, text="이름").grid(row=0, column=0, sticky="e", padx=10, pady=5)
entry_name = tk.Entry(root)
entry_name.grid(row=0, column=1)

tk.Label(root, text="이메일").grid(row=1, column=0, sticky="e", padx=10, pady=5)
entry_email = tk.Entry(root)
entry_email.grid(row=1, column=1)

tk.Label(root, text="비밀번호").grid(row=2, column=0, sticky="e", padx=10, pady=5)
entry_pw = tk.Entry(root, show="*")
entry_pw.grid(row=2, column=1)

btn = tk.Button(root, text="가입하기", command=submit)
btn.grid(row=3, column=0, columnspan=2, pady=10)

root.mainloop()
```

### 주요 기능 설명

| 요소                      | 설명               |
| ----------------------- | ---------------- |
| `Entry(..., show="*")`  | 비밀번호 입력 시 텍스트 숨김 |
| `messagebox.showinfo()` | 팝업창으로 결과 표시      |
| `strip()`               | 공백 제거하여 빈 입력 방지  |
| `columnspan=2`          | 버튼을 두 칸에 걸쳐 배치   |

---

## 11-10. 창 꾸미기 – 타이틀, 크기, 색상, 아이콘 설정

### 1. 타이틀 설정

```python
root.title("🌟 나의 첫 GUI 앱")
```

* 창의 상단에 표시되는 이름을 설정합니다.
* 이모지도 사용 가능 (`✔️`, `💡`, `📋` 등)

### 2. 창 크기 및 고정 여부

```python
root.geometry("500x300")         # 창 크기 설정 (너비 x 높이)
root.resizable(True, False)      # 가로는 조정 가능, 세로는 고정
```

* `resizable(width, height)` → `True/False`로 조정 가능 여부 지정

### 3. 배경 색상 설정

```python
root.configure(bg="#f0f8ff")  # 전체 창 배경 색 (하늘색 계열)