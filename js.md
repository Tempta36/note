###找出数组中最大的元素
```js
Math.max.call(null,arr);
```
============================================================

###将arr2中的内容push到arr1中
```js
Array.prototype.push.apply(arr1,arr2); 
```	
============================================================

###Javascript报uncaught typeerror illegal invocation错误 
在用ajax向后台传值的时候把一个对象当作参数传上去了
============================================================

###向Json里面追加键值对
```js
json['fruit']='apple';
``` 
============================================================ 

```js 
$.ajax({
	async:false,
	contentType:false,
	processData:false
});
```
>async:false的原因
>>表示同步请求。默认情况下，发送的数据将被转换为对象（从技术角度来讲并非字符串）以配合默认内容类型
>>"application/x-www-form-urlencoded"。

>contentType:false的原因
>>因为对于上传文件，我们没有在使用原有的 http 协议，所以 multipart/form-data 请求是基于 http 原有的请求
>>方式 post 而来的.那么来说说这个全新的请求方式与 post 的区别：
>>>    请求头的不同。对于上传文件的请求，contentType = multipart/form-data是必须的，而 post 则不是，毕竟
>>>	post 又不是只上传文件～。
>>>    请求体不同。这里的不同也就是指前者在发送的每个字段内容之间必须要使用分界符来隔开，比如文件的内容和
>>>	文本的内容就需要分隔开，不然服务器就没有办法正常的解析文件，而后者 post 当然就没有分界符直接以
>>>	name = "value"的形似发送。
>>说到这，我们发现在 JQuery ajax() 方法中我们使contentType = false,这不是冲突了吗？这当然没有，因为当我们
>>查看这时的 Request headers，会发现还是有分界符。这就是因为当我们在 form 标签中设置了
>>enctype = “multipart/form-data”,这样请求中的 contentType 就会默认为 multipart/form-data 。而我们在
 >>ajax 中 contentType 设置为 false 是为了避免 JQuery 对其操作，从而失去分界符，而使服务器不能正常解析文
 >>件。
 
>processData:false的原因
>>不序列化data参数 
============================================================

###判断鼠标点击位置是否在指定元素区域内(可用于点击遮罩层使元素消失)
```js
function isInElement(obj){
    return (event.clientX > obj.offset().left && event.clientX < (obj.width()+
    obj.offset().left) && event.clientY > obj.offset().top && event.clientY <
    (obj.height()+ obj.offset().top));
}
```
============================================================

###将时间戳改为普通日期格式
```js
function getLocalTime(ns) {
    console.log(new Date(parseInt(ns) ).toLocaleString().substr(0,17));
    return ns;
}
```
============================================================

###事件冒泡
```js
function stopBubble(e) {
//如果提供了事件对象，则这是一个非IE浏览器
    if ( e && e.stopPropagation )
    //因此它支持W3C的stopPropagation()方法
        e.stopPropagation();
    else
    //否则，我们需要使用IE的方式来取消事件冒泡
        window.event.cancelBubble = true;
}
```
============================================================

###浏览器默认行为
```js
function stopDefault( e ) {
    //阻止默认浏览器动作(W3C)
    if ( e && e.preventDefault )
        e.preventDefault();
    //IE中阻止函数器默认动作的方式
    else
        window.event.returnValue = false;
    return false;
}
```
============================================================

###offset获取当前元素相对于父元素的位移，要获取当前元素相对于body的位移，使用下面的函数
```js
function offSet(curEle) {
        var totalLeft = null;
        var totalTop = null;
        var par = curEle.offsetParent;
        //首先把自己本身的相加
        totalLeft += curEle.offsetLeft;
        totalTop += curEle.offsetTop;
        //现在开始一级一级往上查找，只要没有遇到body，我们就把父级参照物的边框和偏移相加
        while (par){
			//判断浏览器类型
            if (navigator.userAgent.indexOf("MSIE 8.0") === -1){
                //不是IE8我们才进行累加父级参照物的边框
                totalTop += par.clientTop;
                totalLeft += par.clientLeft;
            }
            //把父级参照物的偏移相加
            totalTop += par.offsetTop;
            totalLeft += par.offsetLeft;
            par = par.offsetParent;
        }
        return {left: totalLeft,top: totalTop};
        //返回一个数组，方便我们使用哦。
    }
```
============================================================

###判断浏览器类型
```js
function getOs() {
    var OsObject = "";
   if(navigator.userAgent.indexOf("MSIE")>0) { 
        return "MSIE";
   }
   if(isFirefox=navigator.userAgent.indexOf("Firefox")>0){
        return "Firefox";
   }
   if(isSafari=navigator.userAgent.indexOf("Safari")>0) {
        return "Safari";
   } 
   if(isCamino=navigator.userAgent.indexOf("Camino")>0){
        return "Camino";
   }
   if(isMozilla=navigator.userAgent.indexOf("Gecko/")>0){
        return "Gecko";
   }
}
```
============================================================

###创建具有兼容性的xmlHttpRequest对象
```js
if (window.XMLHttpRequest) { // Mozilla, Safari, ...

    http_request = new XMLHttpRequest();

} else if (window.ActiveXObject) { // IE

    http_request = new ActiveXObject("Microsoft.XMLHTTP");

}
```
============================================================

###继上次在使用jquery的ajax操作碰到程序请求成功：  
>状态码返回200--表明服务器正常响应了客户端的请求；  
>通过firebug和IE的httpWatcher可以看出服务器端返回了正常的数据，并且是符合业务逻辑的数据。  
但是，程序就是不进入到回调函数success: function(data){****}而是进入到error: function(data){***}  
记得上次是因为存在跨域访问的问题导致。这次查看不存在跨域的问题。此时就很是不解。  
事情的来源是这样的： 后台的配置管理模块中有一块是关于国际化的配置，增加国际化描述等等，查询国际化
描述。  
问题的来源是在输入key='a' 查询前十条数据时发现可以正常的展现数据，但是当我输入key值为z时，并且再查
询前20条数据是发现数据不能展现，但是server返回了数据库中的数据。这时第一反应是事不时数据返回的有问
题，粗略的检查了返回的数据发现和第一次查询没有什么明显的区别。但是只查询第十四条数据时发现，显示不
出来。这时候就开始怀疑了数据问题，进而到数据库中查找第十四条数据没有发现什么特别的地方。  
这时开始怀疑，难道是JS程序有处理数据兼容性有问题，觉得甚是不可思议。整了大约半小时，越来越觉得不大
可能。就放弃了这种想法。  
有转向，重新审视数据。 但是发现数据从中间换行了，没太在意。 在纠结了一会儿后问一同事，指出数据可能
多了一个"回车键"，在其指点下到数据库表中再次查看该条数据发现有一个字段的值多了一个"回车键"。删除后，
一切恢复正常。 

============================================================

###ajax post表单后 url会自动改变。如下：
>提交前：localhost:3000/
>提交后：localhost:3000/?user%5Bname%5D=%E5%A4%A7%E6%B4%92%E5%BA%97
>>解决方法1：
```js
$('#form-signup').on('submit', function(ev) {
  ev.stopPropagation();
  ev.preventDefault();
  ...
});
```
>>解决方法2：
>>>form表单的那个button按钮注意下type
```html
<button type="button">submit<button>
```
>>>这样做虽然也可以阻止，但是不建议这么做，有碍于语义化和不能键盘enter操作
