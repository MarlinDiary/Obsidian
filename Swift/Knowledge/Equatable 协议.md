在幕后，Swift 会将每个属性与其他属性进行比较，但这是相当浪费的。

因此，类似于[[Comparable 协议]]，我们可以编写自己的 `==` 函数，从而节省大量工作：

```swift
static func ==(lhs: Location, rhs: Location) -> Bool {
    lhs.id == rhs.id
}
```

#protocol 