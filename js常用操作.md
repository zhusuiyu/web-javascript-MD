# js常用操作补充
>整理自[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)
- [内置对象常用操作](#obj)  
&nbsp;&nbsp;&nbsp;&nbsp;  [一、数组操作](#arr)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[(1)修改器方法](#xiugaiqi)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[(2)访问方法](#fangwen)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[(3)迭代方法](#diedai)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[(4)其他](#qita)  
&nbsp;&nbsp;&nbsp;&nbsp;  [二、字符串操作](#string)  
&nbsp;&nbsp;&nbsp;&nbsp;  [三、JSON&Date](#json)  
- [运算符补充](#yunsuan)  
&nbsp;&nbsp;&nbsp;&nbsp;  [>typeof](#typeof)  
- [语句补充](#yuju)  
&nbsp;&nbsp;&nbsp;&nbsp;  [>for in](#forin)  
&nbsp;&nbsp;&nbsp;&nbsp;  [>for of](#forof)  
- [Polyfill](#polyfill)

<br><br>

## <span id="obj">内置对象常用操作</span>
### 一、<span id="arr">数组操作</span>
#### （1）<span id="xiugaiqi">修改器方法</span>
>下面的这些方法会改变调用它们的对象自身的值：

|操作|方法|参数|返回值|浏览器兼容性|polyfill|参考|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|添加元素到数组末尾|push(1,2,3)|添加的元素|新数组的长度|ie5|none|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/push)
|删除数组末尾的元素|pop|none|被删元素|ie5|none|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/pop)
|删除数组最前面的元素|shift|none|被删元素|ie5|none|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/shift)
|添加元素到数组头部|unshift(1,2,3)|添加的元素|新数组的长度|ie5|none|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/unshift)
|颠倒数组排列顺序|reverse|none|none|ie5|none|none|
|对数组排序|sort|可选，指定某种排序的函数，默认unicode位点|排序后的数组|ie5|none|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)|
|数组指定位置删除/添加元素|splice(start, deleteCount, item1, item2, ...)|start:开始位置；<br />deleteCount:可选，删除个数；<br />item：可选，要添加的元素|所删元素组成的数组|ie5|none|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

#### （2）<span id="fangwen">访问方法</span>
>下面的方法不会改变对象本身，返回需要的数组或值：

|操作|方法|参数|返回值|浏览器兼容性|polyfill|参考|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|返回一个由数组所有元素拼接成的字符串|join(separator)|指定一个字符串来分隔，默认','|字符串|ie5|none|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/join)
|返回一个由数组所有元素用逗号隔开的字符串|toString()|none|字符串|yes|none|none|
|返回某个元素在数组中的索引|arr.indexOf()|要查找的元素|index,没有则是-1|ie9|[有](#indexOf)|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)|
|返回截取的新数组(浅拷贝)|slice(begin,end)|begin:可选，开始位置(包含)<br />end:可选，结束位置(不包含)|提取的新数组|ie9|[有](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)|
|返回合并后的数组(浅拷贝)|arr1.concat(arr2,arr3)|用于合并的数组|新数组|yes|none|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)|

#### （3）<span id="diedai">迭代方法</span>
|操作|方法|参数|返回值|浏览器兼容性|polyfill|参考|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|遍历数组(无法终止或跳出循环)|forEach(callback(value,index,array){})|value,index,array|undefined|ie9|[有](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)|
|遍历返回一个想要的数组|map(callback(v,i,arr))|value,index,array|新数组|ie9|[有](#map)|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map)|
|遍历返回过滤后的数组|filter(callback(v,i,arr))|value,index,array|过滤后的新数组|ie9|[有](#filter)|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)|
|遍历是否每个都满足|every||boolean|ie9|none|none|
|遍历至少1个满足|some||boolean|ie9|none|none|

#### （4）<span id="qita">其他</span>
|操作|方法|参数|返回值|浏览器兼容性|polyfill|参考|说明|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|判断是否是数组|arr.isArray(element)|需要检测的值|boolean|ie9|[有](#isArray)|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/isArray)|优于instanceof|

### 二、<span id="string">字符串操作</span>
|操作|方法|参数|返回值|浏览器兼容性|polyfill|参考|
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|返回一个字符串中指定的字符|charAt(index)|索引|指定字符|yes|none|none|
|返回第一次出现的指定查找值的索引(区分大小写)|indexOf(serchValue)|要查找的值|第一次出现的索引，没有则-1|yes|none|none|
|字符串中匹配正则表达式|match(regexp)|正则|包含匹配字符的数组|yes|none|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/match)|
|返回替换指定字符串后的新字符串|replace(reg,newStr\|func)|新字符串\|返回新字符串的函数|新字符串|yes|none|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/replace)
|提取并返回新字符串(比substring灵活)|slice(begin[,end])|包含begin,不包含end,允许使用负数|提取的字符串|yes|none|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/slice)|
|返回指定长度的截取字符串(不推荐使用)|substr(start[,length])|包含start,允许使用负数|提取的字符串|yes|[有](#substr)|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/substr)
|返回开始到结束之间的子集|substring(begin[,end])|包含begin,不包含end,不允许负数|子集|yes|none|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/substring)|
|分割字符串并返回数组|split([separator[,limit]])|separator:字符或正则,分隔它两边的字符，limit:限定数量|数组|yes|none|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/split)|
|删除两端空白字符，返回新字符|trim|none|字符|ie9|[有](#trim)|[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/trim)
|字符串转为小写形式并返回|toLowerCase|none|小写字符串|yes|none|none|
|字符串转为大写形式并返回|toUpperCase|none|大写字符串|yes|none|none|

### 三、<span id="json">JSON&Date</span>
- JSON.parse(str)：解析json字符串
- JSON.stringify(value)：某对象解析成json字符串
- [Date](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date)

## <span id="yunsuan">运算符补充</span>
1. ### typeof  （全兼容）<span id="typeof"></span>
### 示例：
```javascript
// Numbers
typeof 37 === 'number';
typeof 3.14 === 'number';
typeof Math.LN2 === 'number';
typeof Infinity === 'number';
typeof NaN === 'number'; // 尽管NaN是"Not-A-Number"的缩写
typeof Number(1) === 'number'; // 但不要使用这种形式!

// Strings
typeof "" === 'string';
typeof "bla" === 'string';
typeof (typeof 1) === 'string'; // typeof总是返回一个字符串
typeof String("abc") === 'string'; // 但不要使用这种形式!

// Booleans
typeof true === 'boolean';
typeof false === 'boolean';
typeof Boolean(true) === 'boolean'; // 但不要使用这种形式!

// Symbols
typeof Symbol() === 'symbol';
typeof Symbol('foo') === 'symbol';
typeof Symbol.iterator === 'symbol';

// Undefined
typeof undefined === 'undefined';
typeof declaredButUndefinedVariable === 'undefined';
typeof undeclaredVariable === 'undefined'; 

// Objects
typeof {a:1} === 'object';

// 使用Array.isArray 或者 Object.prototype.toString.call
// 区分数组,普通对象
typeof [1, 2, 4] === 'object';

typeof new Date() === 'object';

// 下面的容易令人迷惑，不要使用！
typeof new Boolean(true) === 'object';
typeof new Number(1) === 'object';
typeof new String("abc") === 'object';

// 函数
typeof function(){} === 'function';
typeof class C{} === 'function'
typeof Math.sin === 'function';
typeof new Function() === 'function';
```

## <span id="yuju">语句补充</span>
1. ### 遍历对象 for in（兼容至ie6）<span id="forin"></span>
>for ( variable  in object ){ }，以任意顺序遍历一个对象的可枚举属性，取其对应值obj[variable]
2. ### 遍历任意 for of（兼容至edge，不推荐使用） <span id="forof"></span>

## <span id="polyfill">Polyfill</span>
1. <span id="isArray">isArray</span>  
```javascript
if (!Array.isArray) {
  Array.isArray = function(arg) {
    return Object.prototype.toString.call(arg) === '[object Array]';
  };
}
```
2. <span id="indexOf">indexOf</span> 
```javascript
// Production steps of ECMA-262, Edition 5, 15.4.4.14
// Reference: http://es5.github.io/#x15.4.4.14
if (!Array.prototype.indexOf) {
  Array.prototype.indexOf = function(searchElement, fromIndex) {

    var k;

    // 1. Let O be the result of calling ToObject passing
    //    the this value as the argument.
    if (this == null) {
      throw new TypeError('"this" is null or not defined');
    }

    var O = Object(this);

    // 2. Let lenValue be the result of calling the Get
    //    internal method of O with the argument "length".
    // 3. Let len be ToUint32(lenValue).
    var len = O.length >>> 0;

    // 4. If len is 0, return -1.
    if (len === 0) {
      return -1;
    }

    // 5. If argument fromIndex was passed let n be
    //    ToInteger(fromIndex); else let n be 0.
    var n = +fromIndex || 0;

    if (Math.abs(n) === Infinity) {
      n = 0;
    }

    // 6. If n >= len, return -1.
    if (n >= len) {
      return -1;
    }

    // 7. If n >= 0, then Let k be n.
    // 8. Else, n<0, Let k be len - abs(n).
    //    If k is less than 0, then let k be 0.
    k = Math.max(n >= 0 ? n : len - Math.abs(n), 0);

    // 9. Repeat, while k < len
    while (k < len) {
      // a. Let Pk be ToString(k).
      //   This is implicit for LHS operands of the in operator
      // b. Let kPresent be the result of calling the
      //    HasProperty internal method of O with argument Pk.
      //   This step can be combined with c
      // c. If kPresent is true, then
      //    i.  Let elementK be the result of calling the Get
      //        internal method of O with the argument ToString(k).
      //   ii.  Let same be the result of applying the
      //        Strict Equality Comparison Algorithm to
      //        searchElement and elementK.
      //  iii.  If same is true, return k.
      if (k in O && O[k] === searchElement) {
        return k;
      }
      k++;
    }
    return -1;
  };
}
```
3. <span id="map">map</span>
```javascript
// 实现 ECMA-262, Edition 5, 15.4.4.19
// 参考: http://es5.github.com/#x15.4.4.19
if (!Array.prototype.map) {
  Array.prototype.map = function(callback, thisArg) {

    var T, A, k;

    if (this == null) {
      throw new TypeError(" this is null or not defined");
    }

    // 1. 将O赋值为调用map方法的数组.
    var O = Object(this);

    // 2.将len赋值为数组O的长度.
    var len = O.length >>> 0;

    // 3.如果callback不是函数,则抛出TypeError异常.
    if (Object.prototype.toString.call(callback) != "[object Function]") {
      throw new TypeError(callback + " is not a function");
    }

    // 4. 如果参数thisArg有值,则将T赋值为thisArg;否则T为undefined.
    if (thisArg) {
      T = thisArg;
    }

    // 5. 创建新数组A,长度为原数组O长度len
    A = new Array(len);

    // 6. 将k赋值为0
    k = 0;

    // 7. 当 k < len 时,执行循环.
    while(k < len) {

      var kValue, mappedValue;

      //遍历O,k为原数组索引
      if (k in O) {

        //kValue为索引k对应的值.
        kValue = O[ k ];

        // 执行callback,this指向T,参数有三个.分别是kValue:值,k:索引,O:原数组.
        mappedValue = callback.call(T, kValue, k, O);

        // 返回值添加到新数组A中.
        A[ k ] = mappedValue;
      }
      // k自增1
      k++;
    }

    // 8. 返回新数组A
    return A;
  };      
}
```
4. <span id="filter">filter</span>
```javascript
if (!Array.prototype.filter)
{
  Array.prototype.filter = function(fun /* , thisArg*/)
  {
    "use strict";

    if (this === void 0 || this === null)
      throw new TypeError();

    var t = Object(this);
    var len = t.length >>> 0;
    if (typeof fun !== "function")
      throw new TypeError();

    var res = [];
    var thisArg = arguments.length >= 2 ? arguments[1] : void 0;
    for (var i = 0; i < len; i++)
    {
      if (i in t)
      {
        var val = t[i];

        // NOTE: Technically this should Object.defineProperty at
        //       the next index, as push can be affected by
        //       properties on Object.prototype and Array.prototype.
        //       But that method's new, and collisions should be
        //       rare, so use the more-compatible alternative.
        if (fun.call(thisArg, val, i, t))
          res.push(val);
      }
    }

    return res;
  };
}
```
5. <span id="substr">substr</span>
```javascript
// only run when the substr function is broken
if ('ab'.substr(-1) != 'b')
{
  /**
   *  Get the substring of a string
   *  @param  {integer}  start   where to start the substring
   *  @param  {integer}  length  how many characters to return
   *  @return {string}
   */
  String.prototype.substr = function(substr) {
    return function(start, length) {
      // did we get a negative start, calculate how much it is
      // from the beginning of the string
      if (start < 0) start = this.length + start;
      
      // call the original function
      return substr.call(this, start, length);
    }
  }(String.prototype.substr);
}
```
6. <span id="trim">trim</span>
```javascript
if (!String.prototype.trim) {
  String.prototype.trim = function () {
    return this.replace(/^[\s\uFEFF\xA0]+|[\s\uFEFF\xA0]+$/g, '');
  };
}
```

