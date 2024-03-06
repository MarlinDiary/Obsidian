我们有以下这样一个结构（自定义类型）：

```swift
struct User: Identifiable {
    let id = UUID()
    var firstName: String
    var lastName: String
}
```

如果想直接进行排序，这样的代码是行不通的：

```swift
let users = [
    User(firstName: "Arnold", lastName: "Rimmer"),
    User(firstName: "Kristine", lastName: "Kochanski"),
    User(firstName: "David", lastName: "Lister"),
].sorted()
```

一种方法是为 sorted 提供一个[[闭包 - Closure]]：

```swift
let users = [
    User(firstName: "Arnold", lastName: "Rimmer"),
    User(firstName: "Kristine", lastName: "Kochanski"),
    User(firstName: "David", lastName: "Lister"),
].sorted {
    $0.lastName < $1.lastName
}
```

但这不是理想的解决方案，原因有二：

1. 我们不会想在 SwiftUI 代码中告诉模型它应该如何运行，因为 SwiftUI 代表我们的布局。
2. 如果我们想在多个地方对 `User` 数组进行排序，闭包将不能同步更新。

**更好的方法**是让自己的类型符合 `Comparable` ，这样可以得到一个不带参数的 `sorted()` 方法。

这需要两个步骤：

1. 在 `User` 的定义中加入 `Comparable` [[协议 - Protocol]] 的一致性。
2. 添加一个名为 `<` 的方法。

代码如下：

```swift
struct User: Identifiable, Comparable {
    let id = UUID()
    var firstName: String
    var lastName: String

    static func <(lhs: User, rhs: User) -> Bool {
        lhs.lastName < rhs.lastName
    }
}
```

1. 这个方法的确只是在调用 **<**，是在为现有的运算符添加功能（操作符重载）；
2. **lhs** 和 **rhs** 分别是 left hand side 和 right hand side 的约定缩写；
3. 这个方法必需返回一个 **Boolean**；
4. 必须标记为 **static** ，这意味着它是直接在结构上调用，而不是在结构的单个实例上调用；

#protocol 