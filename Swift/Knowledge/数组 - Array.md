## 修饰符

| 修饰符            | 作用                                   |
| -------------- | ------------------------------------ |
| .shuffled      | 随机调整数组顺序                             |
| .randomElement | 返回一个随机项（该随机字符串将会是[[可选项 - Optional]]） |
| .append        | 在数组末尾添加元素                            |
| .insert        | 在数组指定位置插入元素                          |
| .contains      | 根据数组是否包含该元素返回布尔值                     |
| .indices       | 为我们提供每个项目的位置                         |
| .first         | 访问集合中的第一个元素                          |

## 初始化器

- 重复一个值多次，以创建数组：

```swift
@State private var cards = Array<Card>(repeating: .example, count: 10)
```

#array 