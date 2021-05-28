var N=0;  
str=str.replace(/({|})/g, function($0,$1)  
{  
if($1=="{"){ return “<b"+(++N)+">"}  
if($1=="}”){ return "</b"+(N–)+">"}  
});


该正则表达式的主要作用是：弥补了js正则表达式引擎无平衡组功能的缺陷. 提取了嵌套格式内容并对内容进行分级编号。

可用于分析某些表达式的格式，提取深层次嵌套的括号内容等.


//感谢作者 我优化了一下变量 lr 实现了自定义提取首层花括号为数组的方法

var getOutStr = function(s) {
            var tmpSplitTag = 'lrSplit';
            var N =0;
            let newStr = s;
            newStr = newStr.replace(/({|})/g, function($0,$1)
            {
                if($1=="{") {
                    return "<"+tmpSplitTag+(++N)+">";
                }
                if($1=="}"){
                    return "</"+ tmpSplitTag+ (N--) +">";
                }
            });
            //将首节点复原成 { }
            let regAdd1_ = new RegExp("<"+tmpSplitTag+"1>", 'g');
            newStr = newStr.replace(regAdd1_, '{');
            let regAdd2_ = new RegExp("<\/"+tmpSplitTag+"1>", 'g');
            newStr = newStr.replace(regAdd2_, '}');
            //提取首级节点
            let reg_ = new RegExp("{([^\}]+)}");
            let firstTagArray = [];
            function findFirstTagStr(restStr) {
                let findTag = restStr.match(reg_);
                if(findTag) {
                    let findIndex = findTag.index;
                    if(findIndex==0) {
                        firstTagArray.push(findTag[0]);
                    } else {
                        firstTagArray.push(restStr.slice(0, findIndex));
                        firstTagArray.push(findTag[0]);
                    }
                    let rightStr = restStr.slice(findIndex + (findTag[0].length));
                    if(rightStr) {
                        findFirstTagStr(rightStr);
                    }
                } else {
                    firstTagArray.push(restStr);
                }
            }
            findFirstTagStr(newStr);
            //复原
            let removeReg1 = new RegExp("<"+tmpSplitTag+"\\d+>", 'g');
            let removeReg2 = new RegExp("<\/"+tmpSplitTag+"\\d+>", 'g');
            firstTagArray.map(function (str_, n) {
                let newStr = str_;
                newStr =  newStr.replace(removeReg1, '{');
                newStr =  newStr.replace(removeReg2, '}');
                if(newStr != str_) {
                    firstTagArray[n] = newStr;
                }
            });
            return firstTagArray;
        };
