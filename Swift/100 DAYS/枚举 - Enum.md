## 创建 Enum

```swift
enum Weekday {
    case monday, tuesday, wednesday, thursday, friday
}
```

## 调用 Enum

```swift
var day = Weekday.monday
day = .tuesday
day = .friday
```

## 带关联值的枚举

```swift
enum Item { case text(String) } 

let textA: Item = .text("a")
```

#enum #hard 