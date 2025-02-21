## 方法一：format 参数

该参数在过去对我们非常有效（百分比、货币等），在这里我们可以要求显示日期的任何部分。

例如，如果我们只需要日期中的时间，我们可以这样写：

```swift
Text(Date.now, format: .dateTime.hour().minute())
```

如果我们想要日期、月份和年份，我们可以这样写：

```swift
Text(Date.now, format: .dateTime.day().month().year())
```

## 方法二：.formatted

我们可以直接在日期上使用 `formatted()` 方法，并传入配置选项，说明我们希望如何格式化日期和时间，就像这样：

```swift
Text(Date.now.formatted(date: .long, time: .shortened))
```

#swiftui #struct #easy 