**/1.检测类型可以用typeof 和 instanceof**

```javascript
//语法
result = variable（A） instanceof construuctor(B)
alert(person instanceof object)//person 是 object?
//A是变量名，B是结构，array等
```

**2.关于变量作用域，和C语言类似。内存分配。**

```javascript
//if则不同，变量不会被销毁
if(true){
    var color = "blue";
}
alert(color);//blue
//在函数中，使用var是局部，不使用是全局（最好加var）
  function add(num1, num2) {
            var sum = num1 + num2;
            return sum;
        }
        
        var result = add(10, 20);  //30
        alert(sum);                //causes an error since sum is not a valid variable
//去掉var则正确
```

**可以使用try-catch 的catch 和with延长作用域链**

try{ //正常执行 }catch(e/*你感觉会出错的 错误类型*/){ // 可能出现的意外 eg:用户自己操作失误 或者 函数少条件 不影响下面的函数执行 // 有时也会用在 比如 focus() 但可恶的ie有可能会第一次没有focus事件 再让他执行一次 // 有时一些不是bug的bug 在ie上 他要求必须加上 catch 哪怕就一个空catch 以前在ie8上遇到过这个操蛋的js问题 }

可以这样用

1、事情还有得挽回，换条路走
try {
执行某个逻辑
} catch (e) {
出问题鸟，换个逻辑执行
}

2、体面的退出
try {
正常流程
} catch (e) {
弹个框告诉用户不好意思出了点问题
如果是用户的错就告诉用户什么地方错了
如果是程序的错，就告诉用户不好意思没法执行
}

> *基本类型被保存在栈中，引用类型被保存在堆中。*

对于不用的引用类型，手动消除。

```javascript
function creatPerson(name0){
    var localPerson = new object();
    localPerson.name = name;
    return localPerson;
}
var globalPerson = createPerson("haha");

//手动解除
globalPerson = null;
```

**3.引用类型**

3.1Object

```javascript
 person.name = "Nicholas";
        person.age = 29;
//和以下同
   var person = {
            name : "Nicholas",
            age : 29
        };
        //应用
        function displayInfo(args) {
            var output = "";
        
            if (typeof args.name == "string"){
                output += "Name: " + args.name + "\n";
            }
        
            if (typeof args.age == "number") {
                output += "Age: " + args.age + "\n";
            }
        
            alert(output);
        }
        
        displayInfo({ 
            name: "Nicholas", 
            age: 29
        });
        
        displayInfo({
            name: "Greg"
        });
//.和[]的使用。[]可以通过变量访问属性
var person = new object();
person.name = "haha";
var propertyName = name;
alert(person[propertyName]);//haha
```

3.2Array类型

```javascript
//创建数组
var color = Array(3);
//或者
 var colors = ["red", "blue", "green"];    //creates an array with three strings
        colors.length = 2;
        alert(colors[2]);        //undefined
        //通过改变.length来改变数组长度
        
var colors = ["red", "blue", "green"];    //creates an array with three strings
        colors[colors.length] = "black";          //add a color
        colors[colors.length] = "brown";          //add another color

        alert(colors.length);    //5
        alert(colors[3]);        //black
        alert(colors[4]);        //brown
        /*不管是那个环境创建的数组都可以用
        Array.isArray(Array's name)来确定。返回值是布尔*/
        //toString()各各数值拼接成的字符串,valueOf()数组本身,toLocaleString()貌似无用
         var colors = ["red", "blue", "green"];    //creates an array with three strings
        alert(colors.toString());    //red,blue,green
        alert(colors.valueOf());     //red,blue,green
        alert(colors);               //red,blue,green
//join（）一个参数——分割数组元素的符号
  var colors = ["red", "green", "blue"];
        alert(colors.join(","));      //red,green,blue
        alert(colors.join("||"));     //red||green||blue
//栈方法，后进先出，如下：
//push()接收任意参数，添加到数组末尾，返回length
//pop()移除最后一项，返回length
  var colors = new Array();                      //create an array
        var count = colors.push("red", "green");       //push two items
        alert(count);  //2
        
        count = colors.push("black");                  //push another item on
        alert(count);  //3
        
        var item = colors.pop();                       //get the last item
        alert(item);   //"black"
        alert(colors.length);  //2
//或者
var colors = ["red", "blue"];
        colors.push("brown");              //add another item
        colors[3] = "black";               //add an item
        alert(colors.length);  //4
        
        var item = colors.pop();           //get the last item
        alert(item);  //"black"
//队列方法，先进后出：
//shift()（删除第一项并返回该项）和push()结合，像队列一样使用数组
  var colors = new Array();                      //create an array
        var count = colors.push("red", "green");       //push two items
        alert(count);  //2
        
        count = colors.push("black");                  //push another item on
        alert(count);  //3
        
        var item = colors.shift();                     //get the first item
        alert(item);   //"red"
        alert(colors.length);  //2
//unshift()(在前端添加任意项并返回长度)和pop()也可以模拟队列
var colors = new Array();                      //create an array
        var count = colors.unshift("red", "green");    //push two items
        alert(count);  //2
        
        count = colors.unshift("black");               //push another item on
        alert(count);  //3
        
        var item = colors.pop();                     //get the first item
        alert(item);   //"green"
        alert(colors.length);  //2


```

Array的排序

```javascript
//reverse()直接逆向排sort()按字符串排序，返回值是数组
  var values = [0, 1, 5, 10, 15];
        values.sort();
        alert(values);    //0,1,10,15,5
 var values = [1, 2, 3, 4, 5];
        values.reverse();
        alert(values);       //5,4,3,2,1
//可以写函数使sort()按数值排序，返回值是数组
        function compare(value1, value2) {
            if (value1 < value2) {
                return 1;
            } else if (value1 > value2) {
                return -1;
            } else {
                return 0;
            }
        }
        //return value1-value2;
        var values = [0, 1, 5, 10, 15];
        values.sort(compare);
        alert(values);    //15,10,5,1,0

```

**4.操作方法**

```javascript
//concat()添加元素到数组末尾
 var colors = ["red", "green", "blue"];
        var colors2 = colors.concat("yellow", ["black", "brown"]);
        
        alert(colors);     //red,green,blue        
        alert(colors2);    //red,green,blue,yellow,black,brown
//slice()一个参数时返回从该位置到结尾的数组，两个参数则为不包括结束位置的数组
 var colors = ["red", "green", "blue", "yellow", "purple"];
        var colors2 = colors.slice(1);
        var colors3 = colors.slice(1,4);
        
        alert(colors2);   //green,blue,yellow,purple
        alert(colors3);   //green,blue,yellow

```

splice()

删除：splice(起始位置，数量)

插入：splice（起始位置，0，元素1...2）

替换：splice（起始位置，删除的个数，插入元素1....2）

```javascript
var colors = ["red", "green", "blue"];
        var removed = colors.splice(0,1);              //remove the first item
        alert(colors);     //green,blue
        alert(removed);    //red - one item array
        
        removed = colors.splice(1, 0, "yellow", "orange");  //insert two items at position 1
        alert(colors);     //green,yellow,orange,blue
        alert(removed);    //empty array

        removed = colors.splice(1, 1, "red", "purple");    //insert two values, remove one
        alert(colors);     //green,red,purple,orange,blue
        alert(removed);    //yellow - one item array
```

//indexOf()和lastIndexOf()

```javascript
 var numbers = [1,2,3,4,5,4,3,2,1];
        
        alert(numbers.indexOf(4));        //3
        alert(numbers.lastIndexOf(4));    //5
        
        alert(numbers.indexOf(4, 4));     //5
        alert(numbers.lastIndexOf(4, 4)); //3       

        var person = { name: "Nicholas" };
        var people = [{ name: "Nicholas" }];
        var morePeople = [person];
        
        alert(people.indexOf(person));     //-1
        alert(morePeople.indexOf(person)); //0
        //前者从头找,后者从后找
```

**迭代方法**

every()数组中每一项都满足条件则返回true而some()有一个就行

```javascript
var numbers = [1,2,3,4,5,4,3,2,1];
        
        var everyResult = numbers.every(function(item, index, array){
            return (item > 2);
        });
        
        alert(everyResult);       //false
        
        var someResult = numbers.some(function(item, index, array){
            return (item > 2);
        });
        
        alert(someResult);       //true
```

filter()返回数组中符合条件的元素组成的新数组

```javascript
  var numbers = [1,2,3,4,5,4,3,2,1];
        
        var filterResult = numbers.filter(function(item, index, array){
            return (item > 2);
        });
        
        alert(filterResult);   //[3,4,5,4,3]

```

map()返回数组中每一项运行给定函数的结果，forEach()相似，但不返回结果

```javascript
       var numbers = [1,2,3,4,5,4,3,2,1];
        
        var mapResult = numbers.map(function(item, index, array){
            return item * 2;
        });
        
        alert(mapResult);   //[2,4,6,8,10,8,6,4,2]
```

**归并方法**

reduce（）和reduceRight()方向不同，返回运算结果

```javascript
//reduce（函数（第一个值，当前值，索引开始项，数组名），归并初始值，默认0）
   var values = [1,2,3,4,5];
        var sum = values.reduce(function(prev, cur, index, array){
            return prev + cur;
        });
        alert(sum);//15

```

**Date类型**

```javascript
  //构建时间如下，月份从0开始
  //January 1, 2000 at midnight in local time
        var y2k = new Date(2000, 0);
        alert(y2k.toLocaleString());
        
        //May 5, 2005 at 5:55:55 PM in local time
        var allFives = new Date(2005, 4, 5, 17, 55, 55);
        alert(allFives.toLocaleString());
        //输出用toLocaleSting就行
        var start = Date.now();
        //获取当前时间的毫秒值
        //更多方法，P102
        
        
```

**RegExp类型**

var expression = /patter/flages;

//pattern是任何简单或者复杂的正则表达式，flags是一或多个标志

```
g:全部字符串
i：不区分大小写
m:匹配多行
//匹配cat或bat
var pattern2 = /[bc]at/i;//和var pattern2 = new RegExp("[bc]at","i");相等
//匹配所有at结尾3个字符串
var pattern2 = /.at/i;
//([\])等元字符使用时要转义
//RegExp构造对象要双重转义
```

**RegExp方法**

exec（），接收匹配的字符串，返回符号元素组成的数组

```javascript
      var text = "mom and dad and baby";
        
        var pattern = /mom( and dad( and baby)?)?/gi;
        var matches = pattern.exec(text);
        
        alert(matches.index);    //0
        alert(matches.input);    //"mom and dad and baby"
        alert(matches[0]);       //"mom and dad and baby"
        alert(matches[1]);       //" and dad and baby"
        alert(matches[2]);       //" and baby"
//不设置全局标志就只会查找第一个
```

test（），接收字符串参数，模式与参数匹配则true.用于验证用户输入

```javascript
var text = "000-00-0000";
var pattern = /\d{3}-\d{2}-\d{4}/;
if(pattern.test(text)){
    alert("it's matched");
}
```

属性，P108

**Function**

//函数是对象，函数名是指针

调用函数可在 函数前，js会自动把函数提前

函数能做返回值

```javascript
 function callSomeFunction(someFunction, someArgument){
            return someFunction(someArgument);
        }

        function add10(num){
            return num + 10;
        }
        
        var result1 = callSomeFunction(add10, 10);
        alert(result1);   //20
        
        function getGreeting(name){
            return "Hello, " + name;
        }
        
        var result2 = callSomeFunction(getGreeting, "Nicholas");
        alert(result2);   //Hello, Nicholas
//根据属性名创建比较函数
  function createComparisonFunction(propertyName) {
        
            return function(object1, object2){
                var value1 = object1[propertyName];
                var value2 = object2[propertyName];
        
                if (value1 < value2){
                    return -1;
                } else if (value1 > value2){
                    return 1;
                } else {
                    return 0;
                }
            };
        }

        var data = [{name: "Zachary", age: 28}, {name: "Nicholas", age: 29}];
        
        data.sort(createComparisonFunction("name"));
        alert(data[0].name);  //Nicholas
        
        data.sort(createComparisonFunction("age"));
        alert(data[0].name);  //Zachary        
```

//arguments保存传入的参数，argument.callee用来指代该函数，在函数内部  

```javascript
  function factorial(num){
            if (num <= 1) {
                return 1;
            } else {
                return num * arguments.callee(num-1)
            }
        }

        var trueFactorial = factorial;
        
        factorial = function(){
            return 0;
        };
        
        alert(trueFactorial(5));   //120
        alert(factorial(5));       //0

```

this指代当前函数作用域

```javascript
       window.color = "red";
        var o = { color: "blue" };
        
        function sayColor(){
            alert(this.color);
        }
        
        sayColor();     //red
        
        o.sayColor = sayColor;
        o.sayColor();   //blue
```

call和apply主要用于扩充函数作用域

```javascript
     window.color = "red";
        var o = { color: "blue" };
        
        function sayColor(){
            alert(this.color);
        }
        
        sayColor();            //red
        
        sayColor.call(this);   //red
        sayColor.call(window); //red
        sayColor.call(o);      //blue
```

bind()并可以改变作用域

```javascript
       window.color = "red";
        var o = { color: "blue" };
                           
        function sayColor(){
            alert(this.color);
        }
        var objectSayColor = sayColor.bind(o);
        objectSayColor();   //blue

```

**基本包装类型**

最好不要使用布尔对象

```javascript
    var falseObject = new Boolean(false);
        var result = falseObject && true;
        alert(result);  //true

        var falseValue = false;
        result = falseValue && true;
        alert(result);  //false
        
        alert(typeof falseObject);   //object
        alert(typeof falseValue);    //boolean
        alert(falseObject instanceof Boolean);  //true
        alert(falseValue instanceof Boolean);   //false
```

Number类型

```javascript
   var numberObject = new Number(10);
        var numberValue = 99;
        
        //toString() using a radix
        alert(numberObject.toString());       //"10"
        alert(numberObject.toString(2));      //"1010"
        alert(numberObject.toString(8));      //"12"
        alert(numberObject.toString(10));     //"10"
        alert(numberObject.toString(16));     //"a"
        
        //toFixed()四舍五入
        alert(numberObject.toFixed(2));    //outputs "10.00"

        numberObject = new Number(99);
        alert(numberObject.toPrecision(1));    //"1e+2"
        alert(numberObject.toPrecision(2));    //"99"
        alert(numberObject.toPrecision(3));    //"99.0"
           
        alert(typeof numberObject);   //object
        alert(typeof numberValue);    //number
        alert(numberObject instanceof Number);  //true
        alert(numberValue instanceof Number);   //false
        //toExponential()指数形式
```

String类型

```javascript
   var stringObject = new String("hello world");
        var stringValue = "hello world";
        
        alert(typeof stringObject);   //"object"
        alert(typeof stringValue);    //"string"
        alert(stringObject instanceof String);  //true
        alert(stringValue instanceof String);   //false
        //charAt()，charCodeAt()是编码
        slice(),substr(),substring()的用法
           var stringValue = "hello world";
        alert(stringValue.slice(3));        //"lo world"
        alert(stringValue.substring(3));    //"lo world"
        alert(stringValue.substr(3));       //"lo world"
        alert(stringValue.slice(3, 7));     //"lo w"
        alert(stringValue.substring(3,7));  //"lo w"
        alert(stringValue.substr(3, 7));    //"lo worl"
        
        alert(stringValue.slice(-3));         //"rld"
        alert(stringValue.substring(-3));     //"hello world"
        alert(stringValue.substr(-3));        //"rld"
        alert(stringValue.slice(3, -4));      //"lo w"
        alert(stringValue.substring(3, -4));  //"hel"
        alert(stringValue.substr(3, -4));     //"" (empty string)
```

//indexOf()和lastIndexOf()

```javascript
 var stringValue = "hello world";
        alert(stringValue.indexOf("o"));         //4
        alert(stringValue.lastIndexOf("o"));     //7
        alert(stringValue.indexOf("o", 6));         //7
        alert(stringValue.lastIndexOf("o", 6));     //4                
       var stringValue = "Lorem ipsum dolor sit amet, consectetur adipisicing elit";
        var positions = new Array();
        var pos = stringValue.indexOf("e");
        
        while(pos > -1){
            positions.push(pos);
            pos = stringValue.indexOf("e", pos + 1);
        }
            
        alert(positions);    //"3,24,32,35,52"     
```

//trim()返回字符串去除空格后的副本

大小写转换,用locale

```javascript
  var stringValue = "hello world";
        alert(stringValue.toLocaleUpperCase());  //"HELLO WORLD"
        alert(stringValue.toUpperCase());        //"HELLO WORLD"
        alert(stringValue.toLocaleLowerCase());  //"hello world"
        alert(stringValue.toLowerCase());        //"hello world"
```

math()和searh()用于匹配字符串

```javascript
 var text = "cat, bat, sat, fat"; 
        var pattern = /.at/;
        
        var matches = text.match(pattern);        
        alert(matches.index);        //0
        alert(matches[0]);           //"cat"
        alert(pattern.lastIndex);    //0

        var pos = text.search(/at/);
        alert(pos);   //1
//replace的使用
        var result = text.replace("at", "ond");
        alert(result);    //"cond, bat, sat, fat"

        result = text.replace(/at/g, "ond");
        alert(result);    //"cond, bond, sond, fond"

        result = text.replace(/(.at)/g, "word ($1)");
        alert(result);    //word (cat), word (bat), word (sat), word (fat)
      // 正则表达式转义字符 
        function htmlEscape(text){
            return text.replace(/[<>"&]/g, function(match, pos, originalText){
                switch(match){
                    case "<":
                        return "&lt;";
                    case ">":
                        return "&gt;";
                    case "&":
                        return "&amp;";
                    case "\"":
                        return "&quot;";
                }             
            });
        }
```

localeCompare（）

```javascript
   var stringValue = "yellow";       
        alert(stringValue.localeCompare("brick"));  //1
        alert(stringValue.localeCompare("yellow")); //0
        alert(stringValue.localeCompare("zoo"));    //-1
        
        //preferred technique for using localeCompare()
        function determineOrder(value) {
            var result = stringValue.localeCompare(value);
            if (result < 0){
                alert("The string 'yellow' comes before the string '" + value + "'.");
            } else if (result > 0) {
                alert("The string 'yellow' comes after the string '" + value + "'.");
            } else {
                alert("The string 'yellow' is equal to the string '" + value + "'.");
            }
        }
        
        determineOrder("brick");
        determineOrder("yellow");
        determineOrder("zoo");

```

**单体内置对象**

URI编码解决方法

```javascript
encodeURI（）对应decodeURI（）只转换空格
encodeURIComponent()和decodeURIComponent()对任何非法字符编码
  var uri = "http%3A%2F%2Fwww.wrox.com%2Fillegal%20value.htm%23start";
        
        //http%3A%2F%2Fwww.wrox.com%2Fillegal value.htm%23start
        alert(decodeURI(uri));
        
        //http://www.wrox.com/illegal value.htm#start
        alert(decodeURIComponent(uri));
        

```

eval()方法，相当于一个解析器，

```javascript
var msg = “hello world"；
eval("alert(msg)");//hello world
//eval()中的函数和定义的变量在外部也能用（严格模式除外）

```

math对象

```javascript
Math.max/Math.min
var max = Math.max(3, 54, 32, 16);
        alert(max);    //54
        
        var min = Math.min(3, 54, 32, 16);
        alert(min);    //3
    //找到数组中最值
    var values = [1,2,3];
    var max = Math.max.apply(Math,values);
    //apply(作用域，参数)，把Math放第一个，真确设置this,再将任何数组放第二个。
```

Math.ceil/.floor/.round

```javascript
  alert(Math.ceil(25.9));     //26
        alert(Math.ceil(25.5));     //26
        alert(Math.ceil(25.1));     //26
        
        alert(Math.round(25.9));    //26
        alert(Math.round(25.5));    //26
        alert(Math.round(25.1));    //25
                
        alert(Math.floor(25.9));    //25
        alert(Math.floor(25.5));    //25
        alert(Math.floor(25.1));    //25
```

random()

```javascript
//math.random()返回0-1之间随机数
//取得一定范围内的随机数
 function selectFrom(lowerValue, upperValue) {
            var choices = upperValue - lowerValue + 1;
            return Math.floor(Math.random() * choices + lowerValue);
        }
        
        var num = selectFrom(2, 10);
        alert(num);   //number between 2 and 10 (inclusive)
        
        var colors = ["red", "green", "blue", "yellow", "black", "purple", "brown"];
        var color = colors[selectFrom(0, colors.length-1)];
        alert(color);  //any of the strings in the array
```

