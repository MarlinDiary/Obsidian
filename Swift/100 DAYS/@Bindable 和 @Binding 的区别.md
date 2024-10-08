[[@Bindable]] 用于访问使用 `@Observable` 宏的共享[[类 - Class]]：您可以在一个视图中使用 `@State` 创建该类，这样您就可以在该视图中创建绑定，但在与其他视图共享时，您可以使用 `@Bindable` 创建该类，这样 SwiftUI 也可以在该视图中创建绑定。

[[@Binding]] 适用于简单的值类型数据，而不是单独的类。例如，您有一个存储布尔值的 `@State` 属性、一个存储字符串数组的 `Double` 属性等，您希望将它们传递给他人。这并不使用 `@Observable` 宏，因此我们不能使用 `@Bindable` 。相反，我们可以使用 `@Binding` ，这样就可以在多个地方共享布尔值或整数。

`@Binding` 在要创建自定义用户界面组件时变得极为重要，@Binding 属性使它们能够直接与其他视图接口。

#swiftui #easy 