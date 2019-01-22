**原型的动态性**

```javascript
      function Person(){
        }
        
        Person.prototype = {
            constructor: Person,
            name : "Nicholas",
            age : 29,
            job : "Software Engineer",
            sayName : function () {
                alert(this.name);
            }
        };
        
        var friend = new Person();
        //即使先创建实例，原型的修改还是会在实例奏效
        Person.prototype.sayHi = function(){
            alert("hi");
        };
        
        friend.sayHi();   //"hi" ?works!
        //但重写原型则会失效
            function Person(){
        }
        
        var friend = new Person();
                
        Person.prototype = {
            constructor: Person,
            name : "Nicholas",
            age : 29,
            job : "Software Engineer",
            sayName : function () {
                alert(this.name);
            }
        };
        
        friend.sayName();   //error

```

**原生对象的原型，最好别动**

```javascript
//列如可以在，array中找到
array.prototype.sort();
//也可以给原生对象写新方法
 alert(typeof Array.prototype.sort);         //"function"
        alert(typeof String.prototype.substring);   //"function"

        String.prototype.startsWith = function (text) {
            return this.indexOf(text) == 0;
        };
        
        var msg = "Hello world!";
        alert(msg.startsWith("Hello"));   //true
        
```

**原型对象的问题**

```javascript
//对于函数、有基本值的属性来说适合，但对于包含引用类型属性不适合
    function Person(){
        }
        
        Person.prototype = {
            constructor: Person,
            name : "Nicholas",
            age : 29,
            job : "Software Engineer",
            friends : ["Shelby", "Court"],
            sayName : function () {
                alert(this.name);
            }
        };
        
        var person1 = new Person();
        var person2 = new Person();
        
        person1.friends.push("Van");
        
        alert(person1.friends);    //"Shelby,Court,Van"
        alert(person2.friends);    //"Shelby,Court,Van"
        alert(person1.friends === person2.friends);  //true

```

**解决方法**

1.组合使用构造函数和原型模式

```javascript
  function Person(name, age, job){
            this.name = name;
            this.age = age;
            this.job = job;
            this.friends = ["Shelby", "Court"];
        }
        
        Person.prototype = {
            constructor: Person,
            sayName : function () {
                alert(this.name);
            }
        };
        
        var person1 = new Person("Nicholas", 29, "Software Engineer");
        var person2 = new Person("Greg", 27, "Doctor");
        
        person1.friends.push("Van");
        
        alert(person1.friends);    //"Shelby,Court,Van"
        alert(person2.friends);    //"Shelby,Court"
        alert(person1.friends === person2.friends);  //false
        alert(person1.sayName === person2.sayName);  //true
```

2.动态原型模式

```javascript
/*把所有信息封装在构造函数。通过检查某个应该存在的方法是否奏效，来决定是否需要初始化原型*/

  function Person(name, age, job){
        
            //properties
            this.name = name;
            this.age = age;
            this.job = job;
            
            //methods
            if (typeof this.sayName != "function"){
            
                Person.prototype.sayName = function(){
                    alert(this.name);
                };
                
            }
        }

        var friend = new Person("Nicholas", 29, "Software Engineer");
        friend.sayName();


```

//.....以后补，无法完全理解