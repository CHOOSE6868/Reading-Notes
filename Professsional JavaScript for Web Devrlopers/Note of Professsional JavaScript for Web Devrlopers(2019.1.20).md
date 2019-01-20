**1.检测类型可以用typeof 和 instanceof**

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
        //不管是那个环境创建的数组都可以用
        Array.isArray(Array's name)来确定。返回值是布尔
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

