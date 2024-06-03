这是一个专用 [[拾取器 - Picker]] 类型，可以绑定到日期（Date）属性。

首先要有一个 `@State` 属性：

```swift
@State private var wakeUp = Date.now
```

然后就可以像这样将其绑定到日期选择器上：

```swift
DatePicker("Please enter a date", selection: $wakeUp)
```

可以用 .labelsHidden [[修改器 - Modifier]] 删去左侧的标签。

## 日期选择器的配置

| 传入参数 | 用途 |
| ---- | ---- |
| displayedComponents | .date .hourAndMinute |
| in | 工作原理和 [[步进器 - Stepper]] 中的 in 相同，用于提供日期范围 |

## 日期范围的表示

双边范围：

```swift
func exampleDates() {
    // create a second Date instance set to one day in seconds from now
    let tomorrow = Date.now.addingTimeInterval(86400)

    // create a range from those two
    let range = Date.now...tomorrow
}
```

单边范围：

```swift
DatePicker("Please enter a date", selection: $wakeUp, in: Date.now...)
```

#swiftui #struct #hard 