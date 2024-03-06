`List` 的作用是提供一个滚动的数据表。事实上，它与 [[表单 - Form]] 几乎完全相同，只是它用于显示数据而不是请求用户输入。

就像 `Form` 一样，您可以提供 `List` 静态视图（显示上和 Form 没有任何区别）：

```swift
List {
    Text("Hello World")
    Text("Hello World")
    Text("Hello World")
}
```

但与 Form 不同的是，我们可以使用 [[修改器 - Modifier]] 调整 List 的外观：

```swift
.listStyle(.grouped)
```

并且，`List` 能做的一件事是 `Form` 所不能做的，那就是完全通过动态内容生成行时，我们不需要 [[循环视图 - ForEach]]：

```swift
List(0..<5) {
    Text("Dynamic row \($0)")
}
```

`id` 参数在 `List` 和 `ForEach` 中的作用完全相同--它可以让我们准确地告诉 SwiftUI [[数组 - Array]] 中每个项目的唯一性：

```swift
struct ContentView: View {
    let people = ["Finn", "Leia", "Luke", "Rey"]

    var body: some View {
        List(people, id: \.self) {
            Text($0)
        }
    }
}
```

当然，如果我们想混合使用静态行和动态行，我们仍然可以这样写：

```swift
List {
    Text("Static Row")

    ForEach(people, id: \.self) {
        Text($0)
    }

    Text("Static Row")
}
```

#swiftui #struct 