* ##### swift变量在声明的时候必须有值, 一般可以不写类型, 他自己可以推断是什么变量类型,当你想表达一个单字符类型的时候必须带上变量类型

```
let characterA: Character = "a"
let stringDog: String = "Dog"

var integer: Int = 100
integer = Int(decimal)
let actuallyDouble3 = 3 as Double
```

##### _**swift循环有标记, 循环或者条件选择后面可以再加个条件; 判断条件不用再加括号，dowhile 现在变成repeat**_

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

降序stride\(from: 10, to/through: 22, by: 4\)like 10..&lt;22/10...22

```
//for index in stride(from: 10, to: 22, by: 4)不包括22，下面的包括9
for index in stride(from: 10, through: 9, by: -0.1) {
  print(index)
}
```

* 可选值类型, swift新类型代表一个值可能为空



