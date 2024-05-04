我们可以使用 `+` 将文本视图添加到一起，这样就可以创建混合并匹配不同格式的大视图：

```swift
Text(page.title)
    .font(.headline)
+ Text(": ") +
Text("Page description here")
    .italic()
```

#swiftui 