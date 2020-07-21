---
title: RegExp正则表达式
date: 2020-05-22 15:24:49
tags: 学无止境
---

## 1.定义
使用RegExp对象，或者直接在一对 '/ /'中
```javascript
var a = new RegExp("\\d{5}","g");  //第一个参数：正则表达式主体部分；第二个参数：修饰符（选填）
								   //注意：转义字符'\'->'\\'.例如：'\d'->'\\d'
var a = /\d{5}/g;             	   //与第一种定义方式等价
```


## 2.语法

####  1.直接量

|      字符      |                      匹配                      |
| :------------: | :--------------------------------------------: |
| 字母和数字字符 |                      自身                      |
|       \o       |        NUL字符（\u0000）Unicode编码方式        |
|       \t       |                制表符（\u0009）                |
|       \n       |                换行符（\u000A）                |
|       \v       |              垂直制表符（\u000B）              |
|       \f       |                     换页符                     |
|       \r       |                     回车符                     |
|      \xnn      |    由16进制数nn指定的拉丁字符；例：\x0A=\n     |
|     \uxxxx     | 由16进制数xxxx指定的Unicode字符；例：\u000A=\n |
|      \cX       |             控制字符^X；例：\cJ=\n             |



#### 2.具有特殊含义的符号

> ^  $  .  *  +  ?  =  !  :  |  \  /  ( )  [ ]  { }

如果想使用这类字符的直接量，需要在前面加上，转义字符 \'\\\' ；否则作为特殊字符使用。没有特殊含义的字符可直接使用。



#### 3.字符类

|  字符  |          匹配          |
| :----: | :--------------------: |
| [...]  |     括号内任意字符     |
| [^...] |  非括号内大的任意字符  |
|   .    | 除换行符和其他Unicode终止符之外的任意字符 |
|   \w   | ASCII码，=[a-zA-Z0-9]  |
|   \W   | 非ASCII码,=[ ^a-zA-Z0-9] |
|   \s   | 任意的Unicode空白符 |
|   \S   | 任意的Unicode非空白符 |
|   \d   | ASCII码数字，=[0-9] |
|   \D   | 非ASCII码数字，=[ ^0-9] |
|  [\b]  | 退格直接量 |

[\b]无法和其他字符类连用；例：[\d\s]。必须写作[\b]才表示退格，[\b\d]是错误的。



#### 4.重复语法

|  字符  |          匹配          |
| :----: | :--------------------: |
| {n,m}  |     重复至少n次，至多m次     |
| {n,} |  重复至少n次  |
|  {n}  | 重复n次 |
|   ?   | 重复0或1次，={0，1}(及该项可选) |
|   +   | 重复至少一次，={1，} |
|   *   | 重复至少0次，={0,} |

以上字符都是尽可能多的匹配（贪婪的匹配），如果要实现非贪婪的匹配，可以在语句后添加’？‘

```javascript
var a = /\d{3}|[a-z]{4}/;   //匹配前三个数字，后四个是小写字母

var kat="12345678".match(/[0-9]{1,6}?/);    //=>[ '1', index: 0, input: '12345678', groups: undefined ]
var kat="12345678".match(/[0-9]{1,6}/);     //=>[ '123456', index: 0, input: '12345678', groups: undefined ]
```

正则表达式的匹配，总是会寻找字符串中第一个可能匹配的位置，所以下面的两种写法，查询到的结果是一样的

```javascript
var kat="aaab".match(/a+?b/);     //=>[ 'aaab', index: 0, input: 'aaab', groups: undefined ]
var kat="aaab".match(/a+b/);      //=>[ 'aaab', index: 0, input: 'aaab', groups: undefined ]
```



#### 5.选择，分组，引用

|  字符   | 含义                                                         |
| :-----: | :----------------------------------------------------------- |
|   \|    | 选择                                                         |
|  (...)  | 组合，该单元格可以用过“*”，“+”，“？”，“\|”等符号来修饰，并且会记住该条件所匹配的字符串，以便后续调用；可以使用\n引用 |
| (?:...) | 只组合，不会记忆字符串；无法用\n引用                         |
|   \n    | (n是数字)，和第n个分组第一次匹配的字符串相匹配，索引从左到右 |

```javascript
var txt3='\"fakacnfma\''.match(/(['"])[^'"]*\1/);   //=>null

var txt3='\"fakacnfma\''.match(/(['"])[^'"]*['"]/);   
//=>[  `"fakacnfma'`,
//      '"',
//      index: 0,
//      input: `"fakacnfma'`,
//      groups: undefined
//  ]
```

正则表达式不允许在“ ”中有‘ ’，反之亦然。如下实例，匹配到的是里面的‘ ’，而非外面的“ ”

```javascript
var txt3='\"\'fakacnfma\'\"'.match(/(['"])[^'"]*\1/);
//=>  [  "'fakacnfma'",    
//       "'",
//       index: 1,
//       input: `"'fakacnfma'"`,
//       groups: undefined
//     ]
```

不允许在字符类中使用\n的引用。如下实例是错误的:

```javascript
var d = /(['"])[^\1]*\1/;
```



#### 6.指定匹配位置

|  字符  | 含义                                                         |
| :----: | ------------------------------------------------------------ |
|   ^    | 字符串的开头，在多行检索中匹配，每行的开头                   |
|   $    | 字符串的结尾，在多行检索中匹配，每行的结尾                   |
|   \b   | 匹配单词边界 => 位于\w和\W之间的位置（*[\b]匹配退格符）      |
|   \B   | 匹配非单词边界的位置                                         |
| (?=p)  | 零宽正向先行断言 =>接下来的字符都和p匹配，但p不会出现在查询结果中 |
| (?!=p) | 零宽负向先行断言 =>接下来的字符不和p匹配                     |

```javascript
var c=/^JavaScript$/;      //纯JavaScript字符串

var txt5='javascript JavaScript: Is A LANGUAGE'.match(/[Jj]ava([Ss]cript)?(?=\:)/);  //先行正向断言,javascript后须带有‘：’，但‘：’不会被匹配到结果中
//=>[
//     'JavaScript',
//     'Script',
//     index: 0,
//     input: 'JavaScript: Is A LANGUAGE',
//     groups: undefined
//   ]
```



#### 7.修饰符

| 字符 | 含义                                       |
| :--: | ------------------------------------------ |
|  i   | 不区分大小写                               |
|  g   | 全局匹配，找出所以匹配的项，输入一个数组中 |
|  m   | 多行匹配模式，主要针对‘^’和'$'             |

```javascript
var txt2="java12das45".match(/[a-z]+(\d+)/g);  //=>[ 'java12', 'das45' ]
var txt2="java12das45".match(/[a-z]+(\d+)/);   //=>[ 'java12', '12', index: 0, input: 'java12das45', groups: undefined ]
```



## 3.可使用匹配模式的String方法

#### 1.search

查询` string.search(x)`返回匹配字串的第一个字符的位置。该方法不支持全局检索，会忽略修饰符g，及无法返回数组

如果找不到匹配的字串会返回-1

```javascript
var txt2="132java12das45".search(/[a-z]+(\d+)/g);  //=>3
```



#### 2.replace

执行检索与替换操作`string.replace(x,y)第一个参数可以是 正则表达式 或 字符串，第二个参数可以是 进行替换的字符串 或 函数`

```javascript
var txt5='javascript  javaScript: Is A LANGUAGE'.replace(/javascript/ig,"JavaScript"); //=>JavaScript JavaScript: Is A LANGUAGE

```

在replace中，第二个参数可以是正则表达式‘(’，‘)’中匹配的内容，使用‘$’，。具体用法如下：

```javascript
var quote = /"([^"]*)"/g;
var txt = '"fdajfoa"ckajc"fdadasd"231"da34fav"'.replace(quote,"“$1”");
//=> “fdajfoa”ckajc“fdadasd”231“da34fav”  将所有的英文的 ""，替换成中文的 “”
```



#### 3.match

`match(x)`返回一个数组

match返回数组的三种情况

```javascript
//没有修饰词g,没有括号
var kat = "aaab".match(/a+b/);      //=>[ 'aaab', index: 0, input: 'aaab', groups: undefined ]

//有修饰词g有括号
var kat = 'fdajfoackajcfdadasd231da34fav'.match(/f(d)a/g)    //=>[ 'fda', 'fda' ]

//没有g有括号
var kat = 'fdajfoackajcfdadasd231da34fav'.match(/f(d)a/)    //a[n],存放的是$n的内容
//=>[
//     'fda',
//     'd',
//     index: 0,
//     input: 'fdajfoackajcfdadasd231da34fav',
//     groups: undefined
//   ]
```



#### 4.split

`split(x)`将一个字符串拆分成数组，分隔符为split的参数

```javascript
var kat = "1, 2, 3, 4, 5".split(/\s*,\s*/);  //=>[1,2,3,4,5]   允许两边留任意多的空格符
```



## 4.RegExp对象

```javascript
var a= new RegExp("f(d)a","g");
```

#### 1.属性

|    属性    | 含义                                                         |
| :--------: | ------------------------------------------------------------ |
|   source   | 可读字符串，包含正则表达式文本                               |
|   globa    | 布尔值，是否带修饰符g                                        |
| ignoreCase | 布尔值，是否带修饰符i                                        |
| multiline  | 布尔值，是否带修饰符m                                        |
| lastIndex  | 可读写整数，读取的最后字符的下一位(对新字串进行检索，必须将lastIndex置0，否则会出错) |

#### 2.方法

`RegExp.exce()对指定的字符串执行一个正则表达式`，类似于`string.match()`,但是g修饰符对他不起作用

```javascript
var a= new RegExp("f(d)a","g");
a.exec('fdajfoackajcfdadasd231da34fav')  
//=>[
//     'fda',
//     'd',
//     index: 0,
//     input: 'fdajfoackajcfdadasd231da34fav',
//     groups: undefined
//   ]
```

`RegExp.test()只返回true/false `

`test()和exce()方法，都会修改lastIndex的值`当最后一次检索失败时，要手动将`lastIndex`的值置0，否则下一次检索将不会从字符串的起始位置开始。



## 参考代码

``` javascript
var b= /[a-z]+(\d+)/g;     //前面是小写字母，后面是数字
var c=/^JavaScript$/;      //纯JavaScript字符串
var d=/Java(?!Script)([A-Z]\w*)/;      //Java后面不是" Script",而是以大写字母开头的字符串
var e=/[Jj]ava([Ss]cript)?(?=\:)/;    //先行正向断言 
var g=/(\w+)\:\/\/([\w.]+)\/(\S*)/;    //解析一个url 
console.log('This Blog http://ymmltp.github.com/test.html');
//=>[
//     'http://ymmltp.github.com/test.html',
//     'http',
//     'ymmltp.github.com',
//     'test.html',
//    index: 10,
//     input: 'This Blog http://ymmltp.github.com/test.html',
//     groups: undefined
//   ]
```
