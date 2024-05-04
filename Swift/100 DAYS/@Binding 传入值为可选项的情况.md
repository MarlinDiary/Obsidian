[[@Binding]] 的传入值不可以是 [[可选项 - Optional]]。

最简单的解决方案：**一个可以传回新数据的函数**。

1. 将此属性添加到 `SecondView` 中：

```swift
var onSave: (Location) -> Void
```

2. 修改初始化器：

```swift
init(location: Location, onSave: @escaping (Location) -> Void) {
    self.location = location
    self.onSave = onSave

    _name = State(initialValue: location.name)
    _description = State(initialValue: location.description)
}
```

`@escaping` 部分非常重要，它意味着该函数将被保存起来，供用户稍后使用，而不是立即调用。

这里需要它是因为 `onSave` 函数只有在用户按下保存时才会被调用。

3. 更新 Button，使之创建一个修改后的新数据：

```swift
    var newLocation = location
    newLocation.name = name
    newLocation.description = description

    onSave(newLocation)
```

4. 在 ContentView 中用[[闭包 - Closure]]的方式处理 newLocation：

```swift
EditView(location: place) { newLocation in
    if let index = locations.firstIndex(of: place) {
        locations[index] = newLocation
    }
}
```

#struct 