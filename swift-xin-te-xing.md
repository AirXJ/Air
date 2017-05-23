##### _**swift循环有标记, 循环或者条件选择后面可以再加个条件;判断条件不用再加括号**_

```
//如果您想操纵外部循环, 则需要使用标记语句
sum = 0
rowLoop: for row in 0..<8 {
  columnLoop: for column in 0..<8 {
    if row == column {
      continue rowLoop
    }
    sum += row * column
  }
}
```

```
for i in 1...count where i % 2 == 1
switch coordinates {
case let (x, y, z) where x == y && y == z:
```

```
while aLotOfAs.characters.count < 10
```

```
 Switch语句要求必须要有满足的情况,满足这个的前提下可以没有default；
 case必须要有代码，哪怕是break什么也不做;
 case特殊用法_(let)where条件判断
 fallthrough继续执行下面的语句
 break默认不需要,如果贯穿了也可提前跳出
 switch语句可以处理任何数据类型
```

* ##### _**swift常量在棧中，出了｛｝号就跳出了作用域**_

```
let firstName = "Matt"

 if firstName == "Matt" {
     let lastName = "Galloway"
 } else if firstName == "Ray" {
     let lastName = "Wenderlich"
 }
 let fullName = firstName + " " + lastName
```



