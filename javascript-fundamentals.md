
# Javascript

## Language Features
### const  
should be initialized with a value
### let
is block scope  
error if used before defined

### var     
is not block scope  
got undefined value before initialized

### rest params
joins all last params as an array  
rest parameter should be last param in a function

```javascript
function myfunction(...restparams) {}
  
myfunction(param1,param2,param3)
  
function myfunction('hello',...restparams) {}
  
myfunction(word,param1,param2,param3)
```

### destructuring arrays
```javascript
let carIds = [1,2,5]
let [car1,car2,car3] = carIds;
console.log(car1,car2,car3);
// 1 2 5
```
```javascript
let carIds = [1,2,5]
let [car1, remainingCars] = carIds;
console.log(car1,remainingCars);
// 1 [2,  5]
```
```javascript
let carIds = [1,2,5]
//skip first element (could skip any number of elements)
let [, remainingCars] = carIds;
console.log(remainingCars);
// [2,  5]
```

### desctructuring objects
```javascript
let car = {id:5000, style: 'convertible'}
let {id, style} = car;
console.log(id, style);
// 50000 convertible
```
```javascript
let car = {id:5000, style: 'convertible'}
let id, style;
{id, style} = car;
// error
```
```javascript
let car = {id:5000, style: 'convertible'}
let id, style;
({id, style} = car);
// 50000 convertible
``` 

### spread syntax
spread variable in all values  :
```javascript
function myfunction(param1,param2,param3) {}
  
let myparams = [1,2,3];
myfunction(...myparams);
// 1, 2, 3
```

also for strings...
```javascript
function myfunction(param1,param2,param3) {}
  
let myparams = '123';
myfunction(...myparams);
// 1, 2, 3
```

combining with rest params...
```javascript
function myfunction(param1,param2,param3,...params) {}
  
let myparams = '12345678';
myfunction(...myparams);
// 1, 2, 3, [4,5,6,7,8]
```

### typeof()    

type | result 
 --- | ---
typeof(1) | number  
typeof(true) | boolean
typeof('Hello') | string
typeof(function(){}) | function  
typeof({}) | object 
typeof(null) | object 
typeof(undefined) | undefined  
typeof(NaN) | number

### common type convertions
foo.toString();  
Number.parseInt('55');  //55 as a number  
Number.parseFloat('55.99');  //55.99 as a number
Number.parseInt('55asdasd');  //55 as a number, ignores chars after last number
  
### loops
let i=0;
```javascript  
for(;i<12;i++){
    if(i ===2)
        continue;
    console.log(i);
}
// 0 1 3
```

## Operators

### Equality
```
== equal value
== equal value and type
!=
!==
```

### Unary
```
++var1      //increment before use
var1++      //increment after use 
--var1      //decrement before use
var1--      //decrement after use 
+var1       //convert string into numeric 
             (do not change negative string to positive)
-var1       //change numeric value sign
```

### Logical
```
&&  and   (has precedence over logical ||)
||  or
```

outside of a conditional...

```
var1 && var2    //results on var2 if both ar truthy
var1 || var2    //results on var 1 if is defined, if not var2
!var1
```

### Relational

```
>   <   >=  <=
// uppercase letters come first that lowercase
```

### Conditional
```javascript
expression ? 'if yes': 'if no';
```

### Assignment

```
+=
-+
/=
*=
%=
<<=     //bits shift
>>=     //bits shift
>>>=    //bits shift keeping the sign     
```

shift example:
```javascript
let var1 = '12';
var1 >>=1;
console.log(var1);
6
```
    
# Functions and scope

### Function Scope
```javascript
function startCar(carId){
    let message = 'Starting...';
}
startCar(123);
console.log(mesage) //Error
```

```javascript
function startCar(carId){
    let message = 'Starting...';
    let startFn =  function turnKey(){
        console.log(message);    // 'Starting'
    }
    startFn();
}
startCar(123);
```
 
```javascript
function startCar(carId){
    let message = 'Starting...';
    let startFn =  function turnKey(){
        let message = 'Override...';
    }
    startFn();
    console.log(message);    // 'Starting'
}
startCar(123);
```

