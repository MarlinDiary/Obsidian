有时，您希望点击 [[列表 - List]] 时只是**选择**一个项目，这样您就可以在稍后进行某种操作。

这是一个简单的 `List` ，没有选择项，只显示几个字符串：

```swift
struct ContentView: View {
    let users = ["Tohru", "Yuki", "Kyo", "Momiji"]

    var body: some View {
        List(users, id: \.self) { user in
            Text(user)
        }
    }
}
```

## 单选

1. 创建一些状态来存储被点击的行为：

```swift
@State private var selection: String?
```

2. 告诉列表在点击一行时更新该状态：

```swift
List(users, id: \.self, selection: $selection) { user in
    Text(user)
}

//双向绑定意味着点击一行会更新属性，但同时更新属性也会选择该行。
```

3. 可以以某种方式使用该选区：

```swift
if let selection {
    Text("You selected \(selection)")
}
```

## 多选

1. 如果要升级为处理多选，则需要更改 `selection` 属性，使其存储一组值：

```swift
@State private var selection = Set<String>()
```

2. `EditButton` 能自动[[删除项目 - onDelete|启用或禁用编辑]]，也能启用或禁用多选模式：

```swift
EditButton()
```

#swiftui #easy 