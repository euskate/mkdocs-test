# 파이썬 클래스와 객체지향 프로그래밍 🎮
## 게임 유닛으로 배우는 객체지향의 모든 것

---

## 📖 목차

1. [클래스 없이 게임 만들기 - 문제점 발견](#1-클래스-없이-게임-만들기---문제점-발견)
2. [클래스와 객체의 기본 개념](#2-클래스와-객체의-기본-개념)
3. [생성자와 인스턴스 변수](#3-생성자와-인스턴스-변수)
4. [메서드 정의와 호출](#4-메서드-정의와-호출)
5. [클래스 상속](#5-클래스-상속)
6. [다중 상속과 메서드 오버라이딩](#6-다중-상속과-메서드-오버라이딩)
7. [super() 함수](#7-super-함수)
8. [실전 게임 프로그램 완성](#8-실전-게임-프로그램-완성)

---

## 1. 클래스 없이 게임 만들기 - 문제점 발견

### 🤔 상황: 보병과 탱크 유닛 만들기

게임에서 유닛을 만든다고 생각해보세요. 먼저 보병과 탱크를 만들어보겠습니다.

```python
# 보병 유닛
name = "보병"
hp = 40
damage = 5

print(f"{name} 유닛을 생성했습니다.")
print(f"체력 {hp}, 공격력 {damage}")

# 탱크 유닛
tank_name = "탱크"
tank_hp = 150
tank_damage = 35

print(f"{tank_name} 유닛을 생성했습니다.")
print(f"체력 {tank_hp}, 공격력 {tank_damage}")
```

### ❌ 문제점들

1. **코드 중복**: 탱크 2대를 만들려면 변수를 또 만들어야 함
2. **관리 어려움**: 유닛이 많아지면 변수 이름이 복잡해짐
3. **실수 가능성**: `tank2_damage`를 `tank_damage`로 실수할 수 있음
4. **기능 확장 어려움**: 새로운 유닛 타입 추가가 복잡함

### 💡 해결책: 클래스 사용!

이런 문제들을 해결하기 위해 클래스(Class)라는 개념이 등장했습니다.

---

## 2. 클래스와 객체의 기본 개념

### 🏗️ 클래스란?

클래스는 **설계도**라고 생각하면 됩니다. 건물을 지을 때 설계도가 있듯이, 유닛을 만들 때도 설계도가 있어야 합니다.

```python
class Unit:
    def __init__(self, name, hp, damage):
        self.name = name      # 인스턴스 변수
        self.hp = hp          # 인스턴스 변수
        self.damage = damage  # 인스턴스 변수
        print(f"{self.name} 유닛을 생성했습니다.")
        print(f"체력 {self.hp}, 공격력 {self.damage}")
```

### 🎯 객체 생성하기

클래스(설계도)를 사용해서 실제 유닛(객체)을 만들어봅시다.

```python
# 객체 생성
soldier1 = Unit("보병", 40, 5)
soldier2 = Unit("보병", 40, 5)
tank = Unit("탱크", 150, 35)
```

### 🔑 핵심 개념

- **클래스(Class)**: 설계도, 틀
- **객체(Object)**: 클래스로 만든 실제 유닛
- **인스턴스(Instance)**: 객체와 같은 의미
- **인스턴스 변수**: 각 객체가 가지는 고유한 데이터

---

## 3. 생성자와 인스턴스 변수

### 🛠️ 생성자(`__init__`)

생성자는 객체가 만들어질 때 자동으로 호출되는 특별한 메서드입니다.

```python
class Unit:
    def __init__(self, name, hp, damage):  # 생성자
        self.name = name      # self.변수명 = 인스턴스 변수
        self.hp = hp
        self.damage = damage
        print(f"{self.name} 유닛을 생성했습니다.")
```

### 🎮 인스턴스 변수의 동적 생성

객체가 만들어진 후에도 새로운 변수를 추가할 수 있습니다.

```python
# 기본 전투기
stealth1 = Unit("전투기", 80, 5)

# 업그레이드된 전투기
stealth2 = Unit("업그레이드한 전투기", 80, 5)
stealth2.cloaking = True  # 새로운 변수 추가!

if stealth2.cloaking:
    print(f"{stealth2.name}는 현재 은폐 상태입니다.")
```

### ⚠️ 주의사항

```python
# 이렇게 하면 에러 발생!
if stealth1.cloaking:  # stealth1에는 cloaking 변수가 없음
    print("은폐 상태")   # AttributeError 발생
```

---

## 4. 메서드 정의와 호출

### ⚔️ 공격 유닛 만들기

유닛이 공격하고 피해를 받을 수 있게 만들어봅시다.

```python
class AttackUnit:
    def __init__(self, name, hp, damage):
        self.name = name
        self.hp = hp
        self.damage = damage
    
    def attack(self, location):  # 공격 메서드
        print(f"{self.name} : {location} 방향 적군을 공격합니다. [공격력 {self.damage}]")
    
    def damaged(self, damage):   # 피해 메서드
        print(f"{self.name} : {damage}만큼 피해를 입었습니다.")
        self.hp -= damage
        print(f"{self.name} : 현재 체력은 {self.hp}입니다.")
        
        if self.hp <= 0:
            print(f"{self.name} : 파괴됐습니다.")
```

### 🔥 화염방사병 만들기

```python
# 화염방사병 생성
flamethrower = AttackUnit("화염방사병", 50, 16)

# 공격 명령
flamethrower.attack("5시")

# 피해 받기
flamethrower.damaged(25)  # 체력 25 남음
flamethrower.damaged(25)  # 체력 0, 파괴됨
```

---

## 5. 클래스 상속

### 👨‍👩‍👧‍👦 상속이란?

상속은 부모 클래스의 특성을 자식 클래스가 물려받는 것입니다. 부모의 특징을 그대로 가지면서 새로운 특징을 추가할 수 있습니다.

```python
class Unit:  # 부모 클래스
    def __init__(self, name, hp):
        self.name = name
        self.hp = hp

class AttackUnit(Unit):  # Unit 클래스를 상속
    def __init__(self, name, hp, damage):
        Unit.__init__(self, name, hp)  # 부모 클래스 생성자 호출
        self.damage = damage
    
    def attack(self, location):
        print(f"{self.name} : {location} 방향 적군을 공격합니다. [공격력 {self.damage}]")
    
    def damaged(self, damage):
        print(f"{self.name} : {damage}만큼 피해를 입었습니다.")
        self.hp -= damage
        print(f"{self.name} : 현재 체력은 {self.hp}입니다.")
        if self.hp <= 0:
            print(f"{self.name} : 파괴됐습니다.")
```

### 🎯 상속의 장점

1. **코드 재사용**: 공통 기능을 한 번만 작성
2. **유지보수 용이**: 부모 클래스만 수정하면 자식들도 자동 적용
3. **확장성**: 새로운 기능을 쉽게 추가 가능

---

## 6. 다중 상속과 메서드 오버라이딩

### ✈️ 비행 기능 추가

```python
class Flyable:  # 비행 기능 클래스
    def __init__(self, flying_speed):
        self.flying_speed = flying_speed
    
    def fly(self, name, location):
        print(f"{name} : {location} 방향으로 날아갑니다. [속도 {self.flying_speed}]")

class FlyableAttackUnit(AttackUnit, Flyable):  # 다중 상속
    def __init__(self, name, hp, damage, flying_speed):
        AttackUnit.__init__(self, name, hp, damage)
        Flyable.__init__(self, flying_speed)
```

### 🔄 메서드 오버라이딩

부모 클래스의 메서드를 자식 클래스에서 다시 정의하는 것입니다.

```python
class Unit:
    def __init__(self, name, hp, speed):
        self.name = name
        self.hp = hp
        self.speed = speed
    
    def move(self, location):
        print(f"[지상 유닛 이동]")
        print(f"{self.name} : {location} 방향으로 이동합니다. [속도 {self.speed}]")

class FlyableAttackUnit(AttackUnit, Flyable):
    def __init__(self, name, hp, damage, flying_speed):
        AttackUnit.__init__(self, name, hp, damage, 0)  # 지상 속도 0
        Flyable.__init__(self, flying_speed)
    
    def move(self, location):  # 부모의 move 메서드를 오버라이딩
        print(f"[공중 유닛 이동]")
        self.fly(self.name, location)
```

### 🚁 실제 사용 예시

```python
# 지상 유닛
hoverbike = AttackUnit("호버 바이크", 80, 20, 10)

# 공중 유닛
spacecruiser = FlyableAttackUnit("우주 순양함", 500, 25, 3)

hoverbike.move("11시")      # 지상 이동
spacecruiser.move("9시")    # 공중 이동 (오버라이딩된 메서드 사용)
```

---

## 7. super() 함수

### 🔗 super()의 편리함

`super()`를 사용하면 부모 클래스를 더 쉽게 호출할 수 있습니다.

```python
class BuildingUnit(Unit):
    def __init__(self, name, hp, location):
        # 기존 방식
        # Unit.__init__(self, name, hp, 0)
        
        # super() 사용 - 더 간단하고 안전
        super().__init__(name, hp, 0)
        self.location = location

# 보급고 생성
supply_depot = BuildingUnit("보급고", 500, "7시")
```

### 💡 super()의 장점

1. **코드 간결성**: 부모 클래스 이름을 직접 쓸 필요 없음
2. **유지보수성**: 부모 클래스가 바뀌어도 코드 수정 불필요
3. **다중 상속 안전성**: 복잡한 상속 구조에서도 안전

---

## 8. 실전 게임 프로그램 완성

### 🎮 완성된 게임 유닛들

```python
# 보병 유닛
class Soldier(AttackUnit):
    def __init__(self):
        AttackUnit.__init__(self, "보병", 40, 5, 1)
    
    def booster(self):  # 강화제 사용
        if self.hp > 10:
            self.hp -= 10
            print(f"{self.name} : 강화제를 사용합니다. (HP 10 감소)")
        else:
            print(f"{self.name} : 체력이 부족해 기술을 사용할 수 없습니다")

# 탱크 유닛
class Tank(AttackUnit):
    siege_developed = False  # 클래스 변수
    
    def __init__(self):
        AttackUnit.__init__(self, "탱크", 150, 35, 1)
        self.siege_mode = False  # 인스턴스 변수
    
    def set_siege_mode(self):  # 시지 모드 토글
        if not Tank.siege_developed:
            return
        
        if self.siege_mode:
            print(f"{self.name} : 시지 모드를 해제합니다.")
            self.damage //= 2
            self.siege_mode = False
        else:
            print(f"{self.name} : 시지 모드로 전환합니다.")
            self.damage *= 2
            self.siege_mode = True

# 전투기 유닛
class Stealth(FlyableAttackUnit):
    def __init__(self):
        FlyableAttackUnit.__init__(self, "전투기", 80, 20, 5)
        self.cloaked = False
    
    def cloaking(self):  # 은폐 모드 토글
        if self.cloaked:
            print(f"{self.name} : 은폐 모드를 해제합니다.")
            self.cloaked = False
        else:
            print(f"{self.name} : 은폐 모드를 설정합니다.")
            self.cloaked = True
```

### 🎯 게임 시뮬레이션

```python
from random import randint

def game_start():
    print("[알림] 새로운 게임을 시작합니다.")

def game_over():
    print("Player : Good Game")
    print("[Player] 님이 게임에서 퇴장했습니다.")

# 게임 시작
game_start()

# 유닛 생성
soldiers = [Soldier() for _ in range(3)]  # 보병 3기
tanks = [Tank() for _ in range(2)]        # 탱크 2기
stealth = Stealth()                       # 전투기 1기

# 모든 유닛 리스트
attack_units = soldiers + tanks + [stealth]

# 전군 이동
for unit in attack_units:
    unit.move("1시")

# 기술 개발
Tank.siege_developed = True
print("[알림] 탱크의 시지 모드 개발이 완료됐습니다.")

# 전투 준비
for unit in attack_units:
    if isinstance(unit, Soldier):
        unit.booster()
    elif isinstance(unit, Tank):
        unit.set_siege_mode()
    elif isinstance(unit, Stealth):
        unit.cloaking()

# 전군 공격
for unit in attack_units:
    unit.attack("1시")

# 피해 받기
for unit in attack_units:
    unit.damaged(randint(5, 20))

# 게임 종료
game_over()
```

---

## 🎓 학습 정리

### 핵심 개념 체크리스트

- [ ] **클래스와 객체**: 설계도와 실제 제품의 관계
- [ ] **생성자(`__init__`)**: 객체 생성 시 자동 호출
- [ ] **인스턴스 변수**: 각 객체가 가지는 고유한 데이터
- [ ] **메서드**: 객체가 할 수 있는 동작
- [ ] **상속**: 부모 클래스의 특성을 자식이 물려받음
- [ ] **다중 상속**: 여러 부모 클래스에서 상속
- [ ] **메서드 오버라이딩**: 부모 메서드를 자식에서 재정의
- [ ] **super()**: 부모 클래스에 안전하게 접근
- [ ] **isinstance()**: 객체의 타입 확인

### 🚀 다음 단계 학습 추천

1. **추상 클래스 (Abstract Class)**
2. **프로퍼티 (Property)**
3. **매직 메서드 (Magic Methods)**
4. **데코레이터 (Decorators)**
5. **디자인 패턴 (Design Patterns)**

---

## 💻 실습 과제

### 초급 과제
1. 치료 유닛 클래스 만들기 (다른 유닛의 체력 회복)
2. 건물 유닛에 방어력 개념 추가하기

### 중급 과제
1. 유닛 업그레이드 시스템 구현
2. 유닛 간 전투 시뮬레이션 만들기

### 고급 과제
1. 게임 전체 관리 시스템 클래스 설계
2. 유닛 AI 행동 패턴 구현

---

🎮 **축하합니다!** 이제 여러분은 파이썬 클래스와 객체지향 프로그래밍의 기초를 모두 마스터했습니다. 게임 개발부터 웹 개발까지, 이 지식을 바탕으로 더 복잡하고 재미있는 프로그램을 만들어보세요!