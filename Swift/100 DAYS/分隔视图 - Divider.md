一种内置的[[视图 - View]]，用于在布局中创建视觉分隔，但它不可自定义，始终只是一条细线。

当然，也可以自定义分隔视图：

```swift
Rectangle()
    .frame(height: 2)
    .foregroundStyle(.lightBackground)
    .padding(.vertical)
```

#swiftui 