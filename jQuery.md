## 选择器
*  子代选择器 ==>$("ul>li")
*  后代选择器 ==>$("ul li")
*  隐式迭代 
   *  给匹配到的所有元素都进行揗环遍历 执行后面相就的方法
##  筛选选择器
  * :first 获取第一个 元素 
  * :last 获取最后一个元素
  * :eq(index) 获取得到的集合中的第几个元素
  * :odd 获取到集合中索引号为奇数的元素
  * :even 获取到索引号为偶数的元素
### 筛选器方法
* parent()  查找父级
* children(selector)    查找最近一级(亲儿子)
* find(selector)    后代选择器
* siblings(selector)    查找兄弟节点,不包括自己本身
* nextALL([expr])   查找当前元素之后的所有的同辈元素
* prevtALL([expr])  查找当前元素之前 的所有的同辈元素
* hasClass(class)   检查当前的元素是否含有某个特定的类,如有,**则返回true**
* eq(index)     从 index 开始

* 得到当前元素的索引号 $(this).index();


## jQuery 和 DOM 对像的互转
* jQuery 获取到的对象 都会被包装成jQuery 对象
  * $(".box").get(0)  这样可以在jQuery对象里获取到第1个DOM对象 而完成转换;
  * **$(".box")[0]** 同上
  * jQuery 对象不能使用DOM原生的一些属性 要使用必须得先转换

## jQuery 样式操作
* 参数只写属性名,则返回属性的值.是一个string
* 修改单个属性样式 属性名必须要加引号 
  * $(this).css("width","220px");

* 参数可以是对象形式,设置多组样式 属性名和属性值用 冒号 隔开  属性名不用加括号 如果是复合属性则必须采用驼峰命名法 如backgroundColor:"red", 属性值 如果不是数字也必须要加上引号<br>
   "900px" 这里如果要加上px这必须加上引号因为它是string了
  
  * $(this).css({
      color:red,
      width:"900px",  
      height:800,      
   })
* 添加 transition 属性:
  *  transition : "all 10s",<br>
  transform : "rotate(360deg) translate(40px)",

* 类添加/删除/切换
  * addClass("current") 添加类
  * removeClass("current") 删除类
  * toggleClas("current") 切换类