这些绑定具有**固定值**，一方面意味着它们不能在用户界面中更改，另一方面也意味着我们可以轻松创建它们--它们非常适合预览。

```swift
#Preview {
    RatingView(rating: .constant(4))
}
```

常量绑定也可以用作把可交互的视图变为只读视图。

```swift
RatingView(rating: .constant(book.rating))
```

#swiftui 