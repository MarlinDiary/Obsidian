`PhotosPicker` 视图为我们提供了一种从用户照片库中导入一张或多张照片的简单方法。

为避免造成性能问题，数据将以名为 `PhotosPickerItem` 的特殊类型提供给我们，然后我们可以[[异步函数 - Asynchronous Function|异步加载]]该类型，将数据转换为 SwiftUI 图像。

## 导入单个照片

1. 为 PhotosUI 添加一个导入。

```swift
import PhotosUI
import SwiftUI
```

2. 创建两个属性（一个用于存储所选项目，另一个用于将所选项目存储为 SwiftUI 图像）。

```swift
@State private var pickerItem: PhotosPickerItem?
@State private var selectedImage: Image?
```

3. 添加一个 `PhotosPicker` 视图（Title + Binding + Type）。

```swift
VStack {
    PhotosPicker("Select a picture", selection: $pickerItem, matching: .images)
}
```

4. 观察 `pickerItem` 的变化（[[onChange 修改器]] + [[任务 - Task]]）。

```swift
.onChange(of: pickerItem) {
    Task {
        selectedImage = try await pickerItem?.loadTransferable(type: Image.self)
    }
}
```

5. 在某处显示加载的 SwiftUI 图像。

```swift
selectedImage?
    .resizable()
    .scaledToFit()
```

## 导入多个照片

1. 这意味着需要创建一个Picker Item 数组作为属性：

```swift
@State private var pickerItems = [PhotosPickerItem]()
```

2. 然后像之前一样将数组传入：

```swift
PhotosPicker("Select images", selection: $pickerItems, matching: .images)
```

3. 创建一个数组来存储加载的图片：

```swift
@State private var selectedImages = [Image]()
```

4. 使用 `ForEach` 或类似字符显示它们：

```swift
ScrollView {
    ForEach(0..<selectedImages.count, id: \.self) { i in
        selectedImages[i]
            .resizable()
            .scaledToFit()
    }
}
```

5. 更新 `onChange()` 以便在选择新项目时先清空该数组：

```swift
.onChange(of: pickerItems) {
    Task {
        selectedImages.removeAll()

        for item in pickerItems {
            if let loadedImage = try await item.loadTransferable(type: Image.self) {
                selectedImages.append(loadedImage)
            }
        }
    }
}
```

6. 可以用 maxSelectionCount 来限制一次实际可选择的照片数量：

```swift
PhotosPicker("Select images", selection: $pickerItems, maxSelectionCount: 3, matching: .images)
```

## 自定义 PhotosPicker

1. 标签：可能是 `Label` 视图或完全自定义的标签（可把已选中的图片作为标签）。

```swift
PhotosPicker(selection: $pickerItems, maxSelectionCount: 3, matching: .images) {
    Label("Select a picture", systemImage: "photo")
}
```

2. 限制可以导入的图片类型：你可以使用 `.any()` 、 `.all()` 和 `.not()` 应用更高级的过滤器，并将它们传递到一个数组中。

```swift
PhotosPicker(selection: $pickerItems, maxSelectionCount: 3, matching: .any(of: [.images, .not(.screenshots)])) {
    Label("Select a picture", systemImage: "photo")
}
```

#framework #swiftui #easy 