[[导航 - Navigation|NavigationStack]] 可以创建分层的视图堆栈，让用户深入研究数据。但在显示不相关的数据时，需要使用 SwiftUI 的 `TabView` 来创建横跨屏幕底部的按钮带，点击每个按钮都会显示不同的视图。

## 点击标签切换视图

1. 在 `TabView` 内放置 Tabs 非常简单，只需像这样逐个列出即可：

```swift
TabView {
    Text("Tab 1")
    Text("Tab 2")
}
```

2. 为 `TabView` 中的每个视图附加 `tabItem()` 修饰符就可以自定义视图在标签栏中的显示方式：

```swift
TabView {
    Text("Tab 1")
        .tabItem {
            Label("One", systemImage: "star")
        }

    Text("Tab 2")
        .tabItem {
            Label("Two", systemImage: "circle")
        }
}
```

## 编程方式切换视图

1. 创建一个 `@State` 属性，用于跟踪当前显示的 Tab：

```swift
@State private var selectedTab = "One"
```

2. 只要想跳转到不同的 Tab，就可以将该属性修改为新值：

```swift
Button("Show Tab 2") {
    selectedTab = "Two"
}
.tabItem {
    Label("One", systemImage: "star")
}
```

3. 将其作为一个绑定项传入 `TabView` 中，这样它就会被自动跟踪：

```swift
TabView(selection: $selectedTab) {
```

4. 借助 `tag()` 修饰符，告诉 SwiftUI 每个属性值应显示哪个 Tab：

```swift
Text("Tab 2")
    .tabItem {
        Image(systemName: "circle")
        Text("Two")
    }
    .tag("Two")
```

## 提示

同时使用 `NavigationStack` 和 `TabView` 是很常见的情况，但应小心谨慎： `TabView` 应该是父视图，其内部的 Tabs 需要使用 `NavigationStack` ，而不是相反。

#swiftui #easy 