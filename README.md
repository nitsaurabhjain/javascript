# JavaScript
 [JS-Interview-QA] - JavaScript Interview question answer
 ## JavaScript data type
 ### Primitive
 | Data Type | Description |
| ------ | ------ |
| String | represents sequence of characters e.g. "hello" |
|Number| represents numeric values e.g. 100|
|Boolean|represents boolean value either false or true|
|Undefined |	represents undefined value|
|Null |	represents null i.e. no value at all|
### User defined  -  Object is only user defined data type 
  * In JS everythig is Object including function, eccept primitive data type

 **Class like function with respect to primitive data type**
*  Number ("string") coverts string into number, if not convertable then return NaN
* String(1212) : converts number into string ie "1212"
* String has many useful function like charAt, IndexOf, split, slice, toUpperCase, toLowerCase
*  falsey values (false, null,undefined, NaN, 0, "") returns false
*  truthy value (not a falsey value ex true "abcd", "false", "null" "NaN", "0") returns true
* !! always returns either true/false ex !!undefined returns false
* NaN is not equal to anything including NaN.
**examples**

```JS code
NaN == NaN  -> false
```

*  == performs type conversion
*  === does not perform type conversion
* It has all the airthamatic, logical operator, and comparision operator like other languages.
* It also has bitwise operator like &,|,^, >>, << but useless,
* because it covert floating point number into integer and apply operator (>> multiply by 2) and convert back agian in 16 digit floating point number.
* it has all statment like java, if else, for , swith case, try catch while
* Object.hasOwnProperty('name');


## JavaScript Best Practice
* Avoid global variables whenever because 
  1. Name clash and one can change and another will be affected
  1. minimize the memory
* Use one global object and encapsulate all needed variables into that object
* Use var to define a variable otherwise it will be global
* use closer and object to minimize global variables
* Use the meaningful name so that other can understand the code easily
* Not to big and not to short (short and meaningful)
* Always always  add semi-column after each statement because 
  * JavaScript parser automatically adds forgotten semi-column and some time it may cause problem
```
return
      12; 
can be converted into 
return;
12;
instead of return 12;
```
* Always use curly braces in function at the same line to avoid automatically adding semi-column by js compiler
```
function f(){
////
}	 
because js parser may add a semi-column after function();
function()
{
///
}
could be be parsed as
function();
{
//
}
```

* Keep the ternary block isolated to maintain it's mutability
```
  var output = "the output is": +
     conditon? statement1: statement2 (wrong because + will contate string and condition and hence it will always evalute true)
var output = "the output is": +
     (conditon? statement1: statement2) (right)
```

* Minimize DOM usages whenever possible because it's expensive operation

## Some more point about JS
*  ==, !=  perform type convension
*  ===, !== to avoid type convension (identity operator)
* Use let ( from ECMA6 ) keyboard to declare variable instead of var keyboard because it allows us to declare block label variable
* if we create any variable without let or var then by default it is decared as global variable

## JavaScript functions
**JavaScript provides 4 below ways to define funciton**
 1. ananomious function ie (funciton(/*$, age*/){})(jQuery,10);
 1. lambda expression ie (a, b) => a+b;
 1. named function ie  var sum = function(a,b){retur a+b}
 1. constructor funciton ie new MyFunction();

 ##  ECMA5 introduce "use strict";
* "use strict"; can be used on function label or global label 
* in strict mode , variable can not be used until they are not defined.
* in strict mode object's property can't be deleted if they are not exist or not deletable like delete object.prototype
* in strict mode, keyboard or reserved keyboard can not be used as variable/function name 

## Object in JavaScript
*  4 ways to create object in javascript
    1. by new operator
    2. by Object literal let myObj = {};
    3. Object.create(prototypeObject,propertiesObject);
       * Object.create methods accepts two arguments.
          1. prototypeObject: Newly created object's prototype object. It can be an object or null. 
          2. propertiesObject: Properties of new object. This argument is optional
   Object.defineProperty(myObj, {
      name: { value : "Saudrabh",
              writable: false
            },
      skill:{
        value: [Java, JS],
        writable: flase
       }
});

    4. Using ES6 class syntax: 
    ```JS
      class myObject  {
        constructor(name) {
          this.name = name;
        }
      }   
      var e = new myObject("hello");
    ```


## Prototype or prototypical inharitance in Javascript
```JS
funciton PersonFactory(fname, lname){
  return {
    "firstname":fname,
	"lastName" : lname,
	"greet": funciton(){
	  return "Hello"+firstname+" "+ lastName;
	} //greet
  }; //return
} //PersonFactory
let person1  = PersonFactory("persoon1","Deo");
let person2  = PersonFactory("persoon2","Smit");
```
 **Heere there is is big problem of greet funciton, each object has it's own greet function that can consume lots of memory**
 * To avoid it we can use prototypical inharitance
 * Each function/object has a inbuild property : prototype/__proto__ that points to either any other object or null
```
let obj1 = {greet:funciton(){return "Hello Mr." + name}}
let obje2 {name: saurabh,__proto__:obj1} 
or obj2.__proto__ = obj1;
obj2.greet();
```
### In case of functional constructor programming 
```
Person(fname,lname) {}
Employe {
Person.call(this,fname,lname);
}
Employe.prototype =new Person();
```
* call calls the function in context of pirst argument and subsequent argument are passed in function 
* apply calls the funciton in context of first argument and second argument is an array that is passed to functions subsequent arg
function sayHello(){return this.name;}
* Use .bind() when you want that function to later be called with a certain contex
```
sayHello()// will throw error since wont fine this.sayhello;
obj {name:"John"}
sayHello.call(obj);or sayHello.apply(obj)
```

## ECMA6 or ECMA 2015
 * Class: Can say a constructor function
```
 class Vehicle {
   constructor (name, type) {
    this.name = name;
    this.type = type;
  }
   getName () {
    return this.name;
  }
   getType () {
    return this.type;
  }
 }
 ```
**ES5 equivalent could be something like this**
```
function Vehicle (name, type) {
  this.name = name;
  this.type = type;
};
 Vehicle.prototype.getName = function getName () {
  return this.name;
};
Vehicle.prototype.getType = function getType () {
  return this.type;
};
```
**Basically when we create an object of Vehical class**
  * It create a constructor function 
  * And add getName and getType method in function's prototype;
  * it can have static data also, It wont be a part of object
  
### inheritance
```
class Car extends Vehicle {
   constructor (name) {
    super(name, 'car');
  }
   getName () {
    return 'It is a car: ' + super.getName();
  }
 }
```
**ES5 equivalent could be something like this**
```
function Car (name) {
  Vehicle.call(this, name, ‘car’);
}
Car.prototype = Object.create(Vehicle.prototype);
Car.prototype.constructor = Car;
Car.parent = Vehicle.prototype;
Car.prototype.getName = function () {
  return 'It is a car: '+ this.name;
};
```

	
 [JS-Interview-QA]: <https://www.toptal.com/javascript/interview-questions>
