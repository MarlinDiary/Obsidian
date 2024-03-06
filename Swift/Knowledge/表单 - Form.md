表单是一个由 [[结构 - Struct]] 创建的 Type，是文本和图像等静态控件的滚动列表，但也可以包括文本字段、切换开关、按钮等用户交互式控件。

```swift
Form {
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
    Text("Hello, world!")
}
```

如果您想将表单分割成可视化块，就像设置应用所做的那样，您可以像这样使用 `Section` ：

```swift
Form {
    Section("可以加标题") {
        Text("Hello, world!")
    }

    Section {
        Text("Hello, world!")
        Text("Hello, world!")
    }
}
```

表单还可以和 [[堆栈 - Stack]] 结合使用，例如让文字和步进器放在同一个模块中：

```swift
VStack(alignment: .leading, spacing: 0) {
    Text("Desired amount of sleep")
        .font(.headline)

    Stepper("\(sleepAmount.formatted()) hours", value: $sleepAmount, in: 4...12, step: 0.25)
}
```

#struct #swiftui 