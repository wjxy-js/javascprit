### 面向对象
+ 1、把所有的变量放到类中，把变量变成属性
+ 2、把函数抽出来，挂到构造函数的原型上
### 面向对象特征
+ 封装、继承、多态
+ 继承：
    + 子类具有父类的一部分特征（这部分相同的特征是从父类继承下来的），自己还有自己的特征
    + 继承的写法可以让子类的代码量减少很多，从而达到高内聚，低耦合的目的，减少了开发成本
    + 继承的方式很多：
        + 类式继承（call继承）（构造继承）
        + 原型继承
        + 寄生式继承
        + 拷贝继承
        + 对象继承
        + class类继承
    + 继承最后的结果是能够继承父类的属性和方法
    + 继承属性
        + 调用父类，通过call把this变为子类的实例即可 
        *** 2个引用类型的赋值就是赋值地址，原始类型的赋值就是普通赋值，其实赋值引用类型的目的是B拿到A下面的属性，如果是一个数组，如果数组中还包有引用类型，那么赋值还是赋址 ***
        如何才能避免赋址？
            1、需要2个不同地址
            2、B地址下拥有A地址下的原始类型的数据即可（原始类型的赋值）
    + 方法继承
        + 通过浅拷贝，把父类原型是上的方法或属性都赋值给子类的原型（拷贝继承）
        + Object.assign  浅拷贝（Object.assign(子类.prototype,父类.prototype)）
        + Object.assign(obj2,obj1,obj0)   从右往左浅拷贝对象的属性，可以放若干对象，最后改变的是obj2（改变的是最左边），obj1是不会被修改的（中间的不会被修改），越往右边层级越高
        + 深度克隆
            + 1、判断传进来的参数的类型是否是对象类型以及判断传进来的参数是否存在
            + 2、判断传进来的值到底是数组还是对象
            + 3、for in循环传进来的值
            + 4、如果碰到了引用类型就继续循环，原始类型才赋值
            + 5、递归
    + class类继承
        + 在继承的constructor中，如果要使用this，一定要写super，super中放父类的参数，super的上方是拿不到this的
        + 通过class中的static，可以创建静态方法，类中的静态方法（static定义的方法），只有类才能调用，实例是调用不到的，就算是继承，也只能是继承的子类去调用，子类的实例是调用不到的
    + 寄生式继承：Objcet.create()
### 函数Function
+ function fn(){} -> new Function
+ Function是个内置类，它也是个函数
+ Function.prototype给所有的小写function使用也包括它自己
+ Function.prototype是个函数，不是对象，而且这个函数还不是new Function构造出来的
+ fn:{
    __proto__:Function.prototype,
    prototype:{
        constructor:fn
    }
    执行栈:{
        console.log(1);
    }
}
fn() -> 执行栈
new fn() -> prototype
fn.a -> Function.prototype