SwiftUI 提供了一个名为 `.requestReview` 的特殊环境键，通过该键，我们可以请求用户在 App Store 上为我们的应用程序留下评论。

这个过程需要三个步骤：

1. 导入 StoreKit。

```swift
import StoreKit
```

2. 添加一个属性，用于从 SwiftUI 的环境中读取评分请求者。

```swift
@Environment(\.requestReview) var requestReview
```

3. 请求评分。

```swift
Button("Leave a review") {
    requestReview()
}
```

提示：按钮不是一个好的选择，最好是在您认为适当的时候自动调用 `requestReview()` 。

4. 如果在使用时，Swift UI 提示关于 MainActor 的错误，只需做出轻微改动。

```swift
@MainActor func
```

#swiftui #easy 