链接：<http://elf8848.iteye.com/blog/347566>

无论是window.setTimeout还是window.setInterval，在使用函数名作为调用句柄时都不能带参数，而在许多场合必须要带参数，这就需要想方法解决。经网上查询后整理如下：
例如对于函数hello(_name)，它用于针对用户名显示欢
迎信息：
var userName="jack";
//根据用户名显示欢迎信息
function hello(_name){
      alert("hello,"+_name);
}
这时，如果企图使用以下语句来使hello函数延迟3秒执行是不可行的：
window.setTimeout(hello(userName),3000);
这将使hello函数立即执行，并将返回值作为调用句柄传递给setTimeout函数，其结果并不是程序需要的。而使用字符串形式可以达到想要的结果：
window.setTimeout("hello(userName)",3000);这是方法（一） 
这里的字符串是一段JavaScript代码，其中的userName表示的是变量。但这种写法不够直观，而且有些场合必须使用函数名，于是有人想到了如下
方法（二）：
<script language="JavaScript" type="text/javascript">
<!--
var userName="jack";
//根据用户名显示欢迎信息
function hello(_name){
       alert("hello,"+_name);
}
//创建一个函数，用于返回一个无参数函数
function _hello(_name){
       return function(){
             hello(_name);
       }
}
window.setTimeout(_hello(userName),3000);
//-->
</script>
这 里定义了一个函数_hello，用于接收一个参数，并返回一个不带参数的函数，在这个函数内部使用了外部函数的参数，从而对其调用，不需要使用参数。在 window.setTimeout函数中，使用_hello(userName)来返回一个不带参数的函数句柄，从而实现了参数传递的功能。
另外也有人通过修改settimeout、setInterval来实现。即下面的
方法三：
`<script language="JavaScript" type="text/javascript">
<!--
var userName="jack";
//根据用户名显示欢迎信息
function hello(_name){
       alert("hello,"+_name);
}//*=============================================================
//*   功能： 修改 window.setInterval ，使之可以传递参数和对象参数    
//*   方法： setInterval (回调函数,时间,参数1,,参数n)  参数可为对象:如数组等
//*============================================================= 
var __sto = setInterval;     
window.setInterval = function(callback,timeout,param){     
    var args = Array.prototype.slice.call(arguments,2);     
    var _cb = function(){     
        callback.apply(null,args);     
    }     
    __sto(_cb,timeout);     
}
window.setInterval(hello,3000,userName);
//-->`