我们需要使用复合条件来检测 null 值的类型: var a = null;
(!a && typeof a === "object"); // true

JavaScript 中的变量是没有类型的,只有值才有。变量可以随时持有任何类型的值。
undefined 类型只有一个值,即 undefined。null 类型也只有一个值,即 null。它们的名称既是类型也是值。

undefined”和“is not defined”是两码事。此时如果浏览器 报错成“b is not found”或者“b is not declared”会更准确。

JavaScript 有 七 种 内 置 类 型:null、undefined、boolean、number、string、object 和
symbol,可以使用 typeof 运算符来查看。 变量没有类型,但它们持有的值有类型。类型定义了值的行为特征。
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
