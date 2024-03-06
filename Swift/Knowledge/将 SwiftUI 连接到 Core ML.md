当您在 Xcode 中添加 .mlmodel 文件时，它会自动创建一个同名的 Swift [[类 - Class]]。您看不到这个类，也不需要看到，它是作为构建过程的一部分自动生成的。

1. 在使用之前，我们需要 import 一下，因为我们要使用 SwiftUI 以外的功能：

```swift
import CoreML
```

2. 我们需要创建一个 `SleepCalculator` 类的实例：

```swift
do {
    let config = MLModelConfiguration()
    let model = try SleepCalculator(configuration: config)

    // more code here
} catch {
    // something went wrong!
}
```

- configuration 的存在是为了以防万一，你需要启用一些相当晦涩难懂的选项
- 使用 `do` / `catch` 块，因为使用 Core ML 会在两个地方需要 [[处理 Function 中的错误]]：加载模型，以及我们要求预测时

3. 将我们的值输入 Core ML，这是使用模型的 `prediction()` 方法完成的：

```swift
let prediction = try model.prediction(wake: Double(hour + minute), estimatedSleep: sleepAmount, coffee: Double(coffeeAmount))
```

#swiftui #coreml #class 