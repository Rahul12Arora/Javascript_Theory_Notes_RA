# Javascript_Theory_Notes
Javascript_Theory 140322

<h2>Scope & Var, let & const</h2>
A scope of a parameter is a certain region of a programm or its bound where it can be access or recognised

<h3>Scope types</h3>
1.) Global scope</br>
2.) Function Scope</br>
3.) Block Scope</br>

**var is block scoped but let & const are block scoped**

<h3>Shadowing</h3>

**Shadowing is when an inner variable is prioritized over an outer variable of the same name, when in use inside the inner variable's scope**

```
function test(){
    var a = "hello"
    let b = "goodbye"
    
    if(true){
        let a = "hi"    // Shadowing
        var b = "bye"   // Illegal shadowing
    }
}
```

<h3>Declaration</h3>

**let & const cannot be re declared in the same scope**
**var can be redeclared in the same scope**

**const cannot be declared without initialization, once initialized it cannot be re-initialized**



<h2>Hoisting</h2>

<h3>An execution context is created</h3>

** Variables & definitions are moved to the top during the creation phase beofre executing even a single line of code**

<h3>Creation Phase</h3>
<li>Creates a Global/Window Object</li>
    <ul>
    <li>It creates a memory heap for storing variables & function references</li>
    <li>It initializes memory variables as undefined & functions with their entire definition</li>
    </ul>
<li>Creates an Execution Phase</li>
    <ul>
        <li>Javascript code is executed line by line</li>
        <li>For Every function a new execution context is created</li>
    </ul>

```
Note - let and const are hoisted in script memory & they are in temporal dead zone until they are initialized.
Temporal dead zone is the time between declaration and initialization of a variable
```

<h3>Call stack is used to keep track of all the function calls</h3>

<h2>Map, filter & reduce</h2>
<h3>Map</h3>

```
const arr = [1,2,3,4];

const newarr = arr.map((item,index,array)=>{
    return item*10;
})
```

<h3>Filter</h3>

```
const arr = [1,2,3,4];

const grtrthan2 = arr.filter((item,index,array)=>{
    return item>2;    //returns items whose callback functions return true
})
```

<h3>Reduce</h3>

```
const arr = [1,2,3,4];

const sum = arr.reduce((accumulator,item,index,array)=>{
    return accumulator+item;
},0)   //if we dont provide the initial value for accumulator it takes the value of first element by default & starts the iteration from second element
```

<h2>Polyfills for map, filter & reduce</h2>

**When we use the map function we define the callback function that dictates/returns the value to be added in the new array**

<h3>map</h3>

```
Array.prototype.myMap = function(cb){
    let newarr = [];
    
    for(let i=0;i<this.length;i++){
        newarr.push(cb(this[i],i,this))
    }
    return newarr;
}
```

<h3>filter</h3>

```
Array.prototype.myFilter = function(cb){
    let newarr = [];
    
    for(let i=0;i<this.length;i++){
        if(cb(this[i],i,this)) newarr.push(this[i]);
    }
    return newarr;
}
```

<h3>reduce</h3>

```
Array.prototype.myReduce = function(cb,initialValue){
    let accumulator = initialValue;
    
    for(let i=0;i<this.length;i++){
       if(accumulator){
       accumulator = cb(accumulator,this[i],i,this)
       }
       else{
       accumulator = this[i]
       }
    }
    return acuumulator;
}
```

<h3>map v/s forEach</h3>

** forEach lets us iterate through the array, doesn't return anything **

```
const avengers = ['thor', 'captain america', 'hulk'];
avengers.forEach((item, index)=>{
	console.log(index, item)
})
```

<h2>Functions</h2>

<h3>Function declaration/definition/statement</h3>
**Normal function**

```
function square(num){
	return num*num;
}
```

<h3>Function Expression</h3>

**When you store function inside a variable**

```
const square = function(num){
	return num*num;
}
```

**RHS of above; i.e a function without a name is known as an anonymous function, can be assigned to a variable or passed as a callback function**

<h3>First Class Function</h3>

**First class function are those that can be treated as variables i.e they can be passed & returned from other functions**

```
function square(num){
	return num*num;
}
function displaySquare(fn){
	console.log("square is" + fn(5));
}
displaySquare(square);
```

<h3>IIFE</h3>

**Immediately invoked Function Expressions: functions that are invoked just after writing them**

```
(function square(num){
	console.log(num*num);
})(5);
```

**Reminder - var is function scope, let & const are block scope**
Eg:

```
for(var i=0;i<5;i++){
    setTimeout(function(){
        console.log("i is passed in console as ",i);
    },i*1000)
}
output = 5 5 5 5 5

for(let i=0;i<5;i++){
    setTimeout(function(){
        console.log("i is passed in console as ",i);
    },i*1000)
}

output = 0 1 2 3 4
```

