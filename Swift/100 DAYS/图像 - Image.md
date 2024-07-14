创建图片的方式主要有三种：

1. `Image("pencil")` 将加载您添加到项目中的名为 "铅笔" 的图像；
2. `Image(decorative: "pencil")` 将加载相同的图片，但不会为启用了屏幕阅读器的用户读出图片，这对于不传递其他重要信息的图片非常有用；
3. `Image(systemName: "pencil")` 将加载 iOS 内置的铅笔图标。

## 修饰符

| 修饰符 | 作用 |
| ---- | ---- |
| .scaledToFit() | 整个图像将适合容器，即使这意味着视图的某些部分是空的 |
| .scaledToFill() | 视图将没有空的部分，即使这意味着我们的某些图像位于容器之外 |

#struct #swiftui #easy 