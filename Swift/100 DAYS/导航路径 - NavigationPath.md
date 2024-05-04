导航到不同的数据类型有两种形式。

最简单的形式是用 [[navigationDestination 修改器]]访问不同的数据类型，但不跟踪显示的确切路径，因为操作很简单：只需多次添加 `navigationDestination()` 即可，每种数据类型添加一次。

不过，当你想添加[[程序化导航 - programmatic navigation]]，并有多种数据类型的时候，情况就会变得复杂。SwiftUI 的解决方案是一种名为 `NavigationPath` 的特殊类型，它可以在单个路径中容纳多种数据类型。

它的工作原理与[[数组 - Array]]非常相似，我们可以使用它创建一个属性：

```swift
@State private var path = NavigationPath()
```

将其绑定到 `NavigationStack` ：

```swift
NavigationStack(path: $path) {
```

然后以编程方式，例如使用工具栏按钮，向其推送内容：

```swift
.toolbar {
    Button("Push 556") {
        path.append(556)
    }

    Button("Push Hello") {
        path.append("Hello")
    }
}
```

`NavigationPath` 就是我们所说的 **type-eraser** -- 它可以存储任何类型的 `Hashable` 数据，而不会暴露每个项目的具体数据类型。

#swiftui 