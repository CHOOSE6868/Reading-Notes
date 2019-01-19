1<<Professsional JavaScript for Web Devrlopers  >>

​                                                 `Notes`

*219/1/19*

|                      |                      JS的组成                       |                                   |
| :------------------: | :-------------------------------------------------: | :-------------------------------: |
| ECMAScript(核心语言) | DOM（文档对象模型，是提供访问和操作网页内容的方法） | BOM(提供与浏览器交互的方法和接口) |

1.引用外部JS链接时注意，如：

```javascript
<script type="text/javaScript" src="XX">中间不要加其他代码，会被忽略</script>
```

2.页面写的JS放在body最下面，引入外部则加：

```javascript
<script type="text/javaScript" defer="defer" src="XX">中间不要加其他代码，会被忽略</script>
//会先加载，延时执行
<script type="text/javaScript" async src="XX">中间不要加其他代码，会被忽略</script>
//异步执行，让浏览器不等待JS加载
```

3.注意0.1+0.2！=0.3浮点数有精度问题。基于IEEE754数值计算都是这样。

4.关于Number()\parseInt()\parseFloat()

```javascript
 var num1 = Number("Hello world!");  //NaN
        var num2 = Number("");              //0
        var num3 = Number("000011");        //11
        var num4 = Number(true);            //1
        
          var num1 = parseInt("1234blue");    //1234
        var num2 = parseInt("");            //NaN
        var num3 = parseInt("0xA");         //10 - hexadecimal
        var num4 = parseInt(22.5);          //22
        var num5 = parseInt("70");          //70 - decimal
        var num6 = parseInt("0xf");         //15 ?hexadecimal
        var num1 = parseInt("AF", 16);        //175
        var num2 = parseInt("AF");            //NaN
  		 var num1 = parseInt("10", 2);         //2 ?parsed as binary
        var num2 = parseInt("10", 8);         //8 ?parsed as octal
        var num3 = parseInt("10", 10);        //10 ?parsed as decimal
        var num4 = parseInt("10", 16);        //16 ?parsed as hexadecimal
        
        var num1 = parseFloat("1234blue");    //1234 - integer
        var num2 = parseFloat("0xA");         //0
        var num3 = parseFloat("22.5");        //22.5
        var num4 = parseFloat("22.34.5");     //22.34
        var num5 = parseFloat("0908.5");      //908.5
        var num6 = parseFloat("3.125e7");     //31250000
        
```

5.按位非操作(~)，底层操作，更快。ECMAScript执行64—32—64的方式。

```javascript
        var num1 = 25;             //binary 00000000000000000000000000011001
        var num2 = ~num1;          //binary 11111111111111111111111111100110
        alert(num2);               //-26
```

6.按位与（&）同上(同为1才是1)

```javascript
        var result = 25 & 3;
        alert(result);    //outputs 1
        /*25 = 0000 0000 0000 0000 0000 0000 0001 1001
           3 = 0000 0000 0000 0000 0000 0000 0000 0011
       25&3  = 0000 0000 0000 0000 0000 0000 0000 0001    
           */
```

7.按异位（^）只有对应位数各不相同才为1. 

```javascript
        var result = 25 ^ 3;
        alert(result);    //26
  /*25 = 0000 0000 0000 0000 0000 0000 0001 1001
     3 = 0000 0000 0000 0000 0000 0000 0000 0011
 25^3  = 0000 0000 0000 0000 0000 0000 0001 1010    
           */
```

8.按位或（|）有一个为1则为1.

9.左移（<<）右移（>>）

```javascript
 var oldValue = 2;             //equal to binary 10
        var newValue = oldValue << 5; //equal to binary 1000000 which is decimal 64
        alert(newValue);              //64
        //有符号右移，负数右移和正数同
        var oldValue = 64;               //equal to binary 1000000
        var newValue = oldValue >> 5;    //equal to binary 10 which is decimal 2
        alert(newValue);                 //2

        //对于无符号右移，正数同>>负数则：
           var oldValue = -64;              //equal to binary 11111111111111111111111111000000
        var newValue = oldValue >>> 5;   //equal to decimal 134217726
        alert(newValue);                 //134217726

        
```

10.对于加法，要注意。

```javascript
var num1 = 5;
        var num2 = 10;
        var message = "The sum of 5 and 10 is " + num1 + num2;
        alert(message);    //"The sum of 5 and 10 is 510"
        //字符+数字是将数字转化为字符相加
          var num1 = 5;
        var num2 = 10;
        var message = "The sum of 5 and 10 is " + (num1 + num2);
        alert(message);    //"The sum of 5 and 10 is 15"

```

11.for-in.

```javascript
for(property in expression) statement;

//例如：
for(var propName in windows){
    document.write(propName);
```

12.lable和break联用。

```javascript
        outermost:
        for (var i=0; i < 10; i++) {
             for (var j=0; j < 10; j++) {
                if (i == 5 && j == 5) {
                    break outermost;
                }
                num++;
            }
        }
        
        alert(num);    //55

```

13.关于函数

多个同名函数不会报错。但是最后一个出现的函数会覆盖之前的。

```javascript
   function doAdd() {
            if(arguments.length == 1) {
                alert(arguments[0] + 10);
            } else if (arguments.length == 2) {
                alert(arguments[0] + arguments[1]);
            }
        }
        
        doAdd(10);        //20
        doAdd(30, 20);    //50
//原型函数可以不写参数名，JS会用argument数组记录输入数据。
 function doAdd(num1, num2) {
            if(arguments.length == 1) {
                alert(num1 + 10);
            } else if (arguments.length == 2) {
                alert(arguments[0] + num2);
            }
        }

        
        doAdd(10);        //20
        doAdd(30, 20);    //50
        //argument数组和对应1元素同等且有联动，改变一个会都改。
```



14.关于变量的传递、内存问题。

创造对象类似于C语言中malloc

```javascript
  var person = new Object();
        person.name = "Nicholas";
        alert(person.name);    //"Nicholas"
        //只有对象能被添加属性
             var name = "Nicholas";
        name.age = 27;
        alert(name.age);    //undefined
        //name无法被加上age属性
```

对于对象的相互赋值，类似于指针。

```javascript
var obj1 = new Object();
var obj2 = obj1;
obj1.name = "haha";
alert(obj2.name);// "haha"
```

对于普通变量，参数传递是传真，对object是地址。

```javascript
 function addTen(num) {
            num += 10;
            return num;
        }
        
        var count = 20
        var result = addTen(count);
        alert(count);    //20
        alert(result);   //10
        
         function setName(obj) {
            obj.name = "Nicholas";
             obj = new object();//这里又申请了块内存，obj换了指向。局部变量。
             obj.name = "haha";
        }
        
        var person = new Object();
        setName(person);
        alert(person.name);    //"Nicholas"
```

0-P72