### 函数的三种角色
function fn(){}
+ 函数：能够调用的角色
+ 构造函数：new 构造对象的,fn.prototype 公共的属性或者方法挂在这个构造函数的原型下
+ Function的实例：new Function ->function(){}
+ 在函数的原型下有一个属性，constructor，这个属性指向构造函数，但是当前的constructor并不是100%准确的，它的指针仅仅只是一个指向构造函数的方向（一个参考），非常容易被修改
> 注意的是在对象赋值给构造函数原型的时候，constructor指向会被修改指向的是Object,所以手动修正constructor指向
### hasOwnProperty
+ 定义：查看某个属性是不是对象自身的
+ 返回一个布尔值，是自身的属性就是true，否则false
+ 用法：for in的时候回枚举原型，会把自定义的属性或者方法枚举出来；查看某个属性或者方法是否为对象自身的（面向对象中），即查看某个属性或方法是公有的还是私有的
+ 在for in的过程当中，如果不能确定构造函数的原型是否有自定义的属性或者方法，那么建议加一个if判断，判断枚举的属性都是自身的
### this
+ 1、window
    + 全局打印this
    + 函数+括号
    + 定时器
    + 匿名函数自执行
+ 2、事件触发的元素
    + 只要是事件函数内的this都指向事件触发的元素
+ 3、点前面的主（对象）
+ 4、实例
    + 构造函数下的this是实例（new fn）
    + 构造函数原型的this也是实例（实例调用）
        + Fn.prototype.say()   this为Fn.prototype
+ 5、箭头函数
    + 指向的是声明箭头函数的上下文this
    + 没有arguments，不能new
### call，apply，bind
+ 当一个函数创建的时候，其中有call，apply，bind
+ 这三个都是改变this指向的方法
#### call
+ 有若干个参数：
    + 第一个参数：修改this指向
    + 第二个参数以及之后：函数的参数
#### apply
+ 有2个参数
    + 第一个参数：修改this指向
    + 第二个参数：数组，数组里面放的是参数
#### bind（惰性函数，柯里化函数）
+ 有多个参数
    + 第一个参数：改变this指向
    + 第二个参数以及之后：函数的参数
+ 返回的是新函数，只有调用返回的函数才能执行函数内的代码
> *** 在使用它们修改this的时候，不要传null和undefined，因为传了也不认,还是走默认的window ***
