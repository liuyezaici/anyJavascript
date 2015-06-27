**Javascript中void是一个操作符，该操作符指定要计算一个表达式但是不返回值。**

void 操作符用法格式如下：
1.  javascript:void (expression)
2.  javascript:void expression

expression 是一个要计算的 Javascript 标准的表达式。表达式外侧的圆括号是选的，但是写上去是一个好习惯。 (实现版本   Navigator 3.0   )

你可以使用 void 操作符指定超级链接。表达式会被计算但是不会为当前文档处装入任何内容。

下面的代码创建了一个超级链接，当用户以后不会发生任何事。当用户链接时，void(0) 计算为 0，但 Javascript 上没有任何效果。

<A HREF="javascript:void(0)">单此处什么也不会发生</A>

下面的代码创建了一个超级链接，用户单时会提交表单。
<A HREF="javascript:void(document.form.submit())">
单此处提交表单</A>
a href=#与 a href=javascript:void(0) 的区别 链接的几种办法

‘#’ 包含了一个位置信息

默认的锚是#top 也就是网页的上端

而javascript:void(0)   仅仅表示一个死链接

这就是为什么有的时候页面很长浏览链接明明是#是

跳动到了页首

而javascript:void(0) 则不是如此

所以调用脚本的时候最好用void(0)

或者<input onclick>

<div onclick>等     

例子：
         <script>
         function openWin()
         {
             console.log('Click me!');
         }
        </script>

<a href="javascript:void(0)" onclick="openWin()">北京</a>
<a href="#" onclick="openWin()">#北京#</a>
