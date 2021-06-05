# 给元素增加属性
  *  ele.setAttribute('class','classname'); 
    *  这里面的第一个Class是增加一个类名 ,同样也可以增加ID.
    *  第二值 classname 才是需要增加的类名.
  * el是对元素的对象引用
  *  //添加一个或多个类名
  *  el.classList.add("class1");
  *  el.classList.add("class1","class2"...);
  *  
  *  //删除一个或多个类名
  *  el.classList.remove("class1");
  *  el.classList.remove("class1","class2"...);
  *  
  *  //切换元素类名
  *  el.classList.toggle("classname")
  *  
  *  //判断元素是否含有某个类名，如果有返回true，否则返回false
  *  el.classList.contains("classname")
# js 中的回调函数 
*  一. 回调函数的作用

      js代码会至上而下一条线执行下去，但是有时候我们需要等到一个操作结束之后再进行下一个操作，这时候就需要用到回调函数。

      二. 回调函数的解释

      因为函数实际上是一种对象，它可以存储在变量中，通过参数传递给另一个函数，在函数内部创建，从函数中返回结果值”，因为函数是内置对象，我们可以将它作为参数传递给另一个函数，到函数中执行，甚至执行后将它返回，它一直被“专业的程序员”看作是一种难懂的技术。

      回调函数的英文解释为：

      A callback is a function that is passed as an argument to another function and is executed after its parent function has completed.

      翻译过来就是：回调函数是一个作为变量传递给另外一个函数的函数，它在主体函数执行完之后执行。

      function A有一个参数function B，function B会在function A执行完成之后被调用执行。

      三. 回调函数的使用方法

      代码如下：

      function a(callbackFunction){
        alert("这是parent函数a");
        var m =1;
        var n=3;
        return callbackFunction(m,n);
      }
      function b(m,n){
        alert("这是回调函数B");
        return m+n;
      }
      $(function(){
        var result = a(b);
        alert("result = "+ result);
      });

      执行顺序为：

      这是parent函数a

      这是回调函数B

      result = 4

      函数首先执行了主题函数a，之后调用了回调函数b，最后返回函数a的返回值。
# js中函数的调用需要事件来触发
