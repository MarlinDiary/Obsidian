TextField 是一种[[结构 - Struct]]，用于输入文本。

```swift
.currency(code: Locale.current.currency?.identifier ?? "USD"))
```

## 修饰符

| 修饰符                                    | 用法              |
| -------------------------------------- | --------------- |
| `.keyboardType()`                      | 通过 enum 调用具体的键盘 |
| `.textInputAutocapitalization(.never)` | 禁用首字母大写         |
| `.textContentType()`                   | 为用户自动填充信息       |

#struct #swiftui #easy 