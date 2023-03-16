---
title: C#
date: 2020-11-05 15:31:49
tags: 学无止境
---

# C #

## 关键字 ##

override(重写):与父类函数特征（函数名、参数类型与个数）相同

overload(重载):同一个类中的方法名相同，但函数特征不同，可省略

new(overwrite覆写):与父类中同名的方法，也称为覆盖，覆盖不会改变父类方法的功能。

## delegate委托 ##

[^注释1]
**委托，可以将方法当作参数使用**
可以增加方法的复用性，帮助程序解耦

## Struct声明 VS Class声明 ##

Class 声明一个引用类型
Struct 声明一个值类型

Class 实体的赋值，是把地址赋值给了其他对象（任意对象被修改就改变了该地址下的内容）
Struct 实体的赋值，只是把实际值拷贝了一份放到新的地址下

[^注释2]

## Lambda表达式 ##

方法的简化写法,可以直接用于 list,array 等集合中

```C
//定义一个lambda对象
//有返回值的用Func<>
Func<string> fnc2 = () =>  "你好";  //无参数

Func<int, int, bool> fnc1 = (x, y) => x == y;  //有两个参数，最后一个是返回值类型

//无返回值的用Action
Action callback = () =>  Console.WriteLine();  //无参数

Action<string> callback = hha =>   //有一个参数
{
Console.WriteLine(hha);
Console.ReadKey();
};

```

## 参考文件 ##

[^注释1]： [委托，事件和Lambda表达式](https://www.cnblogs.com/zcqiand/p/13656161.html)
[^注释2]： [C#中 struct 和 class 的区别详解](https://www.cnblogs.com/jjg0519/p/10341010.html)