<h3>Reminder - Functions are hoisted completely with definition at top</h3>

<h3>Paramters vs Arguments</h3>

** Arguments are values passed to a function**
** Paramters are the variables that recieve those values in the function definition**

<h2> ... Spread & Rest operator</h2>
<h3>Spread - Distributes the variables from an array or object</h3>

```
nums = [1,2,3,4]
function mutiply(a,b,c,d){
	//function body
}
function multiply(...nums)
```

<h3>Rest - Collects multiple variables passed as arguments & presents them as an array to us</h3>

**func(a, b, ...nums)**

<h2>Callback function</h2>

**Callback function is a function that is passed as an argument to another function, which is then invoked inside the outer function**

**The function that recieves a callback function as an argument is called a Higher order function**

**Functions in js are first class members, they csn be treated as variables**

<h2>Arrow Functions</h2>

```
const arrowfunction = (num1,num2) => {
	return num1+num2
}
```

<h2>Arguments</h2>

```
const square = function(){
	console.log(arguments);
}

square(1,2,3,4,5)     // arguments will give us all the arguments, This arguments keyword is not available in arrow functions
```

<h3>This keyword</h3>

```
let user = {
	username:"rahul"
	rc1: () => { console.log(this.username) }       //this keyword points to global object
	rc2: function() { console.log(this.username) }  // this keyword points to object that this function is a part of
}
```

<h2>Closures</h2>

<h3>Everytime a function is defined, a closure is formed with it</h3>

**A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function's scope from an inner function.**
**Lexical Scope allows inner functions to access the scope of their outer functions. const and let are block scoped variables.**
**Scope determines the accessibility of variables, objects, and functions from different parts of the code.**
***Closure Scope chain - a closure has access to local, parent's & global scope when it is nested (we already know that)***

```
Eg-1
var name = "Global scope"

function outer(){
    var name = "inside function scope"
    return function inner(){
        console.log(name);
    }
}

const newfunc = outer();
newfunc();   // output => inside function scope
// newfunc() knows the value of variable "name" because along with the function definition, it also carries it's lexical enviornment i.e it's a closure.

Eg-2

function createBase(num)
{
    return function addsix(innernum){
        return num+innernum;
    }
}

const addsix = createBase(6);
console.log(addsix(10)); //16
console.log(addsix(20)); //26
```

***Important - How to run a loop with var without referencing to the same value in an asynchronous function***

```
for(var i=0;i<10;i++){

    (function(passed){setTimeout(function(){
        console.log(passed);
    }, i*1000)})(i);
}
//we took advantage by forming a closure of every iteration of i that is passed by wrapping asynchronous function in a wrapper function that takes current value of i & forms a closure with it
```

```
Important question

function fun(){
    var _counter = 0;

    function add(val){
        _counter+=val;
    }
    function retrieve(){
        return _counter;
    }

    return {
        add,
        retrieve
    }

}

const c1 = fun();
c1.add(10)
console.log(c1.retrieve());
```

<h3>Ques. What is Module Pattern?</h3>

<h2>Hiding private functions & allowing public functions to be accessible from inside a fucntion</h2>

```
function modulePattern(){
    function privatefunction(){
        console.log("I am private");
    }
    
    return {
        publicfunction : function publicfunction(){
            console.log("I am public");
        },
        publicfunction2 : function publicfunction2(){
            console.log("I am public2");
        }
    }
}

modulePattern().privatefunction();    //unsupported syntax, Hence protected
modulePattern().publicfunction();     //I am public
modulePattern().publicfunction2();    //I am public2
```

<h3>once(fun) & memoize(fun)</h3>

<h2>Currying</h2>
In currying a function takes one argument at a time & returns another function expecting the next argument
f(a,b) is converted to f(a)(b) with currying

```
function normal(a,b){
    console.log(a,b);
}
normal(1,2)

// converting into curried function
function f(a){
    return function (b){
        console.log(a,b);
    }
}

f(3)(4)
```

Ques - Why should currying be used?
Following are the reasons why currying is good :

✅ It makes a function pure which makes it expose to less errors and side effects.

✅ It helps in avoiding the same variable again and again.

✅ It is a checking method that checks if you have all the things before you proceed.

✅ It divides one function into multiple functions so that one handles one set of responsibility.

```
function evaluate(operation) {
    return (a) => {
        return (b) => {
        if(operation === "sum")
                  return a + b;
                    else if(operation === "multiply")
                    return a * b;
                    else if(operation === "divide")
                    return a / b;
                    else if(operation === "subtract")
                    return a - b;
                    else return "No / Invalid Operation Selected"
        }
    }
}

const mul = evaluate("multiply");
console.log(mul(1)(2));   //2
console.log(mul(5)(2));   //10
```

