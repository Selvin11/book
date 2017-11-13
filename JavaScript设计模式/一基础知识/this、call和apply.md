## this、call和apply

1. [this](#1)
2. [call和apply](#2)



#### <a name="#1">1. this</a>

  JavaScript 的 this **总是指向一个对象**，而具体指向哪个对象是在运行时基于函数的执行环境动态绑定的，而非函数被声明时的环境。

  * this的指向：作为对象方法／普通函数／构造器／call或apply调用

    **如果调用者函数，被某一个对象所拥有，那么该函数在调用时，内部的this指向该对象。如果函数独立调用，那么该函数内部的this，则指向undefined**。但是在非严格模式中，当this指向undefined时，它会被自动指向全局对象。

  * this的丢失：this所属的函数没有被一个对象（非全局对象）所拥有，指向undefined

#### <a name="#2">2. call和apply</a>

  * apply：apply 接受两个参数，第一个参数指定了函数体内 this 对象的指向，第二个参数为一个带下标的集合，这个集合可以为数组，也可以为类数组

  * call：call 传入的参数数量不固定，跟 apply 相同的是，第一个参数也是代表函数体内的 this 指向，从第二个参数开始往后，每个参数被依次传入函数

* call和apply的用途：

  1. 改变this指向

  2. Function.prototype.bind 

  ```javascript
  // 模拟bind实现
  Function.prototype.bind = function(context) {
    var self = this
    return function () {
      return self.apply(context, arguments)
    }
  }
  ```

  3. 借用其它对象的方法
  
  函数的参数列表arguments是一个类数组对象，如需向其添加元素，需要借用Array对象的push方法
  
  ```javascript
  (function(){
    Array.prototype.push.call(arguments,3)
    console.log(arguments) // 输出[1,2,3]
  })(1,2)
  ```
