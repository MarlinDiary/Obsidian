## 父类继承

- 如果子类想要更改父类的方法，则必须在子类的版本中使用 `override`
- 如果子类有任何自定义初始化器，那么它必须在设置完自己的属性（如果有的话）后，始终调用父类的初始化器

```swift
class Car: Vehicle {
    let isConvertible: Bool

    init(isElectric: Bool, isConvertible: Bool) {
        self.isConvertible = isConvertible
        super.init(isElectric: isElectric)
    }
}

// super 是对父类的调用
```

## Deinitializer

只有在类实例的最后一个引用被销毁时，才会调用去初始化器

#class 