Question - How to implement infinite currying

```
function add(a){
    return function (b){
        if(b) return add(a+b);
        else return a;
    }
}

console.log(add(1)(2)(3)(4)(5)());
```

Ques - Partial application is different from currying

```
function sum(a) {
    return function (b, c) {
        return a * b * c
    }
}

const x = sum(10);

console.log(x(1,2));
console.log(x(3,2));
```

Ques - Currying can be used to manipulate Dom elements

```
function updateElement(id){
    return function(content){
        document.querySelector("#"+id).textContent=content;
    }
}

const selectedele = updateElement('id');
selectedele("WE NEED TO COOK JESSE")
```

Ques - Curry Implementation

<h2>Objects</h2>
Objects are a collection of key & property values

```
let car = {
    brand: "honda",
    color : "red",
    type : "AWD"
}

delete car.brand   // deletes property
console.log(car);  //{color: 'red', type: 'AWD'}

let property_var = "firstname"
let value = "john",
car={
   "property with spaces": true,
   [property_var] : value
}

console.log(car[property with spaces])    //Accessed using
```

<h3>Traverse Object</h3>

```
let car = {
    brand: "honda",
    color : "red",
    type : "AWD"
}

for(key in car){
    console.log(car[key]);
}
```

Ques - Double all numeric values of object

```
let car = {
    num1: 40,
    num2: 60,
    type : "AWD"
}

for(key in car){
    if(typeof(car[key]) == "number") car[key] = car[key]*2;
    console.log(car[key]);
}

//curry function for the same

function currydouble(obj){
    return function (n){
        for(key in obj){
            if(typeof(car[key]) == "number") car[key] = car[key]*2;
        }
    }
}

let x = currydouble(car);
x(2);
console.log(car);
```

**objects can't be passed as keys to other objects, it's read as "object Object"**

Ques - What's JSON.stringify() & JSON.parse()
Ans - Object to string & string to object conversion.

```
let car = {
    num1: 40,
    num2: 60,
    type : "AWD"
}

const stringfromobject = JSON.stringify(car);

localStorage.setItem("carobj",stringfromobject);

const retrieve = localStorage.getItem("carobj")
const objectfromstring = JSON.parse(retrieve);

console.log(objectfromstring.num1);
```

Ques - Spread an object inside other

```
let car = {
    num1: 40,
    num2: 60,
    type : "AWD"
}

const newobj = {
    hp:1000,
    ...car
}

console.log(newobj);
```

Ques - What is destructuring in objects?
**Destructuring is a feature in JavaScript that allows you to extract values from arrays and objects into distinct variables.**

```
let car = {
    num1: 40,
    num2: 60,
    type : "AWD"
}

const { num1, type} = car       //Destructuring Object (use square brackets for Array destructuring)
console.log(num1, type);

const { num1 : customname, type:drivetype} = car  // Giving Custom name to destructured variables
console.log(customname, drivetype);
```

Ques - How to copy an Object to another

```
let car = {
    num1: 40,
    num2: 60,
    type : "AWD"
}

const newcar = car;
newcar.type = "4WD";

// doing a=b only copies reference, so they're not independent copies
```

Ques - What's a shallow copy & a deep copy
A shallow copy may contain some references from the original object, but a deep copy is a complete clone & has no reference to the original object
We can make a deep copy by stringifying & then parsing the object.

<h2>This Keyword</h2>

```
this.name = "global object"

let car = {
    name: "inside object",
    insidefun : function() {
        console.log(this.name);      // inside object => this always points to parent object
    },
    childobj : {
        name : "nested child name",

        childfunc : function() {
            console.log(this.name);  // nested child name => this always points to parent object
        },

        arrowfunin : ()=>{
            console.log(this.name);  // global object => this always points to global object
        }
    },

    arrowfun : () =>{
        console.log(this.name);      //global object => this always points to global object
    }
}

car.childobj.arrowfunin()
```

**When arrow function points to normal parent function instead of global object**

```
this.name = "global object"

let car = {
    name: "inside object",
    
    childobj : {
        name : "nested child name",
        childfunc : function() {          //arrow function points here
            const arrowfunin = ()=>{
                console.log(this.name);  // global object => this always points to global object or parent normal function
            }
            arrowfunin()
        },
    }

}

car.childobj.childfunc()            //nested child name
```

Ques - make a calc

