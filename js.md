编码和重排

JavaScript 有 七 种 内 置 类 型:null、undefined、boolean、number、string、object 和
symbol,可以使用 typeof 运算符来查看。 变量没有类型,但它们持有的值有类型。类型定义了值的行为特征。

我们需要使用复合条件来检测 null 值的类型: 
    var a = null;
    (!a && typeof a === "object"); // true

JavaScript 中的变量是没有类型的,只有值才有。变量可以随时持有任何类型的值。
undefined 类型只有一个值,即 undefined。null 类型也只有一个值,即 null。它们的名称既是类型也是值。

undefined”和“is not defined”是两码事。此时如果浏览器 报错成“b is not found”或者“b is not declared”会更准确。

很多开发人员将 undefined 和 undeclared 混为一谈,但在 JavaScript 中它们是两码事。 undefined 是值的一种。undeclared 则表示变量还没有被声明过。
遗憾的是,JavaScript 却将它们混为一谈,在我们试图访问 "undeclared" 变量时这样报 错:ReferenceError: a is not defined,并且typeof对undefined和undeclared变量都返回 "undefined"。
然而,通过 typeof 的安全防范机制(阻止报错)来检查 undeclared 变量,有时是个不错的 办法。

许多数组函数用来处理字符串很方便。虽然字符串没有这些函数,但可以通过“借用”数 组的非变更方法来处理字符串:
    a.join;         // undefined
    a.map;          // undefined
    var c = Array.prototype.join.call( a, "-" );
    var d = Array.prototype.map.call( a, function(v){
       return v.toUpperCase() + ".";
    } ).join( "" );
    c;              // "f-o-o"
    d;              // "F.O.O."
   
更成员函数 reverse():
    a.reverse;
    b.reverse();
    b;
    // undefined
    // ["!","o","O","f"]
    // ["f","O","o","!"]
可惜我们无法“借用”数组的可变更成员函数,因为字符串是不可变的:
    Array.prototype.reverse.call( a );
// 返回值仍然是字符串"foo"的一个封装对象(参见第3章):(
一个变通(破解)的办法是先将字符串转换为数组,待处理完后再将结果转换回字符串:
    var c = a
// 将a的值转换为字符数组 .split( "" )
// 将数组中的字符进行倒转 .reverse()
// 将数组中的字符拼接回字符串 .join( "" );
    c; // "oof"
这种方法的确简单粗暴,但对简单的字符串却完全适用。

tofixed(..) 方法可指定小数部分的显示位数:
a.toFixed( 2 ); // "42.59"
toPrecision(..) 方法用来指定有效数位的显示位数:
a.toPrecision( 2 ); // "43"

0.1 + 0.2 === 0.3; // false
可以使用 Number.EPSILON 来比较两个数字是否相等(在指定的误差范围内):
     if (!Number.EPSILON) {
           Number.EPSILON = Math.pow(2,-52);
     }
     function numbersCloseEnoughToEqual(n1,n2) {
         return Math.abs( n1 - n2 ) < Number.EPSILON;
      }
     var a = 0.1 + 0.2;
     var b = 0.3;
     numbersCloseEnoughToEqual( a, b );
     numbersCloseEnoughToEqual( 0.0000001, 0.0000002 );  // false
     
NAN:not a number
很多 JavaScript 程序都可能存在 NaN 方面的问题,所以我们应该尽量使用 Number.isNaN(..) 这样可靠的方法,无论是系统内置还是 polyfill。
如果你仍在代码中使用 isNaN(..),那么你的程序迟早会出现 bug。
    if (!Number.isNaN) {
       Number.isNaN = function(n) {
           return n !== n;
       };
    }
    
    var a = 1 / 0;  // Infinity
    var b = -1 / 0; // -Infinity
    
数字类型有几个特殊值,包括 NaN(意指“not a number”,更确切地说是“invalid number”)、+Infinity、-Infinity 和 -0。

