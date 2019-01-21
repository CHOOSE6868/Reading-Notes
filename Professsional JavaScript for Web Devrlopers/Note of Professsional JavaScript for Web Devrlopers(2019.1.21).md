**理解对象**

```javascript
//一种写法
var person = {
name:"ahah",
age99,
job:Software Engineer",
sayName :function(){
    alert(this.name);
};
/*es有两种属性，数据属性和访问器属性-P139.这些属性最好别动，Object.defineProperty(属性所在对象，属性名字，描述符)*/
/*访问器属性包含一对getter,setter函数，P141
*/
  var book = {
            _year: 2004,
            edition: 1
        };
          
        Object.defineProperty(book, "year", {
            get: function(){
                return this._year;
            },
            set: function(newValue){
            
                if (newValue > 2004) {
                    this._year = newValue;
                    this.edition += newValue - 2004;
                
                }
            }
        });
        
        book.year = 2005;
        alert(book.edition);   //2
       // “-”代表数据属性，不加则是访问器属性
       //用Object.defineProperties(对象，对应的要修改的属性)
       
        var book = {};
        
        Object.defineProperties(book, {
            _year: {
                value: 2004
            },
            
            edition: {
                value: 1
            },
            
            year: {            
                get: function(){
                    return this._year;
                },
                
                set: function(newValue){
                    if (newValue > 2004) {
                        this._year = newValue;
                        this.edition += newValue - 2004;
                    }                  
                }            
            }        
        });
           
        book.year = 2005;
        alert(book.edition);   //2
        /*object.getOwnPropertyDescriptor(属性所在对象，属性名字)
        返回一个对象，属性由原本对象属性决定。p143*/
             var book = {};
        
        Object.defineProperties(book, {
            _year: {
                value: 2004
            },
            
            edition: {
                value: 1
            },
            
            year: {            
                get: function(){
                    return this._year;
                },
                
                set: function(newValue){
                    if (newValue > 2004) {
                        this._year = newValue;
                        this.edition += newValue - 2004;
                    }                  
                }            
            }        
        });
           
        var descriptor = Object.getOwnPropertyDescriptor(book, "_year");
        alert(descriptor.value);          //2004
        alert(descriptor.configurable);   //false
        alert(typeof descriptor.get);     //"undefined"
        
        var descriptor = Object.getOwnPropertyDescriptor(book, "year");
        alert(descriptor.value);          //undefined
        alert(descriptor.enumerable);     //false
        alert(typeof descriptor.get);     //"function"

```

**创建对象**

```javascript
//方式
   function Person(name, age, job){
            this.name = name;
            this.age = age;
            this.job = job;
            this.sayName = function(){
                alert(this.name);
            };    
        }
/*等价
         function Person(name, age, job){
            this.name = name;
            this.age = age;
            this.job = job;
            this.sayName = sayName;
               
        }
        function sayName(){
        alert(this.name);
        }*/
        var person1 = new Person("Nicholas", 29, "Software Engineer");
        var person2 = new Person("Greg", 27, "Doctor");
        
        person1.sayName();   //"Nicholas"
        person2.sayName();   //"Greg"
        
        alert(person1 instanceof Object);  //true
        alert(person1 instanceof Person);  //true
        alert(person2 instanceof Object);  //true
        alert(person2 instanceof Person);  //true
        //constructor属性指向原型Person
        alert(person1.constructor == Person);  //true
        alert(person2.constructor == Person);  //true
        
        alert(person1.sayName == person2.sayName);  //false    //person()函数使用方式
       function Person(name, age, job){
            this.name = name;
            this.age = age;
            this.job = job;
            this.sayName = function(){
                alert(this.name);
            };
        }
        
        var person = new Person("Nicholas", 29, "Software Engineer");
        person.sayName();   //"Nicholas"。当构造函数
        
        Person("Greg", 27, "Doctor");  //adds to window
        window.sayName();   //"Greg"。普通函数
        
        var o = new Object();//在另一个对象的作用域调用
        Person.call(o, "Kristen", 25, "Nurse");//call()传递参数，扩大作用域
        o.sayName();    //"Kristen"  
```

**原型模式构建**P148