```
const calc = {
    total: 0 ,
    add(a){
        this.total += Number(a);
        return this
    },
    subtract(b){
        this.total -= Number(b);
        return this
    },
    mulitply(c){
        this.total *= Number(c);
        return this
    },
    result(){
        return this.total
    }
}

const x = calc.add(10).add(20).mulitply(2).result();
console.log(x);
```

<h2>Promises</h2>

<h3>Why do we use promises</h3>

**When executing asynchronous code, if we want to execute it in order after some another asynchronous code has executed, we write nested callback functions, This leads to complicated code called Callback Hell**</br>

```
function callback1(message){
    setTimeout(() => {
        console.log("first callback " + message);

        function callback2(){
            setTimeout(()=>{
                console.log("second callback " + message);

                function callback3(){
                    setTimeout(()=>{
                        console.log("second callback " + message);

                        function callback4(){
                            setTimeout(()=>{
                                console.log("second callback " + message);
                            },0)
                        }
                        callback4()
                    },0)
                }
                callback3()

            },0)
        }
        callback2()
    },0)
}

callback1("hello")
```

**To avoid this problem we use promises**</br>

A Promise is in one of these states:</br>
pending: initial state, neither fulfilled nor rejected.</br>
fulfilled: meaning that the operation was completed successfully.</br>
rejected: meaning that the operation failed.</br>


<h3>How to make & use new promises</h3>

```
const np = new Promise((resolve, reject) =>{
    // logic to sent WHAT back via resolve & reject
    if(false){
    resolve("ResloveDataSent - this is the data sent back to promise when then is succesfully executed")
    }
    else{
    reject("errorDataSent - this is sent back to promise when it is not resolved")
    }
})

np.then((resloveDataRecieved) =>{
    console.log(resloveDataRecieved);
}).catch((errorDataRecieved)=>{
    console.log(errorDataRecieved);
})

```
Eg-2

```
const myPromise = new Promise((resolve, reject) => {
  // make a network request
  fetch('https://example.com/data')
    .then(response => response.json())
    .then(data => {
      // resolve the Promise with the retrieved data
      resolve(data);
    })
    .catch(error => {
      // reject the Promise if there was an error
      reject(error);
    });
});

myPromise
  .then(data => {
    // handle the resolved data
    console.log(data);
  })
  .catch(error => {
    // handle any errors that occurred during the Promise's execution
    console.log(error);
  });
```

**Promises are asynchronous by themselves & they resolve after all of the synchronous code has been executed**

```
const np = new Promise((resolve, reject) =>{
    // logic to sent WHAT back via resolve & reject
    if(true){
    resolve("ResloveDataSent - this is the data sent back to promise when then is succesfully executed")
    }
    else{
    reject("errorDataSent - this is sent back to promise when it is not resolved")
    }
})

console.log("start");
console.log(np);

np.then(data=>{
    console.log("start");    //this will be executed at last as it is asynchronous code
})

console.log("end");

output :-

start
index.js:12 Promise {<fulfilled>: 'ResloveDataSent - this is the data sent back to promise when then is succesfully executed'}
index.js:16 end
index.js:14 ResloveDataSent - this is the data sent back to promise when then is succesfully executed

```

<h3>How to chain promises</h3>

```
function fun1(){
    return new Promise((resolve,reject)=>{
        resolve("hello i am first promise");
    })
}

function fun2(){
    return new Promise((resolve,reject)=>{
        resolve("hello i am second promise");
    })
}

function fun3(){
    return new Promise((resolve,reject)=>{
        resolve("hello i am third promise");
    })
}

fun1().then(data=>{
    console.log(data)
    return fun2()
}).then(data=>{
    console.log(data)
    return fun3()
}).then(data=>{
    console.log(data)
})
```

<h3>Using Promise.all to run multiple promises at once & return them in the order provided, if any single promise is not resolved then it will not return anything</h3>

```
const promise1 = new Promise(resolve => setTimeout(() => resolve("Promise 1"), 1000));
const promise2 = new Promise(resolve => setTimeout(() => resolve("Promise 2"), 500));
const promise3 = new Promise(resolve => setTimeout(() => resolve("Promise 3"), 2000));

Promise.all([promise1, promise2, promise3]).then(values => {
  console.log(values);
});
```

<h3>Promise.race</h3>

**Promise.race() takes an array of promises as an argument & it returns the promise that is first settled out of all the promises in the array, doesn't matter if it is resolved or rejected**

```
const promise1 = new Promise(resolve => setTimeout(() => resolve("Promise 1"), 1000));
const promise2 = new Promise(resolve => setTimeout(() => resolve("Promise 2"), 500));
const promise3 = new Promise(resolve => setTimeout(() => resolve("Promise 3"), 2000));

Promise.race([promise1, promise2, promise3]).then(value => {
  console.log(value);
});

output => promise2
```
