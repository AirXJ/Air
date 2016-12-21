- #if的使用

```
#if 的后面接的是表达式 (求表达式的值为真则编译code部分否则跳过)

 code ...

#endif
```

- #if 的表达式是在编译是求值的 

```
#ifdef的使用
#ifdef  GREAT   只要GREAT被#defined定义过则编译code部分
code ...
#endif  
```


- #if defined的使用
```
#if defined(x)   (首先处理defined运算符， defiend运算符 一般用作表达式中的一部分，如果x这个宏有定义把 defined(x) 替换为1 否则替换为0,替换后相当于#if 1或 #if 0 ，到这应该能明白了吧.不说了)
code ...
#endif 
```