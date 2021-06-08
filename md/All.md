# 节点操作
* 删除一个节点只需要拿到这个节点 调用自身的方法 ele.remove();即可自杀,
  * 也可以拿到自己的父亲调用方法删除   ele.parentNode.removeChild(ele);自杀.
* 添加节点 
  * 父节点.apendChild(子节点) 在最后添加节点
  * 父节点.insertBefore(新节点,参考节点)   在参考节点之前添加新节点
* 通过JS 来设置节点CSS属性值 
  * element.setAttribute("style","name1:value1;name2:value2");
  * element.style.setProperty("name","value");   只能设置一个style属性 
  * 使用element.style.cssText = "name1:value1;name2:value2";可以添加一个或多个style样式
          最终使用形式：element.style.cssText  +=  ";name1:value1;name2:value2";
  * 1.使用element.style.cssText设置style样式，会把原有的style中的样式覆盖掉。
    * 解决方法：element.style.cssText  +=  ";name1:value1;name2:value2";加上前置分号“；”,在IE高版本和Chrome等浏览器中会自动去重。

* 通过自定义属性拿到节点
  * document.querySelectorAll("[target]");
    * 可以拿到元素有target属性的所有节点
  * document.querySelectorAll("[target = 'jxls']");
    * 可以通过查找所有节点有属性为target的节点 ,再查找其属性值 为 jxls的所有节点,返回的值还是数组; 
# flex:对齐的注意点
* 副轴对齐需要确定高度.是在当前级操作.
  * 文字纵轴对齐是在其**父级**开通 **line-height**

# 文本框输入事件
* onchange
在用于文本框输入框时,有一个明显的不足. 事件不会随着文字的输入而触发,而是等到文本框失去焦点(onblur)时才会触发. 也就是没有即时性! 且必须值变化才触发

* onblur
与onchange基本相同，唯一的区别是 不管值是否变化，都触发

* onkeyup
只要输入框内容发生变化即可触发，但是无法检测复制粘贴

* oninput
只要输入框内容发生变化即可触发

# 九宫格 
  * 计算列号和行号.
    * //   除得行号 取余得列号  因为余怎么都不能大过 被除数;
  
# 滚动高度
  * windows.pageYoffset
  
# 取消冒泡
  * event.cancelBubble = true;
  * 要停在哪一层就在哪一层用

# JS修改元素属性后 如何清除
  *  ele.removeAttribute("style");
     * 因为在JS中修改元素的属性都是添加 到行内Style 中的.
     * 所以想到的就是先清除这个style 然后再通过添加类名的方法来设置另外的属性.

# 元素随着窗口改变而改变大小
  *     var timer = null;
        ww = window.innerWidth;
        window.onresize = function (eve) {
            timer = setTimeout(function () {
                noww = window.innerWidth;
                sb = noww / ww;
                if (sb >= 1.5) {
                    sb = 1.5;
                }
                if (sb <= 0.5) {
                    sb = 0.5;
                } // console.log(sb); 
                for (var i = 0; i < imgs.length; i++) {
                    imgs[i].style.transition = "all 200";
                    imgs[i].style.transform = "scale(" + sb + ")";

                }
            }, 200)
        };


# Vue
## v-for
* v-for ="(item,index) in arrs"
  * 这里面第一个参数是vlaue ,第二个参数是下标key.
  * 遍历对象也是一样的,第一个是value ,第二个是key