如果 [[图像 - Image|Image]] 被拉伸到大于原始尺寸，会默认开启图像插值，即 iOS 会将像素平滑地混合在一起。

不过，图像插值会在处理精确像素时造成问题。

SwiftUI 提供了 `interpolation()` 修改器，可以控制像素混合的应用方式。其中，`.none` 将完全关闭图像插值功能，因此像素不会混合，只会按比例放大，并带有锐利的边缘。

```swift
Image(.example)
    .interpolation(.none)  
```

#swiftui 