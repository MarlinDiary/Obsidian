有两个方法：

1. 如果您使用一个简单的[[数组 - Array]]作为路径，您可以在该数组上调用 `removeAll()` 来删除路径中的所有内容，返回到根视图：

```swift
.toolbar {
    Button("Home") {
        path.removeAll()
    }
}
```

1. 如果使用 [[导航路径 - NavigationPath]] 作为路径，则可以将其设置为 `NavigationPath` 的一个新的空实例：

```swift
.toolbar {
    Button("Home") {
        path = NavigationPath()
    }
}
```

但还有一个更大的问题需要解决：**在无法访问原始 `path` 属性的情况下，如何从子视图中实现这一功能？**

有两个方法：

1. 将路径存储在使用 @Observable 的外部[[类 - Class]]中
2. 引入一个名为 [[@Binding]] 的新[[属性包装器]]

#swiftui #easy 