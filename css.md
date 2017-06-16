###td设置relative导致td的border消失，解决如下：<br>
```css
td{
	background-clip:padding-box;
}
```	

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

###创建具有兼容性的xmlHttpRequest对象
```js
if (window.XMLHttpRequest) { // Mozilla, Safari, ...

    http_request = new XMLHttpRequest();

} else if (window.ActiveXObject) { // IE

    http_request = new ActiveXObject("Microsoft.XMLHTTP");

}
```
