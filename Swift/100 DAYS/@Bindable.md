对于一个[[类 - Class]]属性，我们没在子视图使用 @State 属性包装器是因为我们没在这里创建类，我们只是接受类。

`@Bindable` 属性包装器的作用就是为我们生成双向绑定，与 [[属性包装器#@Observable|@Observable]] 宏配合使用，而无需使用 `@State` 来创建本地数据。

#swiftui 