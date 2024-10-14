# LedaGames Unity C# Script Style Guide

## Table of Contents

  1. [타입 (Types)](#1-types)
  1. [참조 (References)](#2-references)
  1. [오브젝트 (Objects)](#3-objects)
  1. [컬렉션 (Collection)](#4-collection)
  1. [함수 (Functions)](#5-functions)
  1. [클래스 및 생성자 (Classes & Constructors)](#6-classes--constructors)
  1. [조건식 및 비교 (Conditionals & Comparisons)](#7-conditionals--comparisons)
  1. [공백 및 들여쓰기 (Whitespace & Indentation)](#8-whitespace--indentation)
  1. [명명 규칙 (Naming Conventions)](#9-naming-conventions)
  1. [주석 (Comments)](#10-comments)
  1. [조건문 및 블록 (Conditionals & Blocks)](#11-conditionals--blocks)
  1. [파일 구조 (File Structure)](#12-file-structure)
  1. [오브젝트 생성 및 관리 (Object Creation and Management)](#13-object-creation-and-management)
  1. [변수 선언 및 할당 (Variable Declaration and Assignment)](#14-variable-declaration-and-assignment)
  1. [아트 리소스 기본 설정 (Basic Art Resource Setting)](#15-basic-art-resource-setting)
  1. [WebGL 빌드 기본 설정 (WebGL Build Basic Setting)](#16-webgl-build-basic-setting)


---

## 1. 타입 (Types)

  <a name="1-types"></a>
  - **기본형(Primitive Types)**: Unity C#의 기본형에는 `int`, `float`, `double`, `bool`, `string`, `char` 등이 있으며, 이러한 타입들은 값이 직접적으로 조작됩니다.

    ```csharp
    int a = 10;
    int b = a;
    b = 20;
    Debug.Log(a); // 출력: 10
    Debug.Log(b); // 출력: 20
    ```

  - **참조형(Reference Types)**: 참조형 타입은 `class`, `array`, `object` 등이 있으며, 참조를 통해 값을 변경합니다.

    ```csharp
    int[] array1 = { 1, 2, 3 };
    int[] array2 = array1;
    array2[0] = 9;
    Debug.Log(array1[0]); // 출력: 9
    ```

---
**[⬆ back to top](#table-of-contents)**

## 2. 참조 (References)

  <a name="2-references"></a>
  - **Inspector 사용 권장**: Inspector 창에 직접 캐싱할 수 있다면 스크립트를 통한 참조는 지양합니다.

  - **Find 및 GetComponent 사용**: `Find` 및 `GetComponent` 메서드 참조는 `Awake`에서 호출하며, `null` 값 확인을 통해 메모리 낭비를 방지합니다.

  - **상수 및 readonly 사용**: 재할당을 방지하려면 `const` 또는 `readonly`를 사용하며 `var`는 지양합니다.

    ```csharp
    const int MAX_VALUE = 100;
    readonly string NAME = "Unity";
    ```

  - **명시적 타입 사용**: 가능한 경우 명시적인 타입을 사용하고 `var`는 타입이 불명확할 때만 사용합니다.

---
**[⬆ back to top](#table-of-contents)**

## 3. 오브젝트 (Objects)

  <a name="3-objects"></a>
  - **객체 생성**: 객체는 `new` 키워드를 사용하여 명시적으로 생성합니다.

    ```csharp
    // Bad
    GameObject player;

    // Good
    GameObject player = new GameObject("Player");
    ```

  - **예약어 사용 금지**: 예약어를 변수 이름으로 사용하지 않습니다.

    ```csharp
    // Bad
    var class = "Test";

    // Good
    var type = "Test";
    ```

---
**[⬆ back to top](#table-of-contents)**

## 4. 컬렉션 (Collection) [어레이리스트, 리스트, 큐, 스택, 해시테이블, 해시셋, 딕셔너리]

  <a name="4-collection"></a>
  - **배열 리터럴 사용**: 배열 생성 시 리터럴 구문을 사용하여 가독성을 높입니다.

    ```csharp
    // Bad
    int[] numbers = new int[] { 1, 2, 3 };

    // Good
    int[] numbers = { 1, 2, 3 };
    ```

  - **List 사용**: 배열의 크기를 동적으로 관리할 때는 `List<T>`의 `Add` 메서드를 사용합니다.

    ```csharp
    List<int> numbers = new List<int>();
    numbers.Add(1);
    numbers.Add(2);
    ```

  - **타입 명시가 가능한 경우**: 직접적인 타입을 명시할 수 있다면 ArrayList 대신 List<T>를, Hashtable 대신 Dictionary<T>를 사용합니다.
---
**[⬆ back to top](#table-of-contents)**

## 5. 함수 (Functions)

  <a name="5-functions"></a>
  - **명시적 함수 선언**: 함수는 명시적으로 선언하여 디버깅에 유리하게 작성합니다.

    ```csharp
    // Bad
    Action myFunc = () => Debug.Log("Hello");

    // Good
    void MyFunc() {
        Debug.Log("Hello");
    }
    ```

  - **블록 스코프 내 함수 선언 피하기**: 함수는 블록 외부에서 선언하는 것이 일반적입니다.

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

## 6. 클래스 및 생성자 (Classes & Constructors)

  <a name="6-classes--constructors"></a>
  - **클래스 사용**: 명시적으로 클래스를 사용하여 코드를 구조화합니다.

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

  - **상속 구현**:  `:`를 사용하여 상속을 구현합니다.

    ```csharp
    class Enemy : Player {
        public Enemy(string name, int health){ }
    }
    ```

---
**[⬆ back to top](#table-of-contents)**

## 7. 조건식 및 비교 (Conditionals & Comparisons)

  <a name="7-conditionals--comparisons"></a>
  - **Equals 사용**: 객체 비교 시 `==` 연산자 대신 `Equals` 메서드를 사용합니다.

    ```csharp
    // Bad
    if (a == b) { }

    // Good
    if (a.Equals(b)) { }
    ```

  - **타입 체크 시 is 사용**: `var`로 받은 변수의 타입을 검사할 때 `is` 구문을 사용합니다.

    ```csharp
    if (fromPoint is string)
      Debug.Log("String 타입");
    ```

---
**[⬆ back to top](#table-of-contents)**

## 8. 공백 및 들여쓰기 (Whitespace & Indentation)

  <a name="8-whitespace--indentation"></a>
  - **Tab 들여쓰기 사용**: 들여쓰기는 Tab을 사용하여 가독성을 유지합니다.

    ```csharp
    void MyFunction() {
      if (true) {
          // Tab들여쓰기
      }
    }
    ```

---
**[⬆ back to top](#table-of-contents)**

## 9. 명명 규칙 (Naming Conventions)

  <a name="9-naming-conventions"></a>
  - **camelCase 및 PascalCase 사용**: 변수는 `camelCase`를, 함수나 클래스 이름은 `PascalCase`를 사용합니다.

    ```csharp
    int playerHealth;   // camelCase
    class PlayerCharacter {}   // PascalCase
    ```

---
**[⬆ back to top](#table-of-contents)**

## 10. 주석 (Comments)

  <a name="10-comments"></a>
  - **단일행 주석**: 단일 행 주석은 `//`로 작성하며, 설명이 필요한 경우 주석을 코드 상단에 배치합니다.

    ```csharp
    // 플레이어의 체력을 증가시킵니다.
    playerHealth += 10;
    ```

---
**[⬆ back to top](#table-of-contents)**

## 11. 조건문 및 블록 (Conditionals & Blocks)

  <a name="11-conditionals--blocks"></a>
  - **중괄호 사용**: 모든 조건문 및 반복문의 블록에는 중괄호 `{}`를 사용하여 명확한 코드 흐름을 유지합니다.

    ```csharp
    if (playerHealth > 0) {
      Debug.Log("체력감소");
    }
    ```

---
**[⬆ back to top](#table-of-contents)**

## 12. 파일 구조 (File Structure)

  <a name="12-file-structure"></a>
  - **파일당 하나의 클래스**: 각 파일은 하나의 클래스만 포함하며, 파일 이름은 클래스 이름과 동일하게 설정합니다.

    ```csharp
    // Player.cs
    public class Player {
      // 클래스 구현
    }
    ```

  - **네임스페이스 사용**: 클래스의 논리적 그룹화를 위해 네임스페이스를 사용합니다.

    ```csharp
    namespace GameNamespace {
      public class Player {
        // 클래스 구현
      }
    }
    ```

---
**[⬆ back to top](#table-of-contents)**

## 13. 오브젝트 생성 및 관리 (Object Creation and Management)

  <a name="13-object-creation-and-management"></a>
  - **빈 오브젝트 생성 후 위치 Reset**: 모든 빈 오브젝트는 생성 후 위치를 Reset합니다.

  - **오브젝트 이름 영어 사용**: 모든 빈 오브젝트의 이름은 영어를 지향하고 한글을 지양합니다.

  - **PascalCase 사용**: 모든 빈 오브젝트의 이름은 PascalCase를 사용하고 사용 의미에 알맞은 이름을 부여합니다.

    ```csharp
    // Bad
    move

    // Good
    MovePoint
    ```

---
**[⬆ back to top](#table-of-contents)**

## 14. 변수 선언 및 할당 (Variable Declaration and Assignment)

  <a name="14-variable-declaration-and-assignment"></a>
  - **변수 선언 순서**: 클래스 내부의 맨 위부터 선언합니다.

  - **Inspector에서 캐싱 여부에 따라 분류**: Inspector에서 직접 캐싱해주는 변수와 그렇지 않은 변수로 분류합니다.

  - **타입별 선언 순서**: GameObject, string, int, bool 타입 순서로 선언합니다.

**[⬆ back to top](#table-of-contents)**


## 15. 아트 리소스 기본 설정 (Basic Art Resource Setting)

  <a name="15-basic-art-resource-setting"></a>
  - **Image Resource Size**: 가로,세로 사이즈는 짝수 최소값으로 설정합니다.
    
  - **확장자**: .png로 설정합니다.

  - **맵의 위치**: 각 씬의 알맞은 이미지를 넣은 뒤에 Transform의 값을 Reset하여 (0,0,0) 으로설정합니다.
    
  - **Pixels per unit**: 모든 아트 리소스의 pixels per unit값은 1로 통일합니다.

  - **Pivot**: 모든 아트 리소스의 pivot값은 center로 통일합니다.
    
- **Import Setting**: 다음 설정은 모든 아트 리소스의 Import Setting에 적용됩니다.
  
  - **Max Size**: 아트 리소스의 가로, 세로 길이보다 작아지지 않는 선에서 최소값으로 설정합니다.
    
  - **Build 및 압축 형식**: ASTC방식 선택 (DXT방식은 선택 x - 손실이 발생하는 압축 형식), 4x4를 선택하여 품질을 최상으로 선택합니다. (12x12는 품질최하, 압축률 최고)
    
  - Defalut의 compression 기능(Mitchell, Automatic, NormalQuality, Use Crunch)을 사용하면 이미지가 깨짐(Max size 상관없이)
    

    
**[⬆ back to top](#table-of-contents)**

## 16. WebGL 빌드 기본 설정 (WebGL Build Basic Settings)

  <a name="16-webgl-build-basic-setting"></a>
- *Other Setting - Additional Compiler Arguments*
  - **Strip Engine Code**:  [v] / 사용하지 않는 코드 반영 안하는 기능
    
  - **Managed Stripping Level**: Minimal 로 설정
 
- *Publishing Setting*
  - **Compression Format**: Disabled 로 설정
    
  - **Data Caching**: [x]
    
  - **Decompression Fallback**: [x]
    
  - **Initial Memory Size**: 32 / 너무 큰 초기 값은 모바일 구동 X
    
  - **Memory Growth Mode**: Geometric 로 설정
    
  - **Maximum Memory Size**: 1024 ~ 2048 / 너무 크게 잡으면 모바일 부담

**[⬆ back to top](#table-of-contents)**
