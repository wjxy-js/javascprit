### var、let、const的区别
#### 原始值 vs 引用值
+ 原始值：存储在栈（stack）中的简单数据段，也就是说它们的值直接存储在变量访问的位置
+ 引用值：存储在堆（heap）中的对象，也就是说存储在变量处的值是一个指针（point），指向存储对象的内存处
#### var
+ 当通过var创建一个变量的时候，会进行预解析（会变量提升），因为var会预解析，所以变量会当做属性存到全局的活动变量对象下（window下）
+ var是不会主动存储每次循环的值
+ 不支持块级作用域（不被块级作用域所限制，定义一个变量，在块级作用域之外是可以拿到这个变量的，函数也是，不过函数是就近原则）
#### let 
+ 当通过let创建一个变量的时候，不会进行预解析（不会变量提升），不会在window下存储一个属性，在定义变量之前访问这个变量，之前访问的空间叫暂存死区
+ let会把每次循环的值存储起来（let具有闭包的特性）
+ 支持块级作用域（被块级作用域所限制，定义一个变量，在块级作用域之外是拿不到的）
+ 不能声明同名的变量、函数、参数
#### const:常量（不可变的量）
+ 当声明一个变量不允许改变的时候，就使用const来定义
+ 不能声明同名的变量
> 注意：const赋值的数据，它只会监控这个数据的地址
#### 块：{}
+ 在块套块中，子块有函数，如果在父块或者父块的上方访问这个函数，那么都是undefined，如果在子块的下方访问这个函数，就能找到这个函数
> 函数是不被块级作用域所限制的
```
    console.log(a);  //undefined  块级作用域中，var一个变量，在上面获取到的是undefined,var会进行预解析，会把a这个变量放在window下，所以在块级作用域的上面是可以拿到a这个变量
    {
        var a = 10;
    }
    console.log(a);  //10  在块级作用域的下面可以拿到a这个变量的值


    console.log(a);  //报错 块级作用域中，let一个变量，在上面是拿不到a这个变量的，let不会进行预解析，它不会把a这个变量放在window下，所以在块级作用域的上面是拿不到a这个变量
    {
        let a = 10;
    }
    console.log(a);  //报错   同样在下面也是拿不到的


    {
        let a = 10;
        console.log(a);  //let只能在块级作用域中拿到a这个变量，所以let是受块级作用域的限制，而var是不受块级作用域的限制
        console.log(fn);  //undefined  同var的性质，在块级作用域上面拿到的是undefined
        {
            function fn(){console.log(1)}
        }
        console.log(fn);  //function fn(){console.log(1)}  在下面拿到的是函数,并且函数是就近原则
    }
    function fn(){}

    let ary = [];
    for(var i=0;i<4;i++);{
        ary.push(i+1);
    }
    console.log(ary)  //5   for有一个分号，说明for循环已经执行完成，所以在块级作用域中拿到的i是4
```
```
    <button>1</button>
    <button>2</button>
    <button>3</button>
    <button>4</button>
    //let可以存储循环的索引
    let btn = document.querySelectorAll('button');
    for(let i=0;i<btn.length;i++){
        btn[i].onclick = function(){
            alert(i);
        }
    }
```
### 单例模式
+ 单例：单独的实例    实例：描述具体的一个事务（具体的）      构造函数：抽象一个类的封装过程（相当于一个老师）
+ 原始值：字符串，数字，布尔值......
+ 引用类型：里面放着很多的原始值和引用值，它是一个集合（一个对象就是一个实例，一个对象就是一个单例）
+ 缺点：一个对象只能描述一个具体的事务，不能批量生产实例，增加代码的冗余
#### 高级单例模式
+ 目的就是为了让当前这个实例功能更加强大，还可以隐藏或者暴露细节信息
+ 缺点：不能批量生产实例
```
    (function(){
        function sum(){

        }
        return {

        }
    })()
```
#### 高级单例模式需要知道哪些
+ 为什么要用高级单例模式？
    + 1、让当前这个实例更加强大，还可以隐藏或者暴露内部细节信息，解决了命名冲突的问题
    + 2、高级单例模式如何写
        ```
            (function(){
                return {

                }
            })()
        ```
        最后让一个变量去收这个功能强大的对象
+ 解决命名冲突的问题：
    + 1、封闭空间（把变量或者函数放到函数中）
        ```
            let a = 10;
            (function(){
                let a = 20;
            })()
        ```
    + 2、命名空间
        ```
            //let name = 10;
            obj.name = 10;
            //let name = 20;
            obj2.name = 20;
        ```
