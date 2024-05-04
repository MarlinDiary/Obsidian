如果您想从互联网加载远程图片，则需要使用 `AsyncImage`，而不是 [[图像 - Image|图像视图]] 。

我们可以创建的最简单的图像是这样的：

```swift
AsyncImage(url: URL(string: "https://hws.dev/img/logo.png"))
```

## 调整异步图像大小的方法

1. 方法一：提前告诉 SwiftUI 我们正在尝试加载 3 倍比例的图像

```swift
AsyncImage(url: URL(string: "https://hws.dev/img/logo.png"), scale: 3)
```

2. 方法二：通过[[闭包 - Closure]]的方式来处理图像和占位符（可用 ProgressView 占位）

```swift
AsyncImage(url: URL(string: "https://hws.dev/img/logo.png")) { image in
    image
        .resizable()
        .scaledToFit()
} placeholder: {
    ProgressView()
}
.frame(width: 200, height: 200)
```

3. 方法三：对视图的各个阶段（phase）进行管理

```swift
AsyncImage(url: URL(string: "https://hws.dev/img/bad.png")) { phase in
    if let image = phase.image {
        image
            .resizable()
            .scaledToFit()
    } else if phase.error != nil {
        Text("There was an error loading the image.")
    } else {
        ProgressView()
    }
}
.frame(width: 200, height: 200)
```

#data 