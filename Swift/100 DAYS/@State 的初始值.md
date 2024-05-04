我们使用 `@State` 时，要先赋予一个初始值。

但有时不能这样做--它们的初始值可能需要来自所传入的内容。

解决方法是创建一个新的**初始化器**，该初始化器接受相关数据，并使用该数据创建 `State` 结构。

这与我们在初始化器中创建 [[对 @Query 进行动态排序和筛选|SwiftData]] 查询时使用的**下划线方法**相同，它允许我们创建一个[[属性包装器]]实例（**操作属性包装器本身**），而不是包装器中的数据。

以下是一个初始化器的例子：

```swift
init(location: Location) {
    self.location = location

    _name = State(initialValue: location.name)
    _description = State(initialValue: location.description)
}
```

#struct 