### Block Scope

```javascript
if(5===5){
    let message = 'Equal';
}
console.log(mesage) //error
```

```javascript
let message = 'Outside';
if(5===5){
    let message = 'Equal';
    console.log(mesage) //Equal
}
console.log(mesage) //Outside
```

```javascript
let message = 'Outside';
if(5===5){
    message = 'Equal';
    console.log(mesage) //Equal
}
console.log(mesage) //Equal
```

```javascript
var message = 'Outside';
if(5===5){
    var message = 'Equal';
    console.log(mesage) //Equal
}
console.log(mesage) //Equal
```

### IIFE Immediatly Invoked Function Expression
```javascript
(function(){
    console.log('in function');
})();
```

```javascript
let app = (function(){
    let carId = 123;
    console.log('in function');
    return {};
})();
```

### Closures
When a function executes it goes trough all its code and then completes.  
All of its variables and functions go out of scope  
  
A closure allows some functions and variables to hang around.
```javascript
let app = (function(){
    let carId = 123;
    let getId = function(){
        return carId;
    }
    return {
        getId: getId     //this is the closure
    };
})();
console.log(app.getId());
```

### this keyword
```javascript
let fn = funtion() {
    console.log(this === window);
}
fn();   //true
```
```javascript
let o = {
    carId: 123,
    getId: function(){
        return this.carID;
    }
}
console.log(o.getId());     //123
```

### call and apply
The main ourpose of this functions is to change the value of this  
(Change the object which is the context of the function)
  
call:
```javascript
let o = {
    carId: 123,
    getId: function(){
        return this.carID;
    }
}
let newCar = {carId: 456};
console.log(o.getId.call(newCar));     //456
```
apply (accept an array of arguments to be passed the function):
```javascript
let o = {
    carId: 123,
    getId: function(prefix){
        return prefix + this.carID;
    }
}
let newCar = {carId: 456};
console.log(o.getId.apply(newCar,['ID: ']));     //ID: 456
```

### bind
Makes a copy of a function and assigns new context
```javascript
let o = {
    carId: 123,
    getId: function(){
        return this.carId
    }
}
let newCar = {carId: 456};
let newFn = o.getId.bind(newCar);  
console.log(newFn());     //456
```

### Arrow functions
no params + only return value
```javascript
let getId = () => 123;  
//or
let getId = _ => 123;  
console.log(getId());   //123
```
one param + only return value
```javascript
let getId = prefix => prefix + 123;  
console.log(getId('ID: '));   // ID: 123
```
many params + only return value
```javascript
let getId = (prefix,suffix) => prefix + 123 + suffix;  
console.log(getId('ID: ','!'));   // ID: 123!
```

many params + function body   //return keyword required
```javascript
let getId = (prefix,suffix) => {
    return prefix + 123 + suffix;
}  
console.log( getId('ID: ','!'));   // ID: 123!
```

### Default parameters
Default params should be at the end.  
With variables interpolation:
```javascript
let trackCar = function(carId, city='NY'){
    console.log(`Tracking ${carId} in ${city}.`);
}

console.log(trackCar(123));
// Tracking 123 in NY.
console.log(trackCar(123, 'Chicago'));
// Tracking 123 in Chicago.
```

## Objects and Arrays

### Constructor functions
Use to instantiate new objects  
Capitalize for convention
```javascript
function Car(id){
    this.carId = id;
}
let car = new Car(123);
console.log(car.carId);     // 123
```
In a constructor function the first "this" is a new empty object  
So the properties and methods are attached to "this"  
```javascript
function Car(id){
    this.carId = id;
    this.start =  function(){
        console.log('start: '+ this.carId);
    }
}
let car = new Car(123);
console.log(car.carId);     // start: 123
```
### Prototypes
In this example...
```javascript
function Car(id){
    this.carId = id;
    this.start =  function(){
        console.log('start: '+ this.carId);
    }
}
let car = new Car(123);
console.log(car.carId);     // start: 123
```
if we create too many Car objects the start 
function will be replicated the same times  
There is only needed 1 function
```javascript
function Car(id){
    this.carId = id;
}
Car.prototype.start =  function(){
    console.log('start: '+ this.carId);
}
let car = new Car(123);
console.log(car.carId);     // start: 123
```

