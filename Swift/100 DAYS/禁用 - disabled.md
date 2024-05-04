SwiftUI 的 [[表单 - Form]] 视图可让我们以一种非常快速和方便的方式存储用户输入，但有时需要更进一步，即在继续操作前检查输入以确保其有效。

`disabled()` 修改器需要一个条件来检查，如果条件为真，那么它所连接的任何东西都不会响应用户的输入。

比如可以将以下修饰符附在一个按钮上：

```swift
.disabled(username.isEmpty || email.isEmpty)
```

也可以更复杂些，用计算属性：

```swift
var disableForm: Bool {
    username.count < 5 || email.count < 5
}
```

```swift
.disabled(disableForm)
```

#swiftui 