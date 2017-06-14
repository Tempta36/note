用户体验
------
###静态代码和动态交互
* AJAX<br>
例如：在登录和注册的时候，网速不太好或者需要填写的内容很多时，通过http请求之后如果用户输入的某个信息不正确，用户便要重新填写全部的信息，
这样就可能导致丧失一些用户。因此，使用AJAX异步请求之后，用户输入完信息就可以看到提示是否正确输入信息。<br>
* 页面显示（网页结构）<br>
例如：表单显示隔行变色；当菜单项不多时使用fixed固定在顶部；当有好多个可选项时使用鼠标悬停示意用户当前鼠标所选中的内容;用户点击复选框内容
时，复选框能被选中，而无需用户必须点复选框；用户点击选项卡的时候，整个选项卡都可以点击，而不是只能点文字；点击a链接时，使用
```js
<a onfocus='this.blur()' src=''>链接</a>
```
不会出现令人不爽的虚线框<br>

###产品性能
* 减少http请求，编程技巧<br>

###CSS Sprites合并css图片<br>

###注重细节<br>