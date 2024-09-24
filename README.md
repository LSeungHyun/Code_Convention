# LedaGames Unity C# Script Style Guide

## Table of Contents

  1. [Types](#types)
  1. [References](#references)
  1. [Objects](#objects)
  1. [Arrays](#arrays)
  1. [Functions](#functions)
  1. [Classes & Constructors](#classes--constructors)
  1. [Conditionals & Comparisons](#conditionals--comparisons)
  1. [Whitespace & Indentation](#whitespace--indentation)
  1. [Naming Conventions](#naming-conventions)
  1. [Comments](#comments)
  1. [Conditionals & Blocks](#conditionals--blocks)
  1. [File Structure](#file-structure)
  1. [Object Creation and Management](#object-creation-and-management)
  1. [Variable Declaration and Assignment](#variable-declaration-and-assignment)

---

## 1. Types

  <a name="types--value"></a><a name="1.1"></a>
  - [1.1](#types--value) **기본형(Primitive Types)**: Unity C#의 기본형에는 `int`, `float`, `double`, `bool`, `string`, `char` 등이 있으며, 이러한 타입들은 값이 직접적으로 조작됩니다.

    ```csharp
    int a = 10;
    int b = a;
    b = 20;
    Debug.Log(a); // 출력: 10
    Debug.Log(b); // 출력: 20
    ```

  <a name="types--reference"></a><a name="1.2"></a>
  - [1.2](#types--reference) **참조형(Reference Types)**: 참조형 타입은 `class`, `array`, `object` 등이 있으며, 참조를 통해 값을 변경합니다.

    ```csharp
    int[] array1 = { 1, 2, 3 };
    int[] array2 = array1;
    array2[0] = 9;
    Debug.Log(array1[0]); // 출력: 9
    ```

---

**[⬆ back to top](#table-of-contents)**

## 2. References

  <a name="references--direct-caching"></a><a name="2.1"></a>
  - [2.1](#references--direct-caching) **Inspector 사용 권장**: Inspector 창에 직접 캐싱할 수 있다면 스크립트를 통한 참조는 지양합니다.

  <a name="references--find-getcomponent"></a><a name="2.2"></a>
  - [2.2](#references--find-getcomponent) **Find 및 GetComponent 사용**: `Find` 및 `GetComponent` 메서드 참조는 `Awake`에서 호출하며, `null` 값 확인을 통해 메모리 낭비를 방지합니다.

  <a name="references--const-readonly"></a><a name="2.3"></a>
  - [2.3](#references--const-readonly) **상수 및 readonly 사용**: 재할당을 방지하려면 `const` 또는 `readonly`를 사용하며 `var`는 지양합니다.

    ```csharp
    const int MAX_VALUE = 100;
    readonly string NAME = "Unity";
    ```

  <a name="references--explicit-types"></a><a name="2.4"></a>
  - [2.4](#references--explicit-types) **명시적 타입 사용**: 가능한 경우 명시적인 타입을 사용하고 `var`는 타입이 불명확할 때만 사용합니다.

---

**[⬆ back to top](#table-of-contents)**

## 3. Objects

  <a name="objects--new-keyword"></a><a name="3.1"></a>
  - [3.1](#objects--new-keyword) **객체 생성**: 객체는 `new` 키워드를 사용하여 명시적으로 생성합니다.

    ```csharp
    // Bad
    GameObject player;

    // Good
    GameObject player = new GameObject("Player");
    ```

  <a name="objects--reserved-words"></a><a name="3.2"></a>
  - [3.2](#objects--reserved-words) **예약어 사용 금지**: 예약어를 변수 이름으로 사용하지 않습니다.

    ```csharp
    // Bad
    var class = "Test";

    // Good
    var type = "Test";
    ```

---

**[⬆ back to top](#table-of-contents)**

## 4. Arrays

  <a name="arrays--literal-syntax"></a><a name="4.1"></a>
  - [4.1](#arrays--literal-syntax) **배열 리터럴 사용**: 배열 생성 시 리터럴 구문을 사용하여 가독성을 높입니다.

    ```csharp
    // Bad
    int[] numbers = new int[] { 1, 2, 3 };

    // Good
    int[] numbers = { 1, 2, 3 };
    ```

  <a name="arrays--list-add-method"></a><a name="4.2"></a>
  - [4.2](#arrays--list-add-method) **List 사용**: 배열의 크기를 동적으로 관리할 때는 `List<T>`의 `Add` 메서드를 사용합니다.

    ```csharp
    List<int> numbers = new List<int>();
    numbers.Add(1);
    numbers.Add(2);
    ```

---

**[⬆ back to top](#table-of-contents)**

## 5. Functions

  <a name="functions--declaration"></a><a name="5.1"></a>
  - [5.1](#functions--declaration) **명시적 함수 선언**: 함수는 명시적으로 선언하여 디버깅에 유리하게 작성합니다.

    ```csharp
    // Bad
    Action myFunc = () => Debug.Log("Hello");

    // Good
    void MyFunc() {
        Debug.Log("Hello");
    }
    ```

  <a name="functions--block-scope"></a><a name="5.2"></a>
  - [5.2](#functions--block-scope) **블록 스코프 내 함수 선언 피하기**: 함수는 블록 외부에서 선언하는 것이 일반적입니다.

    ```csharp
    // Bad
    if (condition) {
        void TestFunc() { }
    }

    // Good
    void TestFunc() {
        if (condition) { }
    }
    ```

---

**[⬆ back to top](#table-of-contents)**

## 6. Classes & Constructors

  <a name="classes--declaration"></a><a name="6.1"></a>
  - [6.1](#classes--declaration) **클래스 사용**: 명시적으로 클래스를 사용하여 코드를 구조화합니다.

    ```csharp
    class Player {
        public string Name { get; set; }
        public int Health { get; set; }

        public Player(string name, int health) {
            Name = name;
            Health = health;
        }
    }
    ```

  <a name="classes--inheritance"></a><a name="6.2"></a>
  - [6.2](#classes--inheritance) **상속 구현**: `extends` 대신 `:`를 사용하여 상속을 구현합니다.

    ```csharp
    class Enemy : Player {
        public Enemy(string name, int health) : base(name, health) { }
    }
    ```

---

**[⬆ back to top](#table-of-contents)**

## 7. Conditionals & Comparisons

  <a name="conditionals--equals"></a><a name="7.1"></a>
  - [7.1](#conditionals--equals) **Equals 사용**: 객체 비교 시 `==` 연산자 대신 `Equals` 메서드를 사용합니다.

    ```csharp
    // Bad
    if (a == b) { }

    // Good
    if (a.Equals(b)) { }
    ```

  <a name="conditionals--is"></a><a name="7.2"></a>
  - [7.2](#conditionals--is) **타입 체크 시 is 사용**: `var`로 받은 변수의 타입을 검사할 때 `is` 구문을 사용합니다.

    ```csharp
    if (fromPoint is string)
      Debug.Log("String 타입");
    ```

---

**[⬆ back to top](#table-of-contents)**

## 8. Whitespace & Indentation

  <a name="whitespace--indentation"></a><a name="8.1"></a>
  - [8.1](#whitespace--indentation) **두 칸 들여쓰기 사용**: 들여쓰기는 두 칸을 사용하여 가독성을 유지합니다.

    ```csharp
    void MyFunction() {
      if (true) {
        // 두 칸 들여쓰기
      }
    }
    ```

---

**[⬆ back to top](#table-of-contents)**

## 9. Naming Conventions

  <a name="naming--camelcase-pascalcase"></a><a name="9.1"></a>
  - [9.1](#naming--camelcase-pascalcase) **camelCase 및 PascalCase 사용**: 변수는 `camelCase`를, 함수나 클래스 이름은 `PascalCase`를 사용합니다.

    ```csharp
    int playerHealth;   // camelCase
    class PlayerCharacter {}   // PascalCase
    ```

---

**[⬆ back to top](#table-of-contents)**

## 10. Comments

  <a name="comments--single-line"></a><a name="10.1"></a>
  - [10.1](#comments--single-line) **단일행 주석**: 단일 행 주석은 `//`로 작성하며, 설명이 필요한 경우 주석을 코드 상단에 배치합니다.

    ```csharp
    // 플레이어의 체력을 증가시킵니다.
    playerHealth += 10;
    ```

  <a name="comments--multi-line"></a><a name="10.2"></a>
  - [10.2](#comments--multi-line) **다중 행 주석 (/** */)**: 여러 줄의 설명이 필요한 경우에는 다중 행 주석을 사용합니다.

    ```csharp
    /*
     * 플레이어의 체력을 회복시키는 함수입니다.
     * @param amount 회복할 체력 양
     */
    void HealPlayer(int amount) {
      playerHealth += amount;
    }
    ```

---

**[⬆ back to top](#table-of-contents)**

## 11. Conditionals & Blocks

  <a name="conditionals--braces"></a><a name="11.1"></a>
  - [11.1](#conditionals--braces) **중괄호 사용**: 모든 조건문 및 반복문의 블록에는 중괄호 `{}`를 사용하여 명확한 코드 흐름을 유지합니다.

    ```csharp
    if (playerHealth > 0) {
      Debug.Log("체력감소");
    }
    ```

  <a name="conditionals--single-line-braces"></a><a name="11.2"></a>
  - [11.2](#conditionals--single-line-braces) **한 줄의 조건문도 중괄호 사용**: 조건문의 본문이 한 줄일 때에도 중괄호를 사용하여 일관성을 유지 및 가독성 향상

    ```csharp
    // Bad
    if (isAlive) doSomething();

    // Good
    if (isAlive) {
      doSomething();
    }
    ```

---

**[⬆ back to top](#table-of-contents)**

## 12. File Structure

  <a name="file-structure--one-class-per-file"></a><a name="12.1"></a>
  - [12.1](#file-structure--one-class-per-file) **파일당 하나의 클래스**: 각 파일은 하나의 클래스만 포함하며, 파일 이름은 클래스 이름과 동일하게 설정합니다.

    ```csharp
    // Player.cs
    public class Player {
      // 클래스 구현
    }
    ```

  <a name="file-structure--namespace"></a><a name="12.2"></a>
  - [12.2](#file-structure--namespace) **네임스페이스 사용**: 클래스의 논리적 그룹화를 위해 네임스페이스를 사용합니다.

    ```csharp
    namespace GameNamespace {
      public class Player {
        // 클래스 구현
      }
    }
    ```

---

**[⬆ back to top](#table-of-contents)**

## 13. Object Creation and Management

  <a name="objects--reset-position"></a><a name="13.1"></a>
  - [13.1](#objects--reset-position) **빈 오브젝트 생성 후 위치 Reset**: 모든 빈 오브젝트는 생성 후 위치를 Reset합니다.

  <a name="objects--naming"></a><a name="13.2"></a>
  - [13.2](#objects--naming) **오브젝트 이름 영어 사용**: 모든 빈 오브젝트의 이름은 영어를 지향하고 한글을 지양합니다.

  <a name="objects--naming-case"></a><a name="13.3"></a>
  - [13.3](#objects--naming-case) **PascalCase 사용**: 모든 빈 오브젝트의 이름은 PascalCase를 사용하고 사용 의미에 알맞은 이름을 부여합니다.

    ```csharp
    // Bad
    move

    // Good
    MovePoint
    ```

---

**[⬆ back to top](#table-of-contents)**

## 14. Variable Declaration and Assignment

  <a name="variables--declaration-order"></a><a name="14.1"></a>
  - [14.1](#variables--declaration-order) **변수 선언 순서**: 클래스 내부의 맨 위부터 선언합니다.

  <a name="variables--inspector"></a><a name="14.2"></a>
  - [14.2](#variables--inspector) **Inspector에서 캐싱 여부에 따라 분류**: Inspector에서 직접 캐싱해주는 변수와 그렇지 않은 변수로 분류합니다.

  <a name="variables--type-order"></a><a name="14.3"></a>
  - [14.3](#variables--type-order) **타입별 선언 순서**: GameObject, string, int, bool 타입 순서로 선언합니다.

**[⬆ back to top](#table-of-contents)**