### Expand Objects Using Prototypes
```javascript
String.prototype.hello = function(){
    return this.toString() + ' Hello';
}

console.log('foo'.hello());     // foo Hello
```
### JSON
Used to send javascript object via web (http)

```javascript
let car= {
    id: 123,
    style: 'convertible'
}
console.log(JSON.stringify(car));
// {"id":123,"style":"convertible"}
``` 
### Array iteration
forEach  
```javascript
let carIds = [
  { carId: 123, style: 'sedan'},
  { carId: 456, style: 'convertible'},
  { carId: 789, style: 'sedan'}
];

carIds.forEach(car => console.log(car));

carIds.forEach((car, index)=> console.log(car,index));
```
filter
```javascript
let carIds = [
  { carId: 123, style: 'sedan'},
  { carId: 456, style: 'convertible'},
  { carId: 789, style: 'sedan'}
];
let convertibles = carIds.filter(
  car => car.style === 'convertible'
);
console.log(convertibles);
```
every
```javascript
let carIds = [
  { carId: 123, style: 'sedan'},
  { carId: 456, style: 'convertible'},
  { carId: 789, style: 'sedan'}
];
let result = carIds.every(
  car => car.carId > 0
);
console.log(result);
```
find
```javascript
let carIds = [
  { carId: 123, style: 'sedan'},
  { carId: 456, style: 'convertible'},
  { carId: 789, style: 'sedan'}
];
let result = carIds.find(
  car => car.carId > 500
);
console.log(result);
```
## Classes and Modules

### Class Basics
```javascript
class Car {

}
let car = new Car();
console.log(car);
```
### Constructors and Properties
When working with constructors "this" keyword is required to access properties
```javascript
class Car {
    constructor(id){
        this.id = id;
    }
}
let car = new Car(123);
console.log(car.id);    123
car.id = 456;
console.log(car.id);    456
```
### Methods
```javascript
class Car {
  constructor(id){
    this.id = id;
  }
  identify() {
    return `Car id: ${this.id}`;
  }
}
let car = new Car(123);
console.log(car.identify());    //Car id: 123
```
### Inheritance
```javascript
class Vehicle{
  constructor(){
    this.type = 'car';
  }
  start() {
    return `Starting ${this.type}`;
  }
}
class Car extends Vehicle {
}
let car = new Car();
console.log(car.type);    // car
console.log(car.start());    // Starting car
```
If a derived class requires a constructor..
```javascript
class Vehicle{
  constructor(){
    this.type = 'car';
  }
  start() {
    return `Starting ${this.type}`;
  }
}
class Car extends Vehicle {
  constructor(){
    super();
  }
}
let car = new Car();
console.log(car.type);    // car
console.log(car.start());    // Starting car
```
Same class method definition in derived class
overrides the one in base class.  
Using super() can access to base class methods
```javascript
class Vehicle{
  constructor(){
    this.type = 'car';
  }
  start() {
    return `Starting ${this.type}`;
  }
}
class Car extends Vehicle {
  constructor(){
    super();
  }
  start() {
    return `new starting method`;
  }
}
let car = new Car();
console.log(car.type);    // car
console.log(car.start());    // new starting method
```
### Create Modules
"export"...
```javascript
export class Car {
  constructor(id){
    this.id = id;
  }
}
```
you can also export variable, function, etc...
  
### Importing modules
import { "identifier" } from "path/to/model"; 
```javascript
import { Car } from './models/car.js';

let car = new Car(123);
console.log(car.id);
```

## BOM and DOM
BOM - browser object model (url, get info of url)  
DOM - document object model (manipulate the actual web page)
  
### Window object  
is the global object in js    
you can access window from everywhere
properties | methods | events
--- | --- | --- 
document(dom) | alert() | (not common)
location | back() | 
console | confirm() |
innerHeight (browser window)||
innerWidth (browser window)||
pageXOffset (scrollbar) ||
pageYOffset (scrollbar)||  

year is assigned to global object
```javascript
year  = 1965;

console.log(window.year); //1965
```
when working with modules variables need to be declared
```javascript
import {Car } from './models/car';

year  = 1965;

console.log(window.year); // error (let required)
console.log(window.innerWidth); // still working (default property)
```
#### Timers
##### setTimeOut() 
//once
```javascript
let timeoutId = setTimeout(function(){
  console.log('1 second passed');
},1000);
//if need to cancel...
clearTimeout(timeoutId);
```
##### setInterval()   
//repeatedly
```javascript
let intervalId = setInterval(function(){
  console.log('1 second passed');
},1000);
//if need to cancel...
clearInterval(intervalId);
```
### Location object
Part of the BOM, to get information on the url the browser is pointing to

properties|methods|events
---|---|---
href|assign()|(not common)
hostname|reload()|
port||
pathname||
search||

```javascript
console.log(location.href);
//same as
console.log(document.location.href);
```
### Document

DOM
properties|methods|events
--- | --- | ---
body|createElement()|onload
forms|createEvent()|onclick
links|getElementById()|onkeypress
|getElementsByClassName()|

#### Select elements 

```javascript
document.getElementById('elementId');   //suppose to be unique
document.getElementsByClassName('className');  //HTMLCollection (array) 
document.getElementsByTagName('tagName');      //HTMLCollection (array)
```

#### Modify elements 

```javascript
let element = document.getElementById('elementId');
element.textContent = 'new text here';
element.setAttribute('name','nameValue');
element.classList.add('myClassName');
element.style.color = 'blue';
```
## Promises and error handling 

### Errors
If an erros is not handled execution stops
```javascript
let car =  newCar;
console.log('continuing...');
```
### Error handling using try and catch
Wrap with try and catch
```javascript
try {
  let car = newCar;
}
catch(error){
  console.log('error', error);
}
console.log('continuing...');
```
### Finally
finally block always executes
```javascript
try {
  let car = newCar;
}
catch(error){
  console.log('error', error);
}
finally {
  console.log('always executes');
}
```
### Developer defined errors
```javascript
try {
  throw new Error('my custom error'); 
}
catch(error){
  console.log('error', error);
}
finally {
  console.log('always executes');
}
```
### Create promise
Promise represent a value we don't have access to just yet
```javascript
let promise = new Promise(
  function(resolve, reject){
    setTimeout(resolve,1000,'someValue');
  }
);
// promise status after 1000 ms is resolved
// promise value after 1000 ms is someValue
```
Promise first argument is a function executed inmediatly the promise ys called  
### Settling a Promise
When we do get the value of a promise is refered to as "settling a promise"
```javascript
let promise = new Promise(
  function(resolve, reject){
    setTimeout(resolve,1000,'someValue');
  }
);
// in order to get the value of a promise we execute...
// takes 2 functions as arguments
promise.then(
  // first argument is executed when the promise gets fulfilled
  value => console.log('fulfilled: '+ value),
  // first argument is executed when the promise gets fulfilled
  error => console.log('rejected: '+ error)
);
```
## Data access using HTTP

### HTTP requests using xhr
"X"ml "H"ttp "R"equests
```javascript
let xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function(){
  if(this.readyState == 4 && this.status == 200){
    console.log(this.responseText);
  }
};
xhttp.open("GET", "https://jsonplaceholder.typicode.com/todos",true);
xhttp.send();
```
### Using jQuery
```javascript
import $ from 'jquery';

$.get("https://jsonplaceholder.typicode.com/todos",
  data => console.log('data: ', data)
);
```
But get method returns a promise, so let's handle it as a promise....
```javascript
import $ from 'jquery';

let promise = $.get("https://jsonplaceholder.typicode.com/todos");
promise.then(
  data => console.log('success: ',data),
  error=> console.log('error: ',error)
);
```
### Posting data
```javascript
import $ from 'jquery';

const post = {
  'title': 'foo',
  'body': 'bar',
  'userId': 1,
} ;
let promise = $.post(
  "https://jsonplaceholder.typicode.com/posts",
  post
);
promise.then(
  data => console.log('success: ',data),
  error=> console.log('error: ',error)
);
```