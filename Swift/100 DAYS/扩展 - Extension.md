## 适用范围

Swift 中的扩展（`extension`）不仅仅适用于[[协议 - Protocol]]，它们也可以用于[[类 - Class]]、[[结构 - Struct]]和[[枚举 - Enum]]。

## 作用

我们可以在协议中列出一些必要的方法，然后在协议扩展中添加这些方法的**默认实现**。然后，所有符合要求的类型都可以使用这些默认实现，或根据需要提供自己的实现。

```swift
protocol Person {
    var name: String { get }
    func sayHello()
}
```

```swift
extension Person {
    func sayHello() {
        print("Hi, I'm \(name)")
    }
}
```

我们还可以添加新的方法和属性。

```swift
extension Collection {
    var isNotEmpty: Bool {
        isEmpty == false
    }
}
```

#class  #struct  #enum #easy 