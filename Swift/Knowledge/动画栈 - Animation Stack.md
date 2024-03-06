将「[[修改器 - Modifier#Modifier 的顺序很重要]]」和「[[隐式动画 - implicit animation]]」两个概念相结合，可以的得出以下结论：**您可多次附加 `animation()` 修饰符，但使用顺序很重要**。

- 只有在 `animation()` 修饰符之前发生的更改才会被动画化
- 应用多个 `animation()` 时，每个修改器都会控制之前的所有内容至上一个动画

#animation 