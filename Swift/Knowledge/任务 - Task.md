[[按钮 - Button]]不可以直接运行[[异步函数 - Asynchronous Function]]，但我们可以借助 Task() 实现。

就像使用 `task()` 修饰符一样，它可以运行我们想要的任何异步代码。

```swift
Button("Place Order") {
    Task {
        await placeOrder()
    }
}
```

#data 