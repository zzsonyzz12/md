[toc]
[axios中文文档](http://www.axios-js.com/)
## axios --> config
```
$("button").eq(0).click(function () {
    let url = "http://localhost:3000";
    let cancel = null;
    //判断上一次请求是否成功,如果是成功了cancel 的值会被 then 方法修改为 null 
    if (cancel !== null) {
        //进入判断 即表明正在等待,所以取消上一次请求
        cancel();
    }
    axios({
        //config 选项说明
        // (1) url : 是用于请求的服务器地址
        url: "/posts",
        // (2) method  : 创建请求时使用的方法默认是 get
        method: 'get',
        // (3) baseURL : 自动加在 url 前面 ,除非 url 是绝对路径
        baseURL: 'http://localhost:3000',
        // (4) transformRequest : 向服务器发送前对数据进行修改处理 且必须返回一个字符串
        // 只能用在 'PUT','POST','PATCH',这几个方法中
        transformRequest: [
            (data) => {
                //对 data 进行处理
                return data;
            },
        ],
        // (5) transformResponse : 在传递给 'then / catch '方法前对 响应 的数据进行修改 也必须返回一个字符串
        transformResponse: [
            (data) => {
                //对 data 进行处理 
                return data;
            }
        ],
        // (6) headers : 自定义请求头
        headers: {
            'X-Requested-With': 'XMLHttpRequest'
        },
        // (7) params : 设置与请求一起发送的 URL 参数 
        params: {
            //会表现为: 
            ID: 12345,
        },
        // (8) paramsSerializer :  是一个负责 `params` 序列化的函数
        // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
        paramsSerializer: function (params) {
            return Qs.stringify(params, {
                arrayFormat: 'brackets'
            })
        },
        // (9) data : 作为请求主体被发送的数据 适用于:'PUT','PATH','POST';
        data: {
            firstName: 'xiaobai'
        },
        // (10) timeout : 指定请求超时的毫秒数( 0 表示无超时时间) 超过时间没有响应就中断
        timeout: 1000,
        // (11) withCredentials : 表示跨域请求时是否需要使用凭证 默认是 false
        withCredentials: false,
        // (12) auth : 表示使用 HTTP 基础验证,并提供凭据
        //这将设置一个'Authorization' 头,覆盖掉现有的  headers 
        auth: {
            username: 'xiaobai',
            password: '123456',
        },
        // (13) responseType : 表示服务器响应的数据类型 (arraybuffer/blob/document/json/text/strem) 默认是 json 
        responseType: 'json',
        // (14) xsrfCookieName : 是用作 xsrf token 的值的cookie的名称
        xsrfCookieName: 'XSRF-TOKEN', //默认值
        // (15) xsrfHeaderName : 是承载 xsrf token 的值的 HTTP 头的名称
        xsrfHeaderName: 'X-XSRF-TOKEN', // 默认值
        // (16) cancelToken : 用于取消请求  let cancel = null 定义一个全局变量;              
        cancelToken: new CancelToken((c) => {
            //这个 C 是一个函数参数 赋值给全局变量 cancel 
            //在需要取消的地方调用 cancel(); 这个函数即可取消这个请求
            //常用 情况会在发送请求时检测上一次的请求状态,并取消上一次请求,重新发送
            cancel = c;
        }),
    }).then(result => {
        cancel = null;
    }).catch(response => {

    });

 });

```
## axios --> response 响应体
```
{
    // (1) data:由服务器提供响应的数据
    data:{},
    // (2) status: 来自服务器响应的 HTTP 状态码
    status:200,
    // (3) statusText: 来自服务器响应的 HTTP 状态信息 ()
    statusText:'ok',
    // (4) headers: 所有的响应头名称都是小写
    headers:{};
    // (5) config: axios 请求配置
    config:{};
    // (6) request: 请求
    request: {};
}
// 用 then 可以接受以下的响应信息
axios.get('/user/12345')
  .then(function(response) {
    console.log(response.data);
    console.log(response.status);
    console.log(response.statusText);
    console.log(response.headers);
    console.log(response.config);
  });
```
## axios --> cancelToken 取消请求
> 取消请求,需要在请求体 config 中 new CancelToken((c)=>{}) 这个函数
```
//定义一个全局变量来接受 'CancelToken'函数
let cancel = null;
axios({
    url:'/url',
    method:'GET',
    cancelToken:new CancelToken((c)=>{
        //把 c 函数赋值给cancel 
        cancel = c ;
    })
}).then(value=>{
    //这里如果成功就把 cancel 初始化
    cancel = null ;
}).catch(response=>{
    console.log(response);
})

//在每一个函数调用之前需要检验上一次的请求是否完成 即判断 cancel 的值是否为初始值 null 因为如果成功我们 then 方法会把 cancel 的值初始化.
if(cancel !== null ){
    //调用取消函数
    cancel();
}

```
## axios --> 方法/参数
* axios.request(config),
* axios.get(url,[config]),
* axios.delete(url,[config]),
* axios.head(url,[config]),
* axios.options(url,[config]),
* axios.post(url,[data],[config]),
* axios.put(url,[data],[config]),
* axios.patch(url,[data],[config]),
* axios.all([]) //处理多个请求 all方法的使用和promise的一样
> 在使用以上别名时 url / method / data 属性不用在config 中重复声明 .
> 
## axios --> defaults 全局默认配置
可以设置 config 中的多数选项 通过 axios.defaults.xxx = ''来设置
> axios.defaults.baseURL = 'https://api.example.com';
> axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
> axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
## axios --> create 实例化配置
> 可以通过 create 创建多个实例 以达到每个实例的配置不同 可直接对应每个请求 API
```
 let instance = aixos.create({
        baseURL:'http://localhost:3000',
        url: '/posts',
     })
     //这 axiosapi 基本和 axios 一样使用
    instance();
```
## axios --> instance.defaults 优先级配置
> 优先级别大小为: request config > instance.defaults > 系统默认
> intance 为实例对象
> 用法 : 
```
// 创建一个实例，这时的超时时间为系统默认的 0
var instance = axios.create();
// 通过instance.defaults重新设置超时时间为2.5s，因为优先级比系统默认高
instance.defaults.timeout = 2500;
// 通过request config重新设置超时时间为5s，因为优先级比instance.defaults和系统默认都高
instance.get('/longRequest', {
  timeout: 5000
});
```
## aixos --> interceptors 拦截器
> 添加拦截器可以在 then 和 catch 之前拦截请求和响应.
> 可以添加多个拦截器, 请求拦截器处理结果为 **先进后出**
> 响应拦截器处理结果为 **先进先出**
> 所有拦截器处理完了才会执行 then / catch 
>用法 : 
```
// 添加一个 请求拦截器 多个请求拦截器 优先执行 后面的拦截器
axios.interceptors.request.use(function (config) {
    // 在请求之前需要操作的...即可以对 config 参数进行处理再提交请求.
    return config;
  }, function (error) {
    return Promise.reject(error);
  });
// 添加一个响应拦截器 多个响应拦截器 按顺序执行 与请求拦截器相反.
axios.interceptors.response.use(function (response) {
    //可以对响应体做修改
    return response;
  }, function (error) {
    return Promise.reject(error);
  });
```