*** 面向对象都是用对象来操作的 ***
#### 工厂模式
+ 工厂模式为了批量生产实例
+ 函数的目的就是为了复用
```
    function fn(name,age){
        let obj = {};  //原材料
        //加工
        obj.name=name;
        obj.age=age;
        //出厂
        return obj;
    }
    let obj = fn('珠峰',10);
    console.log(obj);
```
### 面向对象思想（核心：谁来做这件事）
+ 面向对象是一个计算机发展到一定阶段后的产物，面向对象是一种对现实世界理解和抽象的方法
+ JS是一个基于面向对象思维构造出来的，基于对象的编程语言
+ 抽象：抽出像的部分（把相同的代码抽离出来）
+ 类（class）
+ 用面向对象编程的原因：面向对象都是通过对象来编程，扩展性更强，能够做到高内聚（功能比较完善）低耦合（模块化开发）
+ 面向对象：
    将具有相同特征特性的代码抽离出来归为一类，然后把描述这个类的细节特性（属性、方法）挂在这个类的原型下的一种编程方式
+ 面向对象特征
    + 封装、继承、多态
        + 封装就是归类的过程
+ 构造函数（类）
    + 首字母必须大写
    + 构造函数就是用new调用的函数
    + new是函数一元运算符，专门运算函数的，使用new之后会调用函数，就算不加()也会调用执行（用new运算函数，函数可加可不加括号）
    + 使用new之后，this变成了实例，实例就是一个对象（空白对象）
    + 使用new之后，函数默认返回值为实例化对象，就不是undefined，如果return后面有值，为简单类型（原始类型），返回结果还是实例，如果return后面的值为引用类型，返回的结果就是return后面的引用类型
    + 创建对象的方式
        + {}
        + new Object
        + new 函数
+ 实例（更加具体）
```
    function Person(name,age,sex){  //归类  构造函数（构造对象的函数）
        let obj = {};
        obj.name = name;
        obj.age = age;
        obj.sex = sex;
        return obj;
    }
    let p1 = new Person('小花',10,'女');  //p1是实例，在这里new Person
    console.log(p1);


    //直接使用this，返回的结果中会加当前函数的类名（函数名）
    function Person(name,age,sex){  //归类  构造函数（构造对象的函数）
        // let obj = {};   //this  {}
        this.name = name;
        this.age = age;
        this.sex = sex;
        // this.say = function(){
        //     alert('我叫'+this.name);
        // }
    }
    Person.prototype.say = function(){
        alert('我叫'+this.name);
    }
    let p1 = new Person('小花',10,'女');
    let p2 = new Person('小红',11,'女');
    // console.log(p1);
    // console.log(p1.say());
    console.log(p1.say == p2.say);  //true  此时在构造函数的原型上有一个say的属性名，如果是在原型上，那么结果它们是相等的，所以是true
```
### 面向过程
+ 思考如何实现
### 原型
+ 在js中，所有的class（类）都是函数模拟出来的，当声明一个函数的时候，这个函数自身有一些属性或方法（天生自带的），其中有一个属性叫做prototype，它的值为对象
+ prototype就叫原型，也就是说只有函数身上才有原型
+ Object.prototype.__proto__
+ prototype下的方法或者属性只能通过两种方式使用：
    + 1、函数原型下的属性或者方法只给它（构造函数）的实例化对象使用
    + 2、直接使用fn.prototype.a
+ 原型是为了优化性能
### 原型链
+ __proto__   实例化对象下都有__proto__属性，这个属性全等于实例的构造函数的原型（实例化对象下的原型链与构造函数下的原型是全等的，使用同一个原型链下的属性或同一个原型下的属性，结果是true）
+ 如果某个原型下没有想要的属性或者方法，那么还会通过这个原型下的原型链继续查找，知道找到Object.prototype为止，因为Object.prototype.__proto__为null
+ 实例化对象下的属性会通过原型链（__proto__）找到构造函数的原型（prototype），会去取构造函数原型上的属性，因为实例化对象下的原型链和构造函数的原型下都有同一个属性，所以实例化一个函数之后，两个实例化对象下的属性是相等的（返回结果是true）
+ 调取一个对象的属性时，会先从对象本身查找，如果对象本身没有，就会去实例化对象的原型链上查找，原型链上没有，就会去构造函数的原型上去查找，如果查找不到，最后结果就是undefined

*** 实例的constructor就是Object ***


*** 如何查找实例下的某个属性或者方法 ***
1、先找实例下的原型链（__proto__）
2、在通过原型链找到构造函数的原型（prototype）
3、再通过构造函数的原型找到原型下的原型链
4、原型下的原型链没有的话，继续往下找
5、继续找到构造函数的原型，原型下有的话，结果就有，在这里已经没有原型链了，就不会再往下找了

*** 实例有原型链，函数有原型，原型又是一个对象，对象它就是实例，实例又有原型链，找到构造函数的原型，Object.prototype.__proto__ = null ***
### 封闭空间与闭包的区别
封闭空间不是闭包，但是闭包有封闭空间的功能
### 内置类（浏览器自带的）
    所有的类型都是构造函数构造出来的
