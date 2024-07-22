泛型允许我们编写能够处理各种不同**类型**的代码，让代码更有通用性。

1. 提供占位符（用角括号写在方法名称之后、参数之前）

```swift
func decode<T>(_ file: String) -> [String: Astronaut] {
```

2. 在方法内部，我们现在要在所有需要的地方用 T 作为占位符

```swift
func decode<T>(_ file: String) -> T {
```

3. 可以让泛型符合某种 [[协议 - Protocol]]

```swift
func decode<T: Codable>(_ file: String) -> T {
```

4. 类型推断会失效，所以在使用时要配合 [[类型注解特例|类型注释]]

```swift
let astronauts: [String: Astronaut] = Bundle.main.decode("astronauts.json")
```

使用好泛型的关键在于**一开始**不要使用它们。

#generics #hard 