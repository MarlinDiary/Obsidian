有两种让用户输入数字的方式，Stepper 和 Slider。其中，`Stepper` 是一个简单的 - 和 + 按钮，点击它可以选择一个精确的数字。

步进器非常聪明，可以处理任何类型的数字，因此您可以将其绑定到 `Int` 、 `Double` 等，而且它会自动适应。

我们可以创建这样一个属性：

```swift
@State private var sleepAmount = 8.0
```

然后，我们可以将其绑定到步进器上：

```swift
Stepper("\(sleepAmount) hours", value: $sleepAmount)
```

`Stepper` 允许我们通过提供 `in` 范围来限制我们想要接受的值：

```swift
Stepper("\(sleepAmount) hours", value: $sleepAmount, in: 4...12)
```

`Stepper` 还有第四个有用的参数，`step` 值：

```swift
Stepper("\(sleepAmount) hours", value: $sleepAmount, in: 4...12, step: 0.25)
```

格式化浮点数字时可能要用到 formatted [[修改器 - Modifier]]。

#swiftui #struct 