导航是一个由 [[结构 - Struct]] 创建的 Type。

## NavigationStack

```swift
var body: some View {
    NavigationStack {
        Form {
            Section {
                Text("Hello, world!")
            }
        }
    }
}
```

## 修饰符

| 修饰符 | 作用 |
| ---- | ---- |
| `.navigationTitle()` | 用于添加标题 |
| `.navigationBarTitleDisplayMode()` | 用于修改标题的显示方式 |
| `.toolbar()` | 用于定制工具栏 |

以上修饰符用于修饰 NavigationStack 内部的组件。

#struct  #swiftui #easy 