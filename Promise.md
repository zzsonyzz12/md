[toc]
## Promise 封装AJAX

 ```
   function senAjax(url){
        return new Promise((resolve,reject)=>{
            const xhr = new XMLHttpRequest();
            xhr.open("GET",url);
            xhr.send();
            xhr.onreadystatechange = function(){
                //readyState 4 是表示 所有都发送成功
                if(xhr.readyState === 4 ){
                    if(xhr.status>=200 && xhr.status<300){
                        //xhr.response 响应体
                        resolve(xhr.response);
                    }else {
                        reject(xhr.status);
                    }
                }
            }
            
        })
    }
 ```
## Promise --> [PromiseResult]
> 实例对象中的一个属性 保存着对象 (成功/失败) 的结果,它的值只能用resolve/reject 两个函数来修改
```
    let p = new Promise((resolve,reject) =>{
        // 这个data就保存在 PromiseReslut中
        resolve("data");
    })
    p.then((value)=>{
            // 这里的value 就是 PromiseReslut 中保存的值 
            console.log(value); 
            
        }, reason => {
            console.log(reason);
            
        })
```
## Promise --> Promise.prototype.catch
>catch 指定失败时的回调函数 链式时可以最后使用,来处理前面的错误.
```
    let p = new Promise((resolve, reject)=>{
        reject("catch的用法");
    });
    p.catch(reason =>{
        //catch 是失败时调用函数 它会去捕获失败事件.然后回调这个函数
        console.log(reason);        
    })
```
## Promise --> Promise.resolve(value) / Promise.reject(value)
> Promise.resolve(value),它返回的是一个(成功/失败)Promise对象,主要用来把非Promise 封装成Promise对象.
> value: 如果传入的参数 value 为非Promise 类型的对象,则都返回成功的Promise对象
> value: 如果传入的参数为 Promise 对象,则参数里的Promise 结果决定外层Promise 的结果 .
> Promise.reject(value) 它则返回一个失败的Promise 对象,无论value是任何值.
## Promise --> Promise.all([]);
> Promise.all(arr).它的参数一般为一个数组,且数组中都是Promise对象.
> 返回值: 是一个新的Promise对象, 只有数组中所有promise对象成功,它才是成功,只要有一个失败,则直接失败.
> 新Promise 值 ,如果所有的都成功,则其值为数组中第一个的返回值 .如果失败,则其值为第一个失败Promise对象的值 .
## Promise --> Promise.race([]);
> Promise.race(arr) 它也是接受一个Promise 数组 且返回一个新的Promise对象.
> 返回的新的Promise对象的状态是由参数arr 数组中的Promise对象来决定,这个数组中有成功的Promise,也有失败的Promise, 新Promise是看数组中哪个先完成状态改变,无论成功或失败.你成功我就成功. 即最新完成状态改变的成功==>new Promise 则成功,反之;
## Promise --> Promise.then();
> Promise.then((value)=>{},(reason)=>{}) 其返回的也是一个Promise对象
> new Promise 它的状态是看其内部**返回的值**.
> **返回的值** 
> 1,throw "出问题了"; ==> new Promise 状态为 rejected
> 2,return 非Promise 类型对象. ==> new Promise 状态为 fulfilled (成功) 其PromiseResult 保存其 返回的值 
> 3,返回结果为 Promise对象 则你成功我成功,你的值为我的值,反之 .
## Promise --> throw
> throw 抛出问题 改变Promise的状态为rejected
> throw "data-error";
## Promise --> 问题
> * 1,Promise 指定多个回调,多个回调都会执行.
> * 2,Promise 链式如果 需要中断则必须返回一个新的Promise对象且状态为Pending.
>> return new Promise(() => {}); 
## async/await
> * (1) : async function  返回值 为一个Promise 对象.对象状态 和then方法一样.
> > new Promise 它的状态是看其内部**返回的值**.
> **返回的值** 
> 1,throw "出问题了"; ==> new Promise 状态为 rejected
> 2,return 非Promise 类型对象. ==> new Promise 状态为 fulfilled (成功) 其PromiseResult 保存其 返回的值 
> 3,返回结果为 Promise对象 则你成功我成功,你的值为我的值,反之 .

> * (2): await 表达式
> >  * 表达式
> > 1,await右侧的表达式一般为promise对象,但也可以是其它的值.
    > 2,如果表达式是pormise对象,await返回的是promise成功的值.如果 失败则抛出异常.
    > 3,如果表达式是其它的值,则直接将此值作为await的返回值.
> 
> > * 注意
>  await 必须写在aync函数中,但async函数中可以没有await
> 如果await的promise失败了,就会抛出异常,需要通过 try...catch捕获处理.
> 