```javascript
     function Person(){
        }
        
        Person.prototype.name = "Nicholas";
        Person.prototype.age = 29;
        Person.prototype.job = "Software Engineer";
        Person.prototype.sayName = function(){
            alert(this.name);
        };
        
        var person1 = new Person();
        person1.sayName();   //"Nicholas"
        
        var person2 = new Person();
        person2.sayName();   //"Nicholas"
      
        alert(person1.sayName == person2.sayName);  //true
        
        alert(Person.prototype.isPrototypeOf(person1));  //true
        alert(Person.prototype.isPrototypeOf(person2));  //true
        
        //only works if Object.getPrototypeOf() is available
        if (Object.getPrototypeOf){
            alert(Object.getPrototypeOf(person1) == Person.prototype);  //true
            alert(Object.getPrototypeOf(person1).name);  //"Nicholas"
        }
```

实例中创建属性会覆盖原型

```javascript
      function Person(){
        }
        
        Person.prototype.name = "Nicholas";
        Person.prototype.age = 29;
        Person.prototype.job = "Software Engineer";
        Person.prototype.sayName = function(){
            alert(this.name);
        };
        
        var person1 = new Person();
        var person2 = new Person();
        
        person1.name = "Greg";
        alert(person1.name);   //"Greg" ?from instance
        alert(person2.name);   //"Nicholas" ?from prototype
//delete实例中属性，即可继续访问原型
           function Person(){
        }
        
        Person.prototype.name = "Nicholas";
        Person.prototype.age = 29;
        Person.prototype.job = "Software Engineer";
        Person.prototype.sayName = function(){
            alert(this.name);
        };
        
        var person1 = new Person();
        var person2 = new Person();
        
        person1.name = "Greg";
        alert(person1.name);   //"Greg" ?from instance
        alert(person2.name);   //"Nicholas" ?from prototype
        
        delete person1.name;
        alert(person1.name);   //"Nicholas" - from the prototype

```

//利用hasOwnProperty()和In确定该对象是在原型还是实列中

```javascript
       function hasPrototypeProperty(object, name){
            return !object.hasOwnProperty(name) && (name in object);
        }
            
        function Person(){
        }
        
        Person.prototype.name = "Nicholas";
        Person.prototype.age = 29;
        Person.prototype.job = "Software Engineer";
        Person.prototype.sayName = function(){
            alert(this.name);
        };
        
        var person = new Person();        
        alert(hasPrototypeProperty(person, "name"));  //true
        
        person.name = "Greg";
        alert(hasPrototypeProperty(person, "name"));  //false        
```

//es5中Object.keys（）接收一个对象，返回包含可枚举类型的字符数组

```javascript
      function Person(){
        }
        
        Person.prototype.name = "Nicholas";
        Person.prototype.age = 29;
        Person.prototype.job = "Software Engineer";
        Person.prototype.sayName = function(){
            alert(this.name);
        };
        
        var keys = Object.keys(Person.prototype);
        alert(keys);   //"name,age,job,sayName"
        //不论是否可枚举，可以用objcet.getOwnPropertyName()得到
       function Person(){
        }
        
        Person.prototype.name = "Nicholas";
        Person.prototype.age = 29;
        Person.prototype.job = "Software Engineer";
        Person.prototype.sayName = function(){
            alert(this.name);
        };
        
        var keys = Object.getOwnPropertyNames(Person.prototype);
        alert(keys);   //"constructor,name,age,job,sayName"
        
```

更简单的原型语法

```javascript
       function Person(){
        }
        
        Person.prototype = {
            name : "Nicholas",
            age : 29,
            job: "Software Engineer",
            sayName : function () {
                alert(this.name);
            }
        };

        var friend = new Person();
        
        alert(friend instanceof Object);  //true
        alert(friend instanceof Person);  //true
        alert(friend.constructor == Person);  //false，constructor无法确定类型了
        alert(friend.constructor == Object);  //true
        //constructor，P155
            
        Person.prototype = {
            constructor : Person,
            name : "Nicholas",
            age : 29,
            job: "Software Engineer",
            sayName : function () {
                alert(this.name);
            }
        };

        var friend = new Person();
        
        alert(friend instanceof Object);  //true
        alert(friend instanceof Person);  //true
        alert(friend.constructor == Person);  //true
        alert(friend.constructor == Object);  //false
```

