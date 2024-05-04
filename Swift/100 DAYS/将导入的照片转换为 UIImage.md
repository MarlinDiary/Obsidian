结合 [[导入照片 - PhotosPicker]] 和 [[Core Image 框架]] ，我们应该加载一个纯 `Data` 对象，并将其转换为 `UIImage` 。

```swift
func loadImage() {
    Task {
        guard let imageData = try await selectedItem?.loadTransferable(type: Data.self) else { return }
        guard let inputImage = UIImage(data: imageData) else { return }

        // more code to come
    }
}
```

#swiftui 