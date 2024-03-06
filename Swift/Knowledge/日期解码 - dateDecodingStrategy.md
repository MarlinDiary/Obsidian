这是 JSONDecoder 的一个属性，它决定了日期的解码方式。我们可以提供一个 [[格式化日期 - DateFormatter]] 实例来描述日期的格式化方式。

```swift
let decoder = JSONDecoder()

let formatter = DateFormatter()
formatter.dateFormat = "y-MM-dd"
decoder.dateDecodingStrategy = .formatted(formatter)
```

现在，我们的解码代码已经理解了日期的格式化方式，我们可以将日期属性改为 `Date` ：

```swift
let launchDate: Date?
```

当然，该日期可以用以下方式格式化为字符串：

```swift
var formattedLaunchDate: String {
    launchDate?.formatted(date: .abbreviated, time: .omitted) ?? "N/A"
}
```

#data 