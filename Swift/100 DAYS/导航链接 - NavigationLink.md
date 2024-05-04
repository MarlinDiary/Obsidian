SwiftUI 的 [[导航 - Navigation|NavigationStack]] 在视图的顶部显示了一个导航栏，但它还可以做其他事情：**将[[视图 - View]]推送到[[堆栈 - Stack]]中**。

这种视图堆栈系统与我们之前使用的[[弹出窗口 - sheet]]非常不同。没错，两者都显示了某种新的视图，但它们的显示方式不同，会影响用户对它们的看法。

NavigationLink 的使用非常简单，给它一个**目的地**和**可以点击的东西**，它会处理剩下的事情：

```swift
NavigationStack {
    NavigationLink("Tap Me") {
        Text("Detail View")
    }
    .navigationTitle("SwiftUI")
}
```

如果不希望用简单的文本视图作为标签，可在 `NavigationLink` 中使用两个尾部[[闭包 - Closure]]：

```swift
NavigationStack {
    NavigationLink {
        Text("Detail View")
    } label: {
        VStack {
            Text("This is the label")
            Text("So is this")
            Image(systemName: "face.smiling")
        }
        .font(.largeTitle)
    }
}
```

您最常见到的 `NavigationLink` 是[[列表 - List]]：

```swift
NavigationStack {
    List(0..<100) { row in
        NavigationLink("Row \(row)") {
            Text("Detail \(row)")
        }
    }
    .navigationTitle("SwiftUI")
}
```

#swiftui 