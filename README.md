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
  * **I believe DOM is a swming pool and element is coin. so it's not good to dive in swming pool to find the coin**

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

##  Privacy 
 we can achieve privacy by using closer.
```JS
var Person = (function() {
let privateData = new WeakMap();
   class Person {
     constructor(fname,lname){
          privateData.set(this, { fname: fname, lname:lname });
       }
  fullName(){
   return privateData.get(this).fname + " " +privateData.get(this).fname;
  }
 }
   return Person;
}());
let emp = new Person("John","doe");
console.log(emp.fullName());
```

## JavaScript Immutable
> **Note:**  It works only in **'use strict'** mode
```
const object1 = {
  property1: 42
};
Object.freeze(object1);
object1.property1 = 33;
// Throws an error in strict mode
console.log(object1.property1);
// expected output: 42
```


##  this in JavaScript
 1. **this** determined only when a function is called
 2. in each funciton is called in an executional context and it's pointed by this keyboard
 3. if functin is callded directly then, this points to window object **Note:** in strict mode this point to undefined instead of window.
ex:-
```
function foo(){
var name ="foo";
baz();
}
function baz(){
 console.log(this.name);
}
var name ="window"
foo();
```
> output : window # because 
> foo.call(obj); or foo.app(obj)//calls the foo function on "obj" object in another words obj is 'this' in foo funciton.
>call and apply both are same, the only diff is way of passing argument
>food.bind(obj) //bind the foo funciton to obj ie keyboard this would be obj inside food function.
## new 
```
 var add =  new food(){
     var this = {}; //automatically an object is created and assigned to this ;
	 ... expression 1...
	 ...  expression n...
	 return this; //At the end of this keyboard is returned;
 }
 ```
> so add =this; //at the end of function called with new keyboard
###  keyboard new has higher precedance then explicit binding ie
  new fn.call(obj) > fn.call(obj) >  global

## JavaScript Design Patter
 1. **Callback** : In this, we give control to call a function to another function/API.  callback is a kind of inverse of control means we are giving control to someone else to call our function
 1.  **IIFE** (immediately invocable function expression), example JQuery
 ```
 let calculator = (function($){
      let element = document.getElementById("calResult");
	  document.addEventListener("click", funciton(event){
	    let target = event.target;
		if(target.match("=")){
		    eval();
		}
		if(target.match("calResult")){
		    return;
		}
		  add(target);
	  });
	  let memory =[];
	  let calc={};
	  calc.add = funciton(value){
	       element.innherHtml = elment.innnerHtml+value;
	  };
	  calc.eval : funciton(){
         element.innherHtml = evel(elment.innnerHtml)
      };
	  return calc;
	  
})(jQuery);

```
1.  module, ex require


## import export modules
```
// module "my-module.js"
function cube(x) {
  return x * x * x;
}
const foo = Math.PI + Math.SQRT2;
var graph = {
    options:{
        color:'white',
        thickness:'2px'
    },
    draw: function(){
        console.log('From graph draw function');
    }
}
export { cube, foo, graph };

// use the module in diff file
import { cube, foo, graph } from 'my-module';
graph.options = {
    color:'blue',
    thickness:'3px'
}; 
graph.draw();
console.log(cube(3)); // 27
console.log(foo); 

// using default export ("my-module.js")
export default function cube(x) {
  return x * x * x;
}

import Cube from 'my-module'; // here cube is assigned to Cube it happens in case of default export
console.log(cube(3)); // 27
```

 
# AND THE REAL STORY BEGINS NOW
## Advance JavaScirpt
*  Javascript execute the code in two pass
    1. Hoisting (variable and function hoisting)
    1. Parse and run
 

### JavaScirpt Hoisting
 *  JavaScript shift the all variable and function declaration, declared by "var" keyboard at the top  of it's scope is called hoisting 
 *  Remember variables  declared by let keyboard are not hoisted
 *  function or variable are overridden if we declare them again
 * >Example
```
(function(){
g();
  function g(){
    console.log("g");
    f();
  }
var  f = function(){
      console.log("first");
    };
})();
#after hoisting
(function(){
  function g(){  //function comes first in hoisting
    console.log("g");
    f();
  }
  var f; // after function variables are declared
g();
f = function(){
      console.log("first");
    };
})();
#output : -f is not a funciton
```
## JavaScript has two scope  
1) functional and
2) block.

* JavaScript first find the variable in local scope if not find then go to immediate upper label and so on and if still not find then
    1.  (in not strict mode )it declare at top most label (window) and assign a value undefined ie var name =undefined;
    2. (in strict mode)  if variable is not found then it gives error like undeclared
*  undefined means when we declare a variable but not assign any value. 
* undeclared means we have even not declared any **var** and trying to use it.
* ECMA6 has indroduce a **'let'** keyboard to declare block label variable which is not hoisted
## Function declaration and function expression
*  if 'function' is the first keyboard in statement then it's function declaration; ex. funciton myFn(){};
* rest is 'function expression' ex var fun = function myFn(){};
* Use function declaration over function expression to take advantage of hoisting
 ## Never ever use it ?? bad cause
```
function myFunc(str){
var a =12;
eval(str);
console.log(a) //output 20
}
myFunc("var a=20;");
```

## Dynamic scoping
```
funciton foo(){
 console.log(this.str); //print "dynamic scope"
}
var obj1 = {str:"obj1"}
var obj2 = {str:"obj2"}
foo(obj1); //obj1
foo(obj2); //obj2
```

## Closer
When we define a function inside another function and expose it, the inner function will have access to the variables/function of  outer function scope, even after the outer function has finished.

 * Lexical scoping : function find some variable inside it then it use it otherwise it find the variable at it's immediate parent function and so on... is called lexical or compile time scoping.
**Closer : when a function use lexical scope to resolves it's variable/function scope is called closer**

## JavaScirpt Fucntion and Object Relations 
*  JavaScript is actually an object oriented language
*  Java is not object oriented actually it's class oriented.
* In JS everything is object, even function and it is linked to an anonymous object by **\_\_proto\_\_** prototype property.
* each function has a hidden property named **prototype** that is linked to an anonymous object.
* Each object has a hidden property named **\_\_proto\_\_** that is linked to an anonymous object
* When we create an object by **new funciton()** then in that case function's **prototype** property and object's **\_\_proto__** property points to same anonymous object
* the anonymous object has a property called **constructor** that points to function
ie
```
then Foo.prototype  = ao;
and ao.constructor = Foo;
var obj = new Foo();
obj.__proto__ == ao
```
* JavaScript has a build in function named 'Function()' that also point to an anonymous obj (say aof) (having call apply, bind funciton)

* In JavaScript, each function is an object so it also has constructor property.
```
Foo.constructor = Function
Foo.__proto__ =  aof
```
* Dont say or never say JavaScirpt has inharitance because inharitance means one object copy the something from other obj.
* JavaScirpt have prototypical inharitance means one object does not copy anything from another obj, it just links them called
**OLOO : object linked to other object**
## Object inharitance machenics;
```
var obj1 ={
  add: add(a,b){};
  del: del(){}
}
var obj2  =  Object.create(obj1); //create an obj2 whose prototype is obj ie obj2__proto__ = obj
obj.add();
```
**another way**
```
function Foo(){...}
funciion Bar(){ Foo.appply(this).....}
Bar.prototype =Object.create(Foo.prototype); 
//or 
Bar.prototype =new Foo(); 
```
 
##  ECMA6 new feature like Promise,  Generator -yield, async-await function.
```
function resolveAfter2Seconds() {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve('resolved');
    }, 2000);
  });
}
async function asyncCall() {
  console.log('calling');
  //**await can only be used inside async function**
  var result = await resolveAfter2Seconds();
  console.log(result);
  return "async done";
}
asyncCall().then(function(val){
console.log(val);
});
```
## Generator function example
```
function* idMaker() {
  var index = 0;
  while (index < 3)
    yield index++;
}
var gen = idMaker();
console.log(gen.next().value); // 0
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // undefined
```
 
 [JS-Interview-QA]: <https://www.toptal.com/javascript/interview-questions>
 [stackedit]: <https://stackedit.io/app#>