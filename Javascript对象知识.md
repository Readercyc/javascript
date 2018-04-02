# Javascript对象知识



---

## Javascript基本数据类型
- null
- undefined
- boolean
- 字符串
- 数字

除了上述的5种基本数据类型外，剩下的所有值都是对象，所以俗称js中万物皆对象

**需要了解基本数据类型可以去看我github里面的「类型，值，变量」**

## 对象的意义

1. 面向对象语言的出现，代替面向过程语言
    - 为了解决第一次软件危机
    - 拥有更好的可读性，可操作性，可维护性
    - 移植性优秀

2. 代替结构体
```c
strcut people{
    char name[10];
    int id;
    char sex;
}
function eat(){
    ...
}
function sleep(){
    ...
}
int main()
{
    strcut people zhangzixv;
    zhangzixv.name = "zhangzixv";
    zhangzixv.id ="2017";
    zhangzixv.sex = 'm';
}

```

```
class People{
    public:
        People(char name[],int id,char sex){
            this.name = name;
            this.id = id;
            this.sex = sex;
        }
    private:
        char name[10];
        int id;
        char sex;
}
int main(){
    People zhangzixv("zhangzixv",2017,'m');
}
```
3. 以此延伸出封装性，多态性，继承性等等一系列属性

## js中的对象

1. Object
2. Math对象
3. String对象
4. Function对象
5. Date对象
......

为什么Math，String这些东西也可以是对象呢？刚才不是说他们是基本类型吗？

注意区分**数值类型**和**数值对象类型**

后者仅仅只是自动将传入的参数以对象的形式存储而已

但其实他们拥有同样的方法，只是表达形式不同

js也有中的内置对象

比如

1. Date() 日期对象，可以得到一个日期值，并有相对应的函数可以处理值来得到需要的年/月/日/时/分/秒
2. Exp() 正则对象，用于一些字符串匹配
...

他们本质上都是对象，只是里面事先封装好了一些值和功能给予使用

## 对象里有什么?
```js
var obj = {
    x:1,
    getX:function(){
        console.log(this.x);
    }
}
```
1. 属性
2. 值
3. **原型** 

## 创建对象

1. 直接用表达式，赋值创建

```js
var empty = {}; // 空对象
var point = {
    x:1,
    y:1,
} // 有值的对象
var point = {
    x:x,
    y:y,
} // 用别的变量进行赋值

var obj = {
    "my name":"reader",
    "my-name":"reader",
    "for":"reader",
    //属性名含有空格，横线，关键词
}
//建议在最后一个对象后面也加,否则IE会报错
```


2. 使用new创建对象

例如
```
var obj = new Object();
// 创建一个空对象{}
var arr = new Array();
// 创建一个空数组
var date = new Date();
// 创建一个表示当前日期的Date对象
```

使用new创建对象是有条件的  
new 后面跟的是一个**构造函数**

构造函数

简单来说因为函数本身是一种对象，而函数本身可以被调用,所以就提出了一个方案

对函数对象使用new函数可以将这个函数作为一个原型，以此为基础创建一个新对象，而这个函数本身我们称之为构造函数

```

```











