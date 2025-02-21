您可以使用 `ToolbarItem` 自定义 toolbar [[按钮 - Button]] 的位置。

我们可以这样要求左侧的位置：

```swift
NavigationStack {
    Text("Hello, world!")
    .toolbar {
        ToolbarItem(placement: .topBarLeading) {
            Button("Tap Me") {
                // button action here
            }
        }
    }
}
```

虽然这样做效果很好，但通常情况下，最好还是使用**语义选项**：

| 修饰符 | 作用 |
| ---- | ---- |
| .confirmationAction | 当您希望用户同意某些内容 |
| .destructiveAction | 当用户需要选择销毁他们正在处理的任何内容 |
| .cancellationAction | 当用户需要撤销所做的更改 |
| .navigation | 让用户在数据间移动（浏览器中前进和后退） |

如果需要放在相同的位置，可以**重复**使用：

```swift
.toolbar {
    ToolbarItem(placement: .topBarLeading) {
        Button("Tap Me") {
            // button action here
        }
    }

    ToolbarItem(placement: .topBarLeading) {
        Button("Or Tap Me") {
            // button action here
        }
    }
}
```

或者使用 `ToolbarItemGroup`：

```swift
.toolbar {
    ToolbarItemGroup(placement: .topBarLeading) {
        Button("Tap Me") {
            // button action here
        }

        Button("Tap Me 2") {
            // button action here
        }
    }
}
```

#swiftui #hard 