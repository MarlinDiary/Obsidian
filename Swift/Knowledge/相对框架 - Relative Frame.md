比起硬编码宽度为 300，有的时候，你真正想说的是 "让这张[[图像 - Image]]占满屏幕宽度的 80%"。

SwiftUI 提供了一个专用的 `containerRelativeFrame()` [[修改器 - Modifier]]，其中的 container 可能是整个屏幕，但也可能只是该视图的父级视图所占屏幕的部分。

我们可以制作一张宽度为屏幕 80% 的图片：

```swift
Image(.example)
    .resizable()
    .scaledToFit()
    .containerRelativeFrame(.horizontal) { size, axis in
        size * 0.8
    }
```

1. 我们要给这幅图像一个相对于其父视图水平（horizontal）尺寸的框架；
2. `size` 值将是我们容器的大小；
3. 我们需要为这个 axis 返回我们想要的尺寸，因此我们返回了容器宽度的 80%。

#swiftui 