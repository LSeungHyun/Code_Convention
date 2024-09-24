# LedaGames Unity C#Script Style Guide() {

*A mostly reasonable approach to JavaScript*
# LedaGames Unity C# Script Style Guide

## 1. 타입(Types)

### 1.1 기본형
- Unity C#의 기본형에는 `int`, `float`, `double`, `bool`, `string`, `char` 등이 있으며, 이러한 타입들은 값이 직접적으로 조작됩니다.

```csharp
int a = 10;
int b = a;
b = 20;
Debug.Log(a); // 출력: 10
Debug.Log(b); // 출력: 20
