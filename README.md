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