以下方法并不改变原字符串的值,而是返回一个新字符串。
    • String#indexOf(..) 在字符串中找到指定子字符串的位置。
    • String#charAt(..) 获得字符串指定位置上的字符。
    • String#substr(..)、String#substring(..) 和 String#slice(..) 获得字符串的指定部分。
    • String#toUpperCase() 和 String#toLowerCase() 将字符串转换为大写或小写。
    • String#trim() 去掉字符串前后的空格,返回新的字符串。
将对象强制类型转换为 string 是通过 ToPrimitive 抽象操作来完成的。
工具函数 JSON.stringify(..) 在将 JSON 对象序列化为字符串时也用到了 ToString。
所有安全的 JSON 值(JSON-safe)都可以使用 JSON.stringify(..) 字符串化。安全的 JSON 值是指能够呈现为有效 JSON 格式的值。
为了简单起见,我们来看看什么是不安全的 JSON 值。undefined、function、symbol (ES6+)和包含循环引用(对象之间相互引用,形成一个无限循环)的对象都不符合JSON结构标准,支持 JSON 的语言无法处理它们。
我们可以向 JSON.stringify(..) 传递一个可选参数 replacer,它可以是数组或者函数,用 来指定对象序列化过程中哪些属性应该被处理,哪些应该被排除,和 toJSON() 很像。
如果 replacer 是一个数组,那么它必须是一个字符串数组,其中包含序列化要处理的对象 的属性名称,除此之外其他的属性则被忽略。
如果 replacer 是一个函数,它会对对象本身调用一次,然后对对象中的每个属性各调用 一次,每次传递两个参数,键和值。如果要忽略某个键就返回 undefined,否则返回指定 的值。
SON.string 还有一个可选参数 space,用来指定输出的缩进格式。space 为正整数时是指定 每一级缩进的字符数,它还可以是字符串,此时最前面的十个字符被用于每一级的缩进:
请记住,JSON.stringify(..) 并不是强制类型转换。在这里介绍是因为它涉及 ToString 强
制类型转换,具体表现在以下两点。
(1) 字符串、数字、布尔值和 null 的 JSON.stringify(..) 规则与 ToString 基本相同。
(2) 如果传递给 JSON.stringify(..) 的对象中定义了 toJSON() 方法,那么该方法会在字符
串化前调用,以便将对象转换为安全的 JSON 值。

ToNumber
其中 true 转换为 1,false 转换为 0。undefined 转换为 NaN,null 转换为 0。
使用 Object.create(null) 创建的对象 [[Prototype]] 属性为 null,并且没 有 valueOf() 和 toString() 方法。

以下这些是假值:
• undefined
• null
• false
• +0、-0 和 NaN
• ""
真值就是假值列表之外的值。

(1)如果Type(x)是数字,Type(y)是字符串,则返回x == ToNumber(y)的结果。 
(2)如果Type(x)是字符串,Type(y)是数字,则返回ToNumber(x) == y的结果。
重点是我们要搞清楚 == 对不同的类型组合怎样处理。== 两边的布尔值会被强制类型转换为数字。
很奇怪吧?我个人建议无论什么情况下都不要使用== true和== false。

(1) 如果 x 为 null,y 为 undefined,则结果为 true。
(2) 如果 x 为 undefined,y 为 null,则结果为 true。

(1)如果Type(x)是字符串或数字,Type(y)是对象,则返回x == ToPrimitive(y)的结果; 
(2)如果Type(x)是对象,Type(y)是字符串或数字,则返回ToPromitive(x) == y的结果。

但有一些值不这样,原因是 == 算法中其他优先级更高的规则。例如:
    var a = null;
    var b = Object( a );
    a == b;
    var c = undefined;
    var d = Object( c );
    c == d;
    var e = NaN;
    var f = Object( e );
    e == f;
// 和Object()一样 // false
// 和Object()一样 // false
// 和new Number( e )一样 // false
因为没有对应的封装对象,所以 null 和 undefined 不能够被封装(boxed),Object(null) 和 Object() 均返回一个常规对象。

• 如果两边的值中有true或者false,千万不要使用==。 
• 如果两边的值中有[]、""或者0,尽量不要使用==。
