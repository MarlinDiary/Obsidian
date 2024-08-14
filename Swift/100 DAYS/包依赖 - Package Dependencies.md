包依赖让我们可以获取第三方代码并将其用于我们的项目中。

Xcode 内置了一个包依赖管理器，名为 Swift Package Manager (SPM)。您可以告诉 Xcode 在线存储的代码的 URL，它就会帮您下载。您甚至可以告诉它要下载的版本，这意味着如果远程代码在未来某个时候发生变化，您可以确保它不会破坏您现有的代码。

1. 将 package 添加到项目：File → Add Package Dependencies → Input URL → Up to Next Major Version → Add Package → Add Package

2. 如果要使用的话，需要在顶部添加导入：

```swift
import SamplePackage
```

是的，外部依赖现在是一个 module，我们可以在任何需要的地方导入它。

3. 如果需要浏览源代码，可以在 Xcode 中访问 Sources

#swiftui #easy 