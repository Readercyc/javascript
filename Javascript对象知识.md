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

3. 使用new创建对象

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

对函数对象使用new，可以将这个函数作为一个原型，以此为基础创建一个新对象，而这个函数本身我们称之为构造函数

```js
function foo(x,y){
    this.x = x;
    this.y = y;
    this.readXY = funtion(){
        alert(x + " " + y);
    }
}

var fun = new foo();
//利用foo为原型构造函数创建fun对象
```

构造函数的详细知识会在函数的章节讲解

2. 用Object.create() ES5标准
通过传入对象，以传入对象为原型创建新对象

```
    var o1 = Object.create({x:1，y:2});
```

可以通过传入`null`的方式创建一个非常**干净**的对象，什么都没有。


3. 原型

每个对象都有一个原型，原型本质也是一个对象，js中没有「类」的概念，如果要实现继承使用的原型的方法。

新对象会拥有其原型对象的所有属性和方法，以此来实现继承

和原型的相关的属性`prototype`和`__proto__`

`__proto`是任何一个只要拥有原型的对象都拥有的属性，通过访问该属性查看其原型

`prototype`是**构造函数**才会拥有的属性，访问它可以看到其构造函数和原型

```js
function Point(x,y){
    this.x = x;
    this.y = y;
    this.readXY = funtion(){
        alert(x + " " + y);
    }
}

var point = new Point();
//利用foo为原型构造函数创建fun对象
//但事实上这么做很蠢
```

为什么要这么设计？？js的对象继承怎么和别的面向对象的继承不一样？？

[js继承原理的设计][1]

isprototype
### 属性


#### 访问方法

```js
//可以用(.)访问
people.name
people.age
//也可以用中括号访问
people[name];
people[age];
//第二种方法用来访问名字中含有空格，横线，或者本身名字是数字，字符串等
people["name"];
people["age"];
people[1];
//也可以用来进行动态访问
for(var i = 0 ; i < 10 ; i++)
{
    console.log(people.["name"+i]);
    //访问name0，name1，name2......
}
```

#### 访问原则

```js

var obj = new Object();
//以Object为原型创建obj，当然也顺便继承了Object.prototype
obj.x //undefined，因为没有这个元素
obj.x = 5 //那我们就创建一个元素吧

再以obj为原型创建一个p
p = Object.create(obj);

p.x  //可以得到5

//如果访问本对象没有，那么顺着原型链往下查找直到找到相同的，到底还没找到，就返回undefined

p.x = 6；

p.x // 这样会得到6

//如果出现同名的看优先级，先找到就先输出

//小实战，不允许使用Object.create()，但要创建一个p对象，其原型为obj
```

#### 删除元素

语法：delete  属性名
delete obj.x  
需要注意的是，删除后再访问会返回undefined

但不是所有的属性都可以删除

#### 枚举元素

使用for/in 可以将对象中枚举属性为true的元素枚举出来，顺序不定
```
for(p in obj)
    console.log(p)
```

#### 属性的属性 -- 属性特性

每个属性在被创建时都会自带属性，我们称之为属性特性

```
value //值
writable attribute  //决定元素是否可写
configurable attribute //决定元素是否可配置
enumerable attribute //决定元素是否可以被枚举
```

#### get/set

![image_1ca5jd19aesl178c6fq1c501sii9.png-13.1kB][2]

#### 锁死对象

`Object.seal()`

`Object.freeze()`

`Object.preventExtensions()`


  [1]: http://www.ruanyifeng.com/blog/2011/06/designing_ideas_of_inheritance_mechanism_in_javascript.html
  [2]: http://static.zybuluo.com/reader-cyc/2tur2tb554eio4x5k23d2c83/image_1ca5jd19aesl178c6fq1c501sii9.png