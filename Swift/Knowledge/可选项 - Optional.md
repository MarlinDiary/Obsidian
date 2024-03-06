## 含义

可选项就像一个盒子，里面可能有东西，也可能没有。因此， `String?` 表示里面可能有一个字符串在等着我们，也可能什么都没有--一个叫做 `nil` 的特殊值，表示 "无值"。

任何类型的数据都可以是可选的，包括 `Int` 、 `Double` 和 `Bool` 以及[[枚举 - Enum]]、[[结构 - Struct]]和[[类 - Class]]的实例。

## 解包

### if let

Swift 提供了两种主要的可选项解包方法，但你最常见的是这种：

```swift
if let marioOpposite = opposites["Mario"] {
    print("Mario's opposite is \(marioOpposite)")
}
```

在解包可选项时，将其解包为同名常量是很常见的做法。

```swift
if let number = number {
    print(square(number: number))
}
```

### guard let

还有第二种方法可以做同样的事情，而且几乎同样常见： `guard let` 。

看起来是这样的：

```swift
func printSquare(of number: Int?) {
    guard let number = number else {
        print("Missing input")
        return
    }

    print("\(number) x \(number) is \(number * number)")
}
```

然而，它这样做的方式却让事情发生了翻天覆地的变化：

```swift
func printSquare(of number: Int?) {
    guard let number = number else {
        print("Missing input")

        // 1: We *must* exit the function here
        return
    }

    // 2: `number` is still available outside of `guard`
    print("\(number) x \(number) is \(number * number)")
}
```

### ??

```swift
let new = captains["Serenity"] ?? "N/A"
```

## 用可选链处理多个可选项

可选链的长度可以随心所欲，只要有任何部分发送回 `nil` ，代码的其余部分就会被忽略，并发送回 `nil` 。

```swift
struct Book {
    let title: String
    let author: String?
}

var book: Book? = nil
let author = book?.author?.first?.uppercased() ?? "A"
print(author)
```

#optional