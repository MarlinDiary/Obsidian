为了避免涉及到夏令时、闰秒和公历等复杂的情况，我们应当把程序中与日期相关的使用交给苹果的框架，即 Calendar。

除了 [[日期拾取器 - DatePicker|Date 类型]] 外，Swift 还提供了 DateComponents 类型，它允许我们**读取或写入日期的特定部分**，而不是整个日期。

## 写入日期的特定部分

如果我们想要一个代表上午 8 点的日期，我们可以这样编写代码：

```swift
var components = DateComponents()
components.hour = 8
components.minute = 0
let date = Calendar.current.date(from: components)
```

`date(from:)` 方法实际上返回的是一个[[可选项 - Optional]]的日期，因此使用 nil coalescing 来表示 "如果失败，就返回当前日期 "是个好主意：

```swift
let date = Calendar.current.date(from: components) ?? .now
```

## 读取日期的特定部分

我们可以请求小时和分钟，但我们仍然需要拆开[[可选项 - Optional]]或提供默认值：

```swift
let components = Calendar.current.dateComponents([.hour, .minute], from: someDate)
let hour = components.hour ?? 0
let minute = components.minute ?? 0
```

此处的 `Calendar.current` 返回的是一个表示当前设备的日历系统的`Calendar`对象，而不是表示"今天"的日期。这个"当前"更多的是指当前的日历系统，比如公历或者儒略历等。

#swiftui #type