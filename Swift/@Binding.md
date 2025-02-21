通过 `@Binding` [[属性包装器]]，我们可以将 `@State` 属性传递到另一个[[视图 - View]]中，并在其中对其进行修改。

这意味着，在**接受**属性的视图中添加：

```swift
@Binding var path: [Int]
```

在**传入**属性的地方添加：

```swift
DetailView(number: 0, path: $path)
```

#swiftui #easy 