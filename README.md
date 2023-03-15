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
