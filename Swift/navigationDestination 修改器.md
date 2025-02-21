在导航的最简单形式中，我们在单个 [[导航链接 - NavigationLink]] 中同时提供**标签**和**目标视图**，但对于更高级的导航，最好将**目的地**与**值**分开。用原始的方法会导致过多的实例被创建。

这需要两个步骤：

1. 为 `NavigationLink` 附加一个**值**。这个值可以是你想要的**任何东西**。但有一个要求：无论使用什么类型，都必须符合 [[Hashable 协议]]。

```swift
NavigationStack {
    List(0..<100) { i in
        NavigationLink("Select \(i)", value: i)
    }
}
```

2. 在导航堆栈中附加 `navigationDestination()` 修饰符，告诉导航堆栈在收到**值**时怎么做。

```swift
NavigationStack {
    List(0..<100) { i in
        NavigationLink("Select \(i)", value: i)
    }
    .navigationDestination(for: Int.self) { selection in
        Text("You selected \(selection)")
    }
}
```

#swiftui #hard 