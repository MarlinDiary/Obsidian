SF 符号提供了从 0 到 50 的**圆圈数字**，所有数字都使用 "x.circle.fill" 格式命名--例如 1.circle.fill, 20.circle.fill。

我们可以通过 [[图像 - Image]] 的第三种方式来调用：

```swift
Image(systemName: "\(word.count).circle")
```

另外，我们可以通过一个简单的 `font()` 修改器将 SF Symbol 无缝缩放：

```swift
.font(.largeTitle)
```

#swiftui #